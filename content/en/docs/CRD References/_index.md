---
title: "CRD References"
linkTitle: "CRD References"
description: "Reference documentation for CRDs in kcp"
weight: 40
---

## Packages

- [apiresource.kcp.dev/v1alpha1](#apiresourcekcpdevv1alpha1)
- [apis.kcp.dev/v1alpha1](#apiskcpdevv1alpha1)
- [scheduling.kcp.dev/v1alpha1](#schedulingkcpdevv1alpha1)
- [tenancy.kcp.dev/v1alpha1](#tenancykcpdevv1alpha1)
- [tenancy.kcp.dev/v1beta1](#tenancykcpdevv1beta1)
- [workload.kcp.dev/v1alpha1](#workloadkcpdevv1alpha1)

## apiresource.kcp.dev/v1alpha1

#### APIResourceImport

APIResourceImport describes an API resource imported from external clusters (either physical or logical) for a given GVR.

_Appears in:_

- [APIResourceImportList](#apiresourceimportlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[APIResourceImportSpec](#apiresourceimportspec)_ |  |
| `status` _[APIResourceImportStatus](#apiresourceimportstatus)_ |  |

#### APIResourceImportCondition

APIResourceImportCondition contains details for the current condition of this negotiated api resource.

_Appears in:_

- [APIResourceImportStatus](#apiresourceimportstatus)

| Field | Description |
| --- | --- |
| `type` _[APIResourceImportConditionType](#apiresourceimportconditiontype)_ | Type is the type of the condition. Types include Compatible. |
| `status` _[ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#conditionstatus-v1-meta)_ | Status is the status of the condition. Can be True, False, Unknown. |
| `lastTransitionTime` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#time-v1-meta)_ | Last time the condition transitioned from one status to another. |
| `reason` _string_ | Unique, one-word, CamelCase reason for the condition's last transition. |
| `message` _string_ | Human-readable message indicating details about last transition. |

#### APIResourceImportConditionType

_Underlying type:_ `string`

APIResourceImportConditionType is a valid value for APIResourceImportCondition.Type

_Appears in:_

- [APIResourceImportCondition](#apiresourceimportcondition)

#### APIResourceImportSpec

APIResourceImportSpec holds the desired state of the APIResourceImport (from the client).

_Appears in:_

- [APIResourceImport](#apiresourceimport)

| Field | Description |
| --- | --- |
| `CommonAPIResourceSpec` _[CommonAPIResourceSpec](#commonapiresourcespec)_ |  |
| `schemaUpdateStrategy` _[SchemaUpdateStrategyType](#schemaupdatestrategytype)_ | SchemaUpdateStrategy defines the schema update strategy for this API Resource import. Default value is UpdateUnpublished |
| `location` _string_ | Locaton the API resource is imported from This field is required |

#### APIResourceImportStatus

APIResourceImportStatus communicates the observed state of the APIResourceImport (from the controller).

_Appears in:_

- [APIResourceImport](#apiresourceimport)

| Field | Description |
| --- | --- |
| `conditions` _[APIResourceImportCondition](#apiresourceimportcondition) array_ |  |

#### ColumnDefinition

_Appears in:_

- [CommonAPIResourceSpec](#commonapiresourcespec)

| Field | Description |
| --- | --- |
| `TableColumnDefinition` _[TableColumnDefinition](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#tablecolumndefinition-v1-meta)_ |  |
| `jsonPath` _string_ |  |

#### CommonAPIResourceSpec

CommonAPIResourceSpec holds the common content of both NegotiatedAPIResourceSpec and APIResourceImportSpec.

_Appears in:_

- [APIResourceImportSpec](#apiresourceimportspec)
- [NegotiatedAPIResourceSpec](#negotiatedapiresourcespec)

| Field | Description |
| --- | --- |
| `groupVersion` _[GroupVersion](#groupversion)_ |  |
| `scope` _ResourceScope_ |  |
| `CustomResourceDefinitionNames` _[CustomResourceDefinitionNames](#customresourcedefinitionnames)_ |  |
| `openAPIV3Schema` _[RawExtension](#rawextension)_ |  |
| `subResources` _[SubResource](#subresource) array_ |  |
| `columnDefinitions` _[ColumnDefinition](#columndefinition) array_ |  |

#### GroupVersion

_Appears in:_

- [CommonAPIResourceSpec](#commonapiresourcespec)

| Field | Description |
| --- | --- |
| `group` _string_ |  |
| `version` _string_ |  |

#### NegotiatedAPIResource

NegotiatedAPIResource describes the result of either the normalization of any number of imports of an API resource from external clusters (either physical or logical), or the the manual application of a CRD version for the corresponding GVR.

_Appears in:_

- [NegotiatedAPIResourceList](#negotiatedapiresourcelist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[NegotiatedAPIResourceSpec](#negotiatedapiresourcespec)_ |  |
| `status` _[NegotiatedAPIResourceStatus](#negotiatedapiresourcestatus)_ |  |

#### NegotiatedAPIResourceCondition

NegotiatedAPIResourceCondition contains details for the current condition of this negotiated api resource.

_Appears in:_

- [NegotiatedAPIResourceStatus](#negotiatedapiresourcestatus)

| Field | Description |
| --- | --- |
| `type` _[NegotiatedAPIResourceConditionType](#negotiatedapiresourceconditiontype)_ | Type is the type of the condition. Types include Submitted, Published, Refused and Enforced. |
| `status` _[ConditionStatus](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#conditionstatus-v1-meta)_ | Status is the status of the condition. Can be True, False, Unknown. |
| `lastTransitionTime` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#time-v1-meta)_ | Last time the condition transitioned from one status to another. |
| `reason` _string_ | Unique, one-word, CamelCase reason for the condition's last transition. |
| `message` _string_ | Human-readable message indicating details about last transition. |

#### NegotiatedAPIResourceConditionType

_Underlying type:_ `string`

NegotiatedAPIResourceConditionType is a valid value for NegotiatedAPIResourceCondition.Type

_Appears in:_

- [NegotiatedAPIResourceCondition](#negotiatedapiresourcecondition)

#### NegotiatedAPIResourceSpec

NegotiatedAPIResourceSpec holds the desired state of the NegotiatedAPIResource (from the client).

_Appears in:_

- [NegotiatedAPIResource](#negotiatedapiresource)

| Field | Description |
| --- | --- |
| `CommonAPIResourceSpec` _[CommonAPIResourceSpec](#commonapiresourcespec)_ |  |
| `publish` _boolean_ |  |

#### NegotiatedAPIResourceStatus

NegotiatedAPIResourceStatus communicates the observed state of the NegotiatedAPIResource (from the controller).

_Appears in:_

- [NegotiatedAPIResource](#negotiatedapiresource)

| Field | Description |
| --- | --- |
| `conditions` _[NegotiatedAPIResourceCondition](#negotiatedapiresourcecondition) array_ |  |

#### SchemaUpdateStrategyType

_Underlying type:_ `string`

SchemaUpdateStrategy defines the strategy for updating the correspondoing negotiated API resource based on the schema of this API Resource Import

_Appears in:_

- [APIResourceImportSpec](#apiresourceimportspec)

#### SubResource

_Appears in:_

- [CommonAPIResourceSpec](#commonapiresourcespec)

| Field | Description |
| --- | --- |
| `name` _string_ |  |

## apis.kcp.dev/v1alpha1

#### APIBinding

APIBinding enables a set of resources and their behaviour through an external service provider in this workspace.
 The service provider uses an APIExport to expose the API.

_Appears in:_

- [APIBindingList](#apibindinglist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[APIBindingSpec](#apibindingspec)_ | Spec holds the desired state. |
| `status` _[APIBindingStatus](#apibindingstatus)_ | Status communicates the observed state. |

#### APIBindingPhaseType

_Underlying type:_ `string`

APIBindingPhaseType is the type of the current phase of an APIBinding.

_Appears in:_

- [APIBindingStatus](#apibindingstatus)

#### APIBindingSpec

APIBindingSpec records the APIs and implementations that are to be bound.

_Appears in:_

- [APIBinding](#apibinding)

| Field | Description |
| --- | --- |
| `reference` _[ExportReference](#exportreference)_ | reference uniquely identifies an API to bind to. |
| `permissionClaims` _[AcceptablePermissionClaim](#acceptablepermissionclaim) array_ | permissionClaims records decisions about permission claims requested by the API service provider. Individual claims can be accepted or rejected. If accepted, the API service provider gets the requested access to the specified resources in this workspace. Access is granted per GroupResource, identity, and other properties. |

#### APIBindingStatus

APIBindingStatus records which schemas are bound.

_Appears in:_

- [APIBinding](#apibinding)

| Field | Description |
| --- | --- |
| `boundExport` _[ExportReference](#exportreference)_ | boundExport records the export this binding is bound to currently. It can differ from the export that was specified in the spec while rebinding to a different APIExport.
 This field is what gives the APIExport visibility into the objects in this workspace. |
| `boundResources` _[BoundAPIResource](#boundapiresource) array_ | boundResources records the state of bound APIs. |
| `phase` _[APIBindingPhaseType](#apibindingphasetype)_ | phase is the current phase of the APIBinding: - "": the APIBinding has just been created, waiting to be bound. - Binding: the APIBinding is being bound. - Bound: the APIBinding is bound and the referenced APIs are available in the workspace. |
| `conditions` _[Condition](#condition) array_ | conditions is a list of conditions that apply to the APIBinding. |
| `appliedPermissionClaims` _[PermissionClaim](#permissionclaim) array_ | appliedPermissionClaims is a list of the permission claims the system has seen and applied, according to the requests of the API service provider in the APIExport and the acceptance state in spec.permissionClaims. |
| `exportPermissionClaims` _[PermissionClaim](#permissionclaim) array_ | exportPermissionClaims records the permissions that the export provider is asking for the binding to grant. |

#### APIExport

APIExport registers an API and implementation to allow consumption by others through APIBindings.
 APIExports cannot be deleted until status.resourceSchemasInUse is empty.

_Appears in:_

- [APIExportList](#apiexportlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[APIExportSpec](#apiexportspec)_ | Spec holds the desired state. |
| `status` _[APIExportStatus](#apiexportstatus)_ | Status communicates the observed state. |

#### APIExportSpec

APIExportSpec defines the desired state of APIExport.

_Appears in:_

- [APIExport](#apiexport)

| Field | Description |
| --- | --- |
| `latestResourceSchemas` _string array_ | latestResourceSchemas records the latest APIResourceSchemas that are exposed with this APIExport.
 The schemas can be changed in the life-cycle of the APIExport. These changes have no effect on existing APIBindings, but only on newly bound ones.
 For updating existing APIBindings, use an APIDeployment keeping bound workspaces up-to-date. |
| `identity` _[Identity](#identity)_ | identity points to a secret that contains the API identity in the 'key' file. The API identity determines an unique etcd prefix for objects stored via this APIExport.
 Different APIExport in a workspace can share a common identity, or have different ones. The identity (the secret) can also be transferred to another workspace when the APIExport is moved.
 The identity is a secret of the API provider. The APIBindings referencing this APIExport will store a derived, non-sensitive value of this identity.
 The identity of an APIExport cannot be changed. A derived, non-sensitive value of the identity key is stored in the APIExport status and this value is immutable.
 The identity is defaulted. A secret with the name of the APIExport is automatically created. |
| `maximalPermissionPolicy` _[MaximalPermissionPolicy](#maximalpermissionpolicy)_ | maximalPermissionPolicy will allow for a service provider to set an upper bound on what is allowed for a consumer of this API. If the policy is not set, no upper bound is applied, i.e the consuming users can do whatever the user workspace allows the user to do.
 The policy consists of RBAC (Cluster)Roles and (Cluster)Bindings. A request of a user in a workspace that binds to this APIExport via an APIBinding is additionally checked against these rules, with the user name and the groups prefixed with `apis.kcp.dev:binding:`.
 For example: assume a user `adam` with groups `system:authenticated` and `a-team` binds to this APIExport in another workspace root:org:ws. Then a request in that workspace against a resource of this APIExport is authorized as every other request in that workspace, but in addition the RBAC policy here in the APIExport workspace has to grant access to the user `apis.kcp.dev:binding:adam` with the groups `apis.kcp.dev:binding:system:authenticated` and `apis.kcp.dev:binding:a-team`. |
| `permissionClaims` _[PermissionClaim](#permissionclaim) array_ | permissionClaims make resources available in APIExport's virtual workspace that are not part of the actual APIExport resources.
 PermissionClaims are optional and should be the least access necessary to complete the functions that the service provider needs. Access is asked for on a GroupResource + identity basis.
 PermissionClaims must be accepted by the user's explicit acknowledgement. Hence, when claims change, the respecting objects are not visible immediately.
 PermissionClaims overlapping with the APIExport resources are ignored. |

#### APIExportStatus

APIExportStatus defines the observed state of APIExport.

_Appears in:_

- [APIExport](#apiexport)

| Field | Description |
| --- | --- |
| `identityHash` _string_ | identityHash is the hash of the API identity key of this APIExport. This value is immutable as soon as it is set. |
| `conditions` _[Condition](#condition) array_ | conditions is a list of conditions that apply to the APIExport. |
| `virtualWorkspaces` _[VirtualWorkspace](#virtualworkspace) array_ | virtualWorkspaces contains all APIExport virtual workspace URLs. |

#### APIResourceSchema

APIResourceSchema describes a resource, identified by (group, version, resource, schema).
 A APIResourceSchema is immutable and cannot be deleted if they are referenced by an APIExport in the same workspace.

_Appears in:_

- [APIResourceSchemaList](#apiresourceschemalist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[APIResourceSchemaSpec](#apiresourceschemaspec)_ | Spec holds the desired state. |

#### APIResourceSchemaSpec

APIResourceSchemaSpec defines the desired state of APIResourceSchema.

_Appears in:_

- [APIResourceSchema](#apiresourceschema)

| Field | Description |
| --- | --- |
| `group` _string_ | group is the API group of the defined custom resource. Empty string means the core API group.  The resources are served under `/apis/<group>/...` or `/api` for the core group. |
| `names` _[CustomResourceDefinitionNames](#customresourcedefinitionnames)_ | names specify the resource and kind names for the custom resource. |
| `scope` _ResourceScope_ | scope indicates whether the defined custom resource is cluster- or namespace-scoped. Allowed values are `Cluster` and `Namespaced`. |
| `versions` _[APIResourceVersion](#apiresourceversion) array_ | versions is the API version of the defined custom resource.
 Note: the OpenAPI v3 schemas must be equal for all versions until CEL       version migration is supported. |

#### APIResourceVersion

APIResourceVersion describes one API version of a resource.

_Appears in:_

- [APIResourceSchemaSpec](#apiresourceschemaspec)

| Field | Description |
| --- | --- |
| `name` _string_ | name is the version name, e.g. “v1”, “v2beta1”, etc. The custom resources are served under this version at `/apis/<group>/<version>/...` if `served` is true. |
| `served` _boolean_ | served is a flag enabling/disabling this version from being served via REST APIs |
| `storage` _boolean_ | storage indicates this version should be used when persisting custom resources to storage. There must be exactly one version with storage=true. |
| `deprecated` _boolean_ | deprecated indicates this version of the custom resource API is deprecated. When set to true, API requests to this version receive a warning header in the server response. Defaults to false. |
| `deprecationWarning` _string_ | deprecationWarning overrides the default warning returned to API clients. May only be set when `deprecated` is true. The default warning indicates this version is deprecated and recommends use of the newest served version of equal or greater stability, if one exists. |
| `schema` _[RawExtension](#rawextension)_ | schema describes the structural schema used for validation, pruning, and defaulting of this version of the custom resource. |
| `subresources` _[CustomResourceSubresources](#customresourcesubresources)_ | subresources specify what subresources this version of the defined custom resource have. |
| `additionalPrinterColumns` _[CustomResourceColumnDefinition](#customresourcecolumndefinition) array_ | additionalPrinterColumns specifies additional columns returned in Table output. See <https://kubernetes.io/docs/reference/using-api/api-concepts/#receiving-resources-as-tables> for details. If no columns are specified, a single column displaying the age of the custom resource is used. |

#### AcceptablePermissionClaim

AcceptablePermissionClaim is a PermissionClaim that records if the user accepts or rejects it.

_Appears in:_

- [APIBindingSpec](#apibindingspec)

| Field | Description |
| --- | --- |
| `PermissionClaim` _[PermissionClaim](#permissionclaim)_ |  |
| `state` _[AcceptablePermissionClaimState](#acceptablepermissionclaimstate)_ |  |

#### AcceptablePermissionClaimState

_Underlying type:_ `string`

_Appears in:_

- [AcceptablePermissionClaim](#acceptablepermissionclaim)

#### BoundAPIResource

BoundAPIResource describes a bound GroupVersionResource through an APIResourceSchema of an APIExport..

_Appears in:_

- [APIBindingStatus](#apibindingstatus)

| Field | Description |
| --- | --- |
| `group` _string_ | group is the group of the bound API. Empty string for the core API group. |
| `resource` _string_ | resource is the resource of the bound API.
 kubebuilder:validation:MinLength=1 |
| `schema` _[BoundAPIResourceSchema](#boundapiresourceschema)_ | Schema references the APIResourceSchema that is bound to this API. |
| `storageVersions` _string array_ | storageVersions lists all versions of a resource that were ever persisted. Tracking these versions allows a migration path for stored versions in etcd. The field is mutable so a migration controller can finish a migration to another version (ensuring no old objects are left in storage), and then remove the rest of the versions from this list.
 Versions may not be removed while they exist in this list. |

#### BoundAPIResourceSchema

BoundAPIResourceSchema is a reference to an APIResourceSchema.

_Appears in:_

- [BoundAPIResource](#boundapiresource)

| Field | Description |
| --- | --- |
| `name` _string_ | name is the bound APIResourceSchema name. |
| `UID` _string_ | UID is the UID of the APIResourceSchema that is bound to this API. |
| `identityHash` _string_ | identityHash is the hash of the API identity that this schema is bound to. The API identity determines the etcd prefix used to persist the object. Different identity means that the objects are effectively served and stored under a distinct resource. A CRD of the same GroupVersionResource uses a different identity and hence a separate etcd prefix. |

#### ExportReference

ExportReference describes a reference to an APIExport. Exactly one of the fields must be set.

_Appears in:_

- [APIBindingSpec](#apibindingspec)
- [APIBindingStatus](#apibindingstatus)
- [SyncTargetSpec](#synctargetspec)

| Field | Description |
| --- | --- |
| `workspace` _[WorkspaceExportReference](#workspaceexportreference)_ | workspace is a reference to an APIExport in the same organization. The creator of the APIBinding needs to have access to the APIExport with the verb `bind` in order to bind to it. |

#### GroupResource

GroupResource identifies a resource.

_Appears in:_

- [PermissionClaim](#permissionclaim)
- [ResourceToSync](#resourcetosync)

| Field | Description |
| --- | --- |
| `group` _string_ | group is the name of an API group. For core groups this is the empty string '""'. |
| `resource` _string_ | resource is the name of the resource. Note: it is worth noting that you can not ask for permissions for resource provided by a CRD not provided by an api export. |

#### Identity

Identity defines the identity of an APIExport, i.e. determines the etcd prefix data of this APIExport are stored under.

_Appears in:_

- [APIExportSpec](#apiexportspec)

| Field | Description |
| --- | --- |
| `secretRef` _[SecretReference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#secretreference-v1-core)_ | secretRef is a reference to a secret that contains the API identity in the 'key' file. |

#### LocalAPIExportPolicy

LocalAPIExportPolicy will tell the APIBinding authorizer to check policy in the local namespace of the API Export

_Appears in:_

- [MaximalPermissionPolicy](#maximalpermissionpolicy)

#### MaximalPermissionPolicy

MaximalPermissionPolicy is a wrapper type around the multiple options that would be allowed.

_Appears in:_

- [APIExportSpec](#apiexportspec)

| Field | Description |
| --- | --- |
| `local` _[LocalAPIExportPolicy](#localapiexportpolicy)_ | local is policy that is defined in same namespace as API Export. |

#### PermissionClaim

PermissionClaim identifies an object by GR and identity hash. It's purpose is to determine the added permisions that a service provider may request and that a consumer may accept and alllow the service provider access to.

_Appears in:_

- [APIBindingStatus](#apibindingstatus)
- [APIExportSpec](#apiexportspec)
- [AcceptablePermissionClaim](#acceptablepermissionclaim)

| Field | Description |
| --- | --- |
| `GroupResource` _[GroupResource](#groupresource)_ |  |
| `identityHash` _string_ | This is the identity for a given APIExport that the APIResourceSchema belongs to. The hash can be found on APIExport and APIResourceSchema's status. It will be empty for core types. Note that one must look this up for a particular KCP instance. |

#### VirtualWorkspace

_Appears in:_

- [APIExportStatus](#apiexportstatus)

| Field | Description |
| --- | --- |
| `url` _string_ | url is an APIExport virtual workspace URL. |

#### WorkspaceExportReference

WorkspaceExportReference describes an API and backing implementation that are provided by an actor in the specified Workspace.

_Appears in:_

- [ExportReference](#exportreference)

| Field | Description |
| --- | --- |
| `path` _string_ | path is an absolute reference to a workspace, e.g. root:org:ws. The workspace must be some ancestor or a child of some ancestor. If it is unset, the path of the APIBinding is used. |
| `exportName` _string_ | Name of the APIExport that describes the API. |

## scheduling.kcp.dev/v1alpha1

#### AvailableSelectorLabel

AvailableSelectorLabel specifies a label with key name and possible values.

_Appears in:_

- [LocationSpec](#locationspec)

| Field | Description |
| --- | --- |
| `key` _[LabelKey](#labelkey)_ | key is the name of the label. |
| `values` _[LabelValue](#labelvalue) array_ | values are the possible values for this labels. |
| `description` _string_ | description is a human readable description of the label. |

#### GroupVersionResource

GroupVersionResource unambiguously identifies a resource.

_Appears in:_

- [LocationSpec](#locationspec)
- [PlacementSpec](#placementspec)

| Field | Description |
| --- | --- |
| `group` _string_ | group is the name of an API group. |
| `version` _string_ | version is the version of the API. |
| `resource` _string_ | resource is the name of the resource. |

#### LabelKey

_Underlying type:_ `string`

LabelKey is a key for a label.

_Appears in:_

- [AvailableSelectorLabel](#availableselectorlabel)

#### LabelValue

_Underlying type:_ `string`

LabelValue specifies a value of a label.

_Appears in:_

- [AvailableSelectorLabel](#availableselectorlabel)

#### Location

Location represents a set of instances of a scheduling resource type acting a target of scheduling.
 The location is chosen by the user (in the future) through a Placement object, while the instance is chosen by the scheduler depending on considerations like load or available resources, or further node selectors specified by the user.

_Appears in:_

- [LocationList](#locationlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[LocationSpec](#locationspec)_ |  |
| `status` _[LocationStatus](#locationstatus)_ |  |

#### LocationReference

LocationReference describes a loaction that are provided in the specified Workspace.

_Appears in:_

- [PlacementStatus](#placementstatus)

| Field | Description |
| --- | --- |
| `path` _string_ | path is an absolute reference to a workspace, e.g. root:org:ws. The workspace must be some ancestor or a child of some ancestor. |
| `locationName` _string_ | Name of the Location. |

#### LocationSpec

LocationSpec holds the desired state of the Location.

_Appears in:_

- [Location](#location)

| Field | Description |
| --- | --- |
| `resource` _[GroupVersionResource](#groupversionresource)_ | resource is the group-version-resource of the instances that are subject to this location. |
| `description` _string_ | description is a human-readable description of the location. |
| `availableSelectorLabels` _[AvailableSelectorLabel](#availableselectorlabel) array_ | availableSelectorLabels is a list of labels that can be used to select an instance at this location in a placement object. |
| `instanceSelector` _[LabelSelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#labelselector-v1-meta)_ | instanceSelector chooses the instances that will be part of this location.
 Note that these labels are not what is shown in the Location objects to the user. Depending on context, both will match or won't match. |

#### LocationStatus

LocationStatus defines the observed state of Location.

_Appears in:_

- [Location](#location)

| Field | Description |
| --- | --- |
| `instances` _integer_ | instances is the number of actual instances at this location. |
| `availableInstances` _integer_ | available is the number of actual instances that are available at this location. |

#### Placement

Placement defines a selection rule to choose ONE location for MULTIPLE namespaces in a workspace.
 placement is in Pending state initially. When a location is selected by the placement, the placement turns to Unbound state. In Pending or Unbound state, the selection rule can be updated to select another location. When the a namespace is annotated by another controller or user with the key of "scheduling.kcp.dev/placement", the namespace will pick one placement, and this placement is transfered to Bound state. Any update to spec of the placement is ignored in Bound state and reflected in the conditions. The placement will turn back to Unbound state when no namespace uses this placement any more.

_Appears in:_

- [PlacementList](#placementlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[PlacementSpec](#placementspec)_ |  |
| `status` _[PlacementStatus](#placementstatus)_ |  |

#### PlacementPhase

_Underlying type:_ `string`

_Appears in:_

- [PlacementStatus](#placementstatus)

#### PlacementSpec

_Appears in:_

- [Placement](#placement)

| Field | Description |
| --- | --- |
| `locationSelectors` _[LabelSelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#labelselector-v1-meta) array_ | loacationSelectors represents a slice of label selector to select a location, these label selectors are logically ORed. |
| `locationResource` _[GroupVersionResource](#groupversionresource)_ | locationResource is the group-version-resource of the instances that are subject to the locations to select. |
| `namespaceSelector` _[LabelSelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#labelselector-v1-meta)_ | namespaceSelector is a label selector to select ns. It match all ns by default, but can be specified to a certain set of ns. |
| `locationWorkspace` _string_ | locationWorkspace is an absolute reference to a workspace for the location. If it is not set, the workspace of APIBinding will be used. |

#### PlacementStatus

_Appears in:_

- [Placement](#placement)

| Field | Description |
| --- | --- |
| `phase` _[PlacementPhase](#placementphase)_ | phase is the current phase of the placement |
| `selectedLocation` _[LocationReference](#locationreference)_ | selectedLocation is the location that a picked by this placement. |
| `conditions` _[Condition](#condition) array_ | Current processing state of the Placement. |

## tenancy.kcp.dev/v1alpha1

#### ClusterWorkspace

ClusterWorkspace defines a Kubernetes-cluster-like endpoint that holds a default set of resources and exhibits standard Kubernetes API semantics of CRUD operations. It represents the full life-cycle of the persisted data in this workspace in a KCP installation.
 ClusterWorkspace is a concrete type that implements a workspace.

_Appears in:_

- [ClusterWorkspaceList](#clusterworkspacelist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[ClusterWorkspaceSpec](#clusterworkspacespec)_ |  |
| `status` _[ClusterWorkspaceStatus](#clusterworkspacestatus)_ |  |

#### ClusterWorkspaceInitializer

_Underlying type:_ `string`

ClusterWorkspaceInitializer is a unique string corresponding to a cluster workspace initialization controller for the given type of workspaces.

_Appears in:_

- [ClusterWorkspaceStatus](#clusterworkspacestatus)
- [WorkspaceStatus](#workspacestatus)

#### ClusterWorkspaceLocation

ClusterWorkspaceLocation specifies workspace placement information, including current, desired (target), and historical information.

_Appears in:_

- [ClusterWorkspaceStatus](#clusterworkspacestatus)

| Field | Description |
| --- | --- |
| `current` _string_ | Current workspace placement (shard). |
| `target` _string_ | Target workspace placement (shard). |

#### ClusterWorkspacePhaseType

_Underlying type:_ `string`

ClusterWorkspacePhaseType is the type of the current phase of the workspace

_Appears in:_

- [ClusterWorkspaceStatus](#clusterworkspacestatus)
- [WorkspaceStatus](#workspacestatus)

#### ClusterWorkspaceShard

ClusterWorkspaceShard describes a Shard (== KCP instance) on which a number of workspaces will live

_Appears in:_

- [ClusterWorkspaceShardList](#clusterworkspaceshardlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[ClusterWorkspaceShardSpec](#clusterworkspaceshardspec)_ |  |
| `status` _[ClusterWorkspaceShardStatus](#clusterworkspaceshardstatus)_ |  |

#### ClusterWorkspaceShardSpec

ClusterWorkspaceShardSpec holds the desired state of the ClusterWorkspaceShard.

_Appears in:_

- [ClusterWorkspaceShard](#clusterworkspaceshard)

| Field | Description |
| --- | --- |
| `baseURL` _string_ | baseURL is the address of the KCP shard for direct connections, e.g. by some front-proxy doing the fan-out to the shards.
 This will be defaulted to the shard's external address if not specified. Note that this is only sensible in single-shards setups. |
| `externalURL` _string_ | externalURL is the externally visible address presented to users in Workspace URLs. Changing this will break all existing workspaces on that shard, i.e. existing kubeconfigs of clients will be invalid. Hence, when changing this value, the old URL used by clients must keep working.
 The external address will not be unique if a front-proxy does a fan-out to shards, but all workspace client will talk to the front-proxy. In that case, put the address of the front-proxy here.
 Note that movement of shards is only possible (in the future) between shards that share a common external URL.
 This will be defaulted to the value of the baseURL. |
| `virtualWorkspaceURL` _string_ | virtualWorkspaceURL is the address of the virtual workspace server associated with this shard. It can be a direct address, an address of a front-proxy or even an address of an LB. As of today this address is assigned to APIExports.
 This will be defaulted to the shard's base address if not specified. |

#### ClusterWorkspaceShardStatus

ClusterWorkspaceShardStatus communicates the observed state of the ClusterWorkspaceShard.

_Appears in:_

- [ClusterWorkspaceShard](#clusterworkspaceshard)

| Field | Description |
| --- | --- |
| `capacity` _object (keys:[ResourceName](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#resourcename-v1-core), values:Quantity)_ | Set of integer resources that workspaces can be scheduled into |
| `conditions` _[Condition](#condition) array_ | Current processing state of the ClusterWorkspaceShard. |

#### ClusterWorkspaceSpec

ClusterWorkspaceSpec holds the desired state of the ClusterWorkspace.

_Appears in:_

- [ClusterWorkspace](#clusterworkspace)

| Field | Description |
| --- | --- |
| `readOnly` _boolean_ |  |
| `type` _[ClusterWorkspaceTypeReference](#clusterworkspacetypereference)_ | type defines properties of the workspace both on creation (e.g. initial resources and initially installed APIs) and during runtime (e.g. permissions). If no type is provided, the default type for the workspace in which this workspace is nesting will be used.
 The type is a reference to a ClusterWorkspaceType in the listed workspace, but lower-cased. The ClusterWorkspaceType existence is validated at admission during creation. The type is immutable after creation. The use of a type is gated via the RBAC clusterworkspacetypes/use resource permission. |
| `shard` _[ShardConstraints](#shardconstraints)_ | shard constraints onto which shards this cluster workspace can be scheduled to. if the constraint is not fulfilled by the current location stored in the status, movement will be attempted.
 Either shard name or shard selector must be specified.
 If the no shard constraints are specified, an aribtrary shard is chosen. |

#### ClusterWorkspaceStatus

ClusterWorkspaceStatus communicates the observed state of the ClusterWorkspace.

_Appears in:_

- [ClusterWorkspace](#clusterworkspace)

| Field | Description |
| --- | --- |
| `phase` _[ClusterWorkspacePhaseType](#clusterworkspacephasetype)_ | Phase of the workspace  (Scheduling / Initializing / Ready) |
| `conditions` _[Condition](#condition) array_ | Current processing state of the ClusterWorkspace. |
| `baseURL` _string_ | Base URL where this ClusterWorkspace can be targeted. This will generally be of the form: https://<workspace shard server>/cluster/<workspace name>. But a workspace could also be targetable by a unique hostname in the future. |
| `location` _[ClusterWorkspaceLocation](#clusterworkspacelocation)_ | Contains workspace placement information. |
| `initializers` _[ClusterWorkspaceInitializer](#clusterworkspaceinitializer) array_ | initializers are set on creation by the system and must be cleared by a controller before the workspace can be used. The workspace will stay in the phase "Initializing" state until all initializers are cleared.
 A cluster workspace in "Initializing" state are gated via the RBAC clusterworkspaces/initialize resource permission. |

#### ClusterWorkspaceType

ClusterWorkspaceType specifies behaviour of workspaces of this type.

_Appears in:_

- [ClusterWorkspaceTypeList](#clusterworkspacetypelist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[ClusterWorkspaceTypeSpec](#clusterworkspacetypespec)_ |  |
| `status` _[ClusterWorkspaceTypeStatus](#clusterworkspacetypestatus)_ |  |

#### ClusterWorkspaceTypeExtension

ClusterWorkspaceTypeExtension defines how other ClusterWorkspaceTypes are composed together to add functionality to the owning ClusterWorkspaceType.

_Appears in:_

- [ClusterWorkspaceTypeSpec](#clusterworkspacetypespec)

| Field | Description |
| --- | --- |
| `with` _[ClusterWorkspaceTypeReference](#clusterworkspacetypereference) array_ | with are ClusterWorkspaceTypes whose initializers are added to the list for the owning type, and for whom the owning type becomes an alias, as long as all of their required types are not mentioned in without. |

#### ClusterWorkspaceTypeName

_Underlying type:_ `string`

ClusterWorkspaceTypeName is a name of a ClusterWorkspaceType

_Appears in:_

- [ClusterWorkspaceTypeReference](#clusterworkspacetypereference)

#### ClusterWorkspaceTypeReference

ClusterWorkspaceTypeReference is a globally unique, fully qualified reference to a cluster workspace type.

_Appears in:_

- [ClusterWorkspaceSpec](#clusterworkspacespec)
- [ClusterWorkspaceTypeExtension](#clusterworkspacetypeextension)
- [ClusterWorkspaceTypeSelector](#clusterworkspacetypeselector)
- [ClusterWorkspaceTypeSpec](#clusterworkspacetypespec)
- [WorkspaceSpec](#workspacespec)

| Field | Description |
| --- | --- |
| `name` _[ClusterWorkspaceTypeName](#clusterworkspacetypename)_ | name is the name of the ClusterWorkspaceType |
| `path` _string_ | path is an absolute reference to the workspace that owns this type, e.g. root:org:ws. |

#### ClusterWorkspaceTypeSelector

ClusterWorkspaceTypeSelector describes a set of types.

_Appears in:_

- [ClusterWorkspaceTypeSpec](#clusterworkspacetypespec)

| Field | Description |
| --- | --- |
| `none` _boolean_ | none means that no type matches. |
| `types` _[ClusterWorkspaceTypeReference](#clusterworkspacetypereference) array_ | types is a list of ClusterWorkspaceTypes that match. A workspace type extending another workspace type automatically is considered as that extended type as well (even transitively).
 An empty list matches all types. |

#### ClusterWorkspaceTypeSpec

_Appears in:_

- [ClusterWorkspaceType](#clusterworkspacetype)

| Field | Description |
| --- | --- |
| `initializer` _boolean_ | initializer determines if this ClusterWorkspaceType has an associated initializing controller. These controllers are used to add functionality to a ClusterWorkspace; all controllers must finish their work before the ClusterWorkspace becomes ready for use.
 One initializing controller is supported per ClusterWorkspaceType; the identifier for this initializer will be a colon-delimited string using the workspace in which the ClusterWorkspaceType is defined, and the type's name. For example, if a ClusterWorkspaceType `example` is created in the `root:org` workspace, the implicit initializer name is `root:org:Example`. |
| `extend` _[ClusterWorkspaceTypeExtension](#clusterworkspacetypeextension)_ | extend is a list of other ClusterWorkspaceTypes whose initializers and limitAllowedChildren and limitAllowedParents this ClusterWorkspaceType is inheriting. By (transitively) extending another ClusterWorkspaceType, this ClusterWorkspaceType will be considered as that other type in evaluation of limitAllowedChildren and limitAllowedParents constraints.
 A dependency cycle stop this ClusterWorkspaceType from being admitted as the type of a ClusterWorkspace.
 A non-existing dependency stop this ClusterWorkspaceType from being admitted as the type of a ClusterWorkspace. |
| `additionalWorkspaceLabels` _object (keys:string, values:string)_ | additionalWorkspaceLabels are a set of labels that will be added to a ClusterWorkspace on creation. |
| `defaultChildWorkspaceType` _[ClusterWorkspaceTypeReference](#clusterworkspacetypereference)_ | defaultChildWorkspaceType is the ClusterWorkspaceType that will be used by default if another, nested ClusterWorkspace is created in a workspace of this type. When this field is unset, the user must specify a type when creating nested workspaces. Extending another ClusterWorkspaceType does not inherit its defaultChildWorkspaceType. |
| `limitAllowedChildren` _[ClusterWorkspaceTypeSelector](#clusterworkspacetypeselector)_ | limitAllowedChildren specifies constraints for sub-workspaces created in workspaces of this type. These are in addition to child constraints of types this one extends. |
| `limitAllowedParents` _[ClusterWorkspaceTypeSelector](#clusterworkspacetypeselector)_ | limitAllowedParents specifies constraints for the parent workspace that workspaces of this type are created in. These are in addition to parent constraints of types this one extends. |

#### ClusterWorkspaceTypeStatus

ClusterWorkspaceTypeStatus defines the observed state of ClusterWorkspaceType.

_Appears in:_

- [ClusterWorkspaceType](#clusterworkspacetype)

| Field | Description |
| --- | --- |
| `conditions` _[Condition](#condition) array_ | conditions is a list of conditions that apply to the APIExport. |
| `virtualWorkspaces` _[VirtualWorkspace](#virtualworkspace) array_ | virtualWorkspaces contains all APIExport virtual workspace URLs. |

#### ShardConstraints

_Appears in:_

- [ClusterWorkspaceSpec](#clusterworkspacespec)

| Field | Description |
| --- | --- |
| `name` _string_ | name is the name of ClusterWorkspaceShard. |
| `selector` _[LabelSelector](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#labelselector-v1-meta)_ | selector is a label selector that filters shard scheduling targets. |

#### VirtualWorkspace

_Appears in:_

- [ClusterWorkspaceTypeStatus](#clusterworkspacetypestatus)

| Field | Description |
| --- | --- |
| `url` _string_ | url is a ClusterWorkspaceType initialization virtual workspace URL. |

## tenancy.kcp.dev/v1beta1

#### Workspace

Workspace defines a generic Kubernetes-cluster-like endpoint, with standard Kubernetes discovery APIs, OpenAPI and resource API endpoints.
 A workspace can be backed by different concrete types of workspace implementation, depending on access pattern. All workspace implementations share the characteristic that the URL that serves a given workspace can be used with standard Kubernetes API machinery and client libraries and command line tools.

_Appears in:_

- [WorkspaceList](#workspacelist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[WorkspaceSpec](#workspacespec)_ |  |
| `status` _[WorkspaceStatus](#workspacestatus)_ |  |

#### WorkspaceSpec

WorkspaceSpec holds the desired state of the ClusterWorkspace.

_Appears in:_

- [Workspace](#workspace)

| Field | Description |
| --- | --- |
| `type` _[ClusterWorkspaceTypeReference](#clusterworkspacetypereference)_ | type defines properties of the workspace both on creation (e.g. initial resources and initially installed APIs) and during runtime (e.g. permissions). If no type is provided, the default type for the workspace in which this workspace is nesting will be used.
 The type is a reference to a ClusterWorkspaceType in the listed workspace, but lower-cased. The ClusterWorkspaceType existence is validated at admission during creation. The type is immutable after creation. The use of a type is gated via the RBAC clusterworkspacetypes/use resource permission. |

#### WorkspaceStatus

WorkspaceStatus communicates the observed state of the Workspace.

_Appears in:_

- [Workspace](#workspace)

| Field | Description |
| --- | --- |
| `URL` _string_ | url is the address under which the Kubernetes-cluster-like endpoint can be found. This URL can be used to access the workspace with standard Kubernetes client libraries and command line tools. |
| `phase` _[ClusterWorkspacePhaseType](#clusterworkspacephasetype)_ | Phase of the workspace (Initializing / Active / Terminating). This field is ALPHA. |
| `conditions` _[Condition](#condition) array_ | Current processing state of the ClusterWorkspace. |
| `initializers` _[ClusterWorkspaceInitializer](#clusterworkspaceinitializer) array_ | initializers are set on creation by the system and must be cleared by a controller before the workspace can be used. The workspace will stay in the phase "Initializing" state until all initializers are cleared.
 A cluster workspace in "Initializing" state are gated via the RBAC clusterworkspaces/initialize resource permission. |

## workload.kcp.dev/v1alpha1

#### ResourceCompatibleState

_Underlying type:_ `string`

_Appears in:_

- [ResourceToSync](#resourcetosync)

#### ResourceToSync

_Appears in:_

- [SyncTargetStatus](#synctargetstatus)

| Field | Description |
| --- | --- |
| `GroupResource` _[GroupResource](#groupresource)_ |  |
| `versions` _string array_ | versions are the resource versions the syncer can choose to sync depending on availability on the downstream cluster. Conversion to the storage version, if necessary, will be done on the kcp side. The versions are ordered by precedence and the first version compatible is preferred by syncer. |
| `identityHash` _string_ | identityHash is the identity for a given APIExport that the APIResourceSchema belongs to. The hash can be found on APIExport and APIResourceSchema's status. It will be empty for core types. |
| `state` _[ResourceCompatibleState](#resourcecompatiblestate)_ | state indicate whether the resources schema is compatible to the SyncTarget. It must be updated by syncer after checking the API compaibility on SyncTarget. |

#### SyncTarget

SyncTarget describes a member cluster capable of running workloads.

_Appears in:_

- [SyncTargetList](#synctargetlist)

| Field | Description |
| --- | --- |
| `TypeMeta` _[TypeMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#typemeta-v1-meta)_ |  |
| `metadata` _[ObjectMeta](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#objectmeta-v1-meta)_ | Refer to Kubernetes API documentation for fields of `metadata`. |
| `spec` _[SyncTargetSpec](#synctargetspec)_ | Spec holds the desired state. |
| `status` _[SyncTargetStatus](#synctargetstatus)_ | Status communicates the observed state. |

#### SyncTargetSpec

SyncTargetSpec holds the desired state of the SyncTarget (from the client).

_Appears in:_

- [SyncTarget](#synctarget)

| Field | Description |
| --- | --- |
| `unschedulable` _boolean_ | Unschedulable controls cluster schedulability of new workloads. By default, cluster is schedulable. |
| `evictAfter` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#time-v1-meta)_ | EvictAfter controls cluster schedulability of new and existing workloads. After the EvictAfter time, any workload scheduled to the cluster will be unassigned from the cluster. By default, workloads scheduled to the cluster are not evicted. |
| `supportedAPIExports` _[ExportReference](#exportreference) array_ | SupportedAPIExports defines a set of APIExports supposed to be supported by this SyncTarget. The SyncTarget will be selected to deploy the workload only when the resource schema on the SyncTarget is compatible with the resource schema included in the exports. If it is not set, the kubernetes export in the same workspace will be used by default. |
| `cells` _object (keys:string, values:string)_ | Cells is a set of labels to identify the cells the SyncTarget belongs to. SyncTargets with the same cells run as they are in the same physical cluster. Each key/value pair in the cells should be added and updated by service providers (i.e. a network provider updates one key/value, while the storage provider updates another.) |

#### SyncTargetStatus

SyncTargetStatus communicates the observed state of the SyncTarget (from the controller).

_Appears in:_

- [SyncTarget](#synctarget)

| Field | Description |
| --- | --- |
| `allocatable` _[ResourceList](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#resourcelist-v1-core)_ | Allocatable represents the resources that are available for scheduling. |
| `capacity` _[ResourceList](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#resourcelist-v1-core)_ | Capacity represents the total resources of the cluster. |
| `conditions` _[Condition](#condition) array_ | Current processing state of the SyncTarget. |
| `syncedResources` _[ResourceToSync](#resourcetosync) array_ | SyncedResources represents the resources that the syncer of the SyncTarget can sync. It MUST be updated by kcp server. |
| `lastSyncerHeartbeatTime` _[Time](https://kubernetes.io/docs/reference/generated/kubernetes-api/v/#time-v1-meta)_ | A timestamp indicating when the syncer last reported status. |
| `virtualWorkspaces` _[VirtualWorkspace](#virtualworkspace) array_ | VirtualWorkspaces contains all syncer virtual workspace URLs. |

#### VirtualWorkspace

_Appears in:_

- [SyncTargetStatus](#synctargetstatus)

| Field | Description |
| --- | --- |
| `url` _string_ | URL is the URL of the syncer virtual workspace. |
