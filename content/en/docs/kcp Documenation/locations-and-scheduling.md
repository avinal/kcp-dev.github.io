---
title: "Locations and Scheduling"
linkTitle: "Locations and Scheduling"
description: "This section contains kcp locations and scheduling documentation."
weight: 5
---


KCP implements *Compute as a Service* via a concept of Transparent Multi Cluster (TMC). TMC means that
Kubernetes clusters are attached to a kcp installation to execute workload objects from the users'
workspaces by syncing these workload objects down to those clusters and the objects' status
back up. This gives the illusion of native compute in KCP.

We call it *Compute as a Service* because the registered `SyncTargets` live in workspaces that
are (normally) invisible to the users, and the teams operating compute can be different from
the compute consumers.

The APIs used for Compute as a Service are:

1. `scheduling.kcp.dev/v1alpha1` – we call the outcome of this *placement* of namespaces.
2. `workload.kcp.dev/v1alpha1` – responsible for the syncer component of TMC.

## Main Concepts

- `SyncTarget` in `workload.kcp.dev/v1alpha1` – representations of Kubernetes clusters that are attached to a kcp installation to
  execute workload objects from the users' workspaces. On a Kubernetes cluster, there is one syncer
  process for each `SyncTarget` object.

  Sync targets are invisible to users, and (medium term) at most identified via a UID.

- `Location` in `scheduling.kcp.dev/v1alpha1` – represents a collection of `SyncTarget` objects selected via instance labels, and
  exposes labels (potentially different from the instance labels) to the users to describe, identify and select locations to be used
  for placement of user namespaces onto sync targets.

  Locations are visible to users, but owned by the compute service team, i.e. read-only to the users and only projected
  into their workspaces for visibility. A placement decision references a location by name.

  `SyncTarget`s in a `Location` are transparent to the user. Workloads should be able to seamlessly move from one `SyncTarget` to another
  within a `Location`, based on operational concerns of the compute service provider, like decommissioning a cluster, rebalancing
  capacity, or due to an outage of a cluster.
  
  It is compute service's responsibility to ensure that for workloads in a location, to the user it looks like ONE cluster.

- `Placement` in `scheduling.kcp.dev/v1alpha1` – represents a selection rule to choose ONE `Location` via location labels, and bind
  the selected location to MULTIPLE namespaces in a user workspace. For Workspaces with multiple Namespaces, users can create multiple
  Placements to assign specific Namespace(s) to specific Locations.

  `Placement` are visible and writable to users. A default `Placement` is automatically created when a workload `APIBinding` is
  created on the user workspace, which randomly select a `Location` and bind to all namespaces in this workspace. The user can mutate
  or delete the default `Placement`. The corresponding `APIBinding` will be annotated with `workload.kcp.dev/skip-default-object-creation`,
  so that the default `Placement` will not be recreated upon deletion.

- *Compute Service Workspace* (previously *Negotiation Workspace*) – the workspace owned by the compute service team to hold
  the `APIExport` (named `kubernetes` today) with the synced resources, and `SyncTarget` and `Location` objects.

  The user binds to the `APIExport` called `kubernetes` using an `APIBinding`. From this moment on, the users' workspaces
  are subject to placement.

Note: binding to a compute service is a permanent decision. Unbinding (i.e. deleting of the APIBinding object) means deletion of the
workload objects.

Note: it is planned to allow multiple location workspaces for the same compute service, even with different owners.

### Placement and resource scheduling

The placement state is one of

- `Pending` – the placement controller waits for a valid `Location` to select
- `Bound` – at least one namespace is bound to the placement. When the user updates the spec of the `Placement`, the selected location of
  the placement will be changed in `Bound` state.
- `Unbound` – a location is selected by the placement, but no namespace is bound to the placement. When the user updates the spec of the `Placement`, the
  selected location of the placement will be changed in `Unbound` state.

Note: sync targets from different locations can be bound at the same time, while each location can only have one sync target bound to the
namespace.

