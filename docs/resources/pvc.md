# PersistentVolumeClaim

Use the `global-templates.pvc` template to manage one or more Kubernetes PersistentVolumeClaims from `pvcs` values.

## Parameters for `pvcs`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `pvcs` | map or list | Yes | PersistentVolumeClaims to render. A map key is used as the claim name when `name` is omitted. |
| `name` | string | Yes* | Claim name. May be omitted when the claim is an entry in a map. |
| `namespace` | string | No | Claim namespace. Defaults to the Helm release namespace and supports `global.nsPrefix`. |
| `disabled` | boolean | No | Prevents the claim from being rendered when `true`. |
| `labels` | map | No | Metadata labels merged with `common_defaults.labels`. |
| `annotations` | map | No | Metadata annotations merged with `common_defaults.annotations`. |
| `accessModes` | list of strings | Yes | Requested access modes, such as `ReadWriteOnce` or `ReadWriteMany`. |
| `resources` | map | Yes | Kubernetes resource requirements. Usually contains `requests.storage`. |
| `storageClassName` | string | No | Storage class. Set it to an empty string to disable dynamic provisioning. |
| `volumeMode` | string | No | Volume mode: `Filesystem` or `Block`. |
| `selector` | map | No | Label selector used to bind to a matching PersistentVolume. |
| `volumeName` | string | No | Name of a specific PersistentVolume to bind. |
| `dataSource` | map | No | Source used to populate the claim. |
| `dataSourceRef` | map | No | Typed object reference used to populate the claim. |
| `volumeAttributesClassName` | string | No | VolumeAttributesClass requested by the claim. |
| `spec` | map | No | Raw PVC spec. When present, it replaces the flattened spec fields above. |

`pvc_defaults` can supply defaults for any spec field. Values on an individual claim take precedence, including empty values such as `storageClassName: ""`.

## Example

```yaml
pvcs:
  application-data:
    namespace: application
    accessModes:
      - ReadWriteOnce
    storageClassName: fast
    volumeMode: Filesystem
    resources:
      requests:
        storage: 20Gi
    annotations:
      helm.sh/resource-policy: keep
```

Include the template in your chart:

```yaml
{{ include "global-templates.pvc" (dict "pvcs" .Values.pvcs "Chart" .Chart "Release" .Release "Capabilities" .Capabilities "Files" .Files "Template" .Template "Values" .Values) }}
```