The user interface to influence the placement decisions is the `Placement` object. For example, use can create a placement to bind namespace with
label of "app=foo" to a location with label "cloud=aws" as below:

```yaml
apiVersion: scheduling.kcp.dev/v1alpha1
kind: Placement
metadata:
  name: aws
spec:
  locationSelectors:
  - matchLabels:
      cloud: aws
  namespaceSelector:
    matchLabels:
      app: foo
  locationWorkspace: root:default:location-ws
```

A matched location will be selected for this `Placement` at first, which makes the `Placement` turns from `Pending` to `Unbound`. Then if there is at
least one matching Namespace, the Namespace will be annotated with `scheduling.kcp.dev/placement` and the placement turns from `Unbound` to `Bound`.
After this, a `SyncTarget` will be selected from the location picked by the placement.  `state.workload.kcp.dev/<cluster-id>` label with value of `Sync` will be set if a valid `SyncTarget` is selected.

The user can create another placement targeted to a different location for this Namespace, e.g.

```yaml
apiVersion: scheduling.kcp.dev/v1alpha1
kind: Placement
metadata:
  name: gce
spec:
  locationSelectors:
  - matchLabels:
      cloud: gce
  namespaceSelector:
    matchLabels:
      app: foo
  locationWorkspace: root:default:location-ws
```

which will result in another `state.workload.kcp.dev/<cluster-id>` label added to the Namespace, and the Namespace will have two different
`state.workload.kcp.dev/<cluster-id>` label.

Placement is in the `Ready` status condition when

1. selected location matches the `Placement` spec.
2. selected location exists in the location workspace.

#### Sync target removing

A sync target will be removed when:

1. corresponding `Placement` is deleted.
2. corresponding `Placement` is not in `Ready` condition.
3. corresponding `SyncTarget` is evicting/not Ready/deleted

All above cases will make the `SyncTraget` represented in the label `state.workload.kcp.dev/<cluster-id>` invalid, which will cause
`finalizers.workload.kcp.dev/<cluster-id>` annotation with removing time in the format of RFC-3339 added on the Namespace.

### Resource Syncing

As soon as the `state.workload.kcp.dev/<cluster-id>` label is set on the Namespace, the workload resource controller will
copy the `state.workload.kcp.dev/<cluster-id>` label to the resources in that namespace.

Note: in the future, the label on the resources is first set to empty string `""`, and a coordination controller will be
able to apply changes before syncing starts. This includes the ability to add per-location finalizers through the
`finalizers.workload.kcp.dev/<cluster-id>` annotation such that the coordination controller gets full control over
the downstream life-cycle of the objects per location (imagine an ingress that blocks downstream removal until the new replicas
have been launched on another sync target). Finally, the coordination controller will replace the empty string with `Sync`
such that the state machine continues.

With the state label set to `Sync`, the syncer will start seeing the resources in the namespace
and starts syncing them downstream, first by creating the namespace. Before syncing, it will also set
a finalizer `workload.kcp.dev/syncer-<cluster-id>` on the upstream object in order to delay upstream deletion until
the downstream object is also deleted.

When the `deletion.internal.workload.kcp.dev/<cluster-id>` is added to the Namespace. The virtual workspace apiserver
will translate that annotation into a deletion timestamp on the object the syncer sees. The syncer
notices that as a started deletion flow. As soon as there are no coordination controller finalizers registered via the
`finalizers.workload.kcp.dev/<cluster-id>` annotation anymore, the syncer will start a deletion of the downstream object.

When the downstream deletion is complete, the syncer will remove the finalizer from the upstream object, and the
`state.workload.kcp.dev/<cluster-id>` labels gets deleted as well. The syncer stops seeing the object in the virtual
workspace.

Note: there is a missing bit in the implementation (in v0.5) about removal of the `state.workload.kcp.dev/<cluster-id>`
label from namespaces: the syncer currently does not participate in the namespace deletion state-machine, but has to and signal finished
downstream namespace deletion via `state.workload.kcp.dev/<cluster-id>` label removal.
