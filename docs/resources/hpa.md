# HorizontalPodAutoscaler

## Parameters for `hpas`

| Parameter                              | Type         | Required | Description                                                                                                     |
| -------------------------------------- | ------------ | -------- | --------------------------------------------------------------------------------------------------------------- |
| `hpas`                                 | List of maps | Yes      | A list containing HPA configurations. Each item in the list defines an HPA.                                     |
| `name`                                 | string       | No       | The name of the HPA.                                                                                            |
| `disabled`                             | boolean      | No       | If true, disables the HPA.                                                                                      |
| `namespace`                            | string       | Yes      | The namespace in which the HPA should be created.                                                               |
| `labels`                               | map          | No       | Custom labels for the HPA.                                                                                      |
| `annotations`                          | map          | No       | Annotations for the HPA metadata.                                                                               |
| `reloaderEnabled`                      | boolean      | No       | If true, enables reloader annotations.                                                                          |
| `minReplicas`                          | integer      | No       | Minimum number of replicas. Defaults to `minReplicas` in `hpa_defaults`.                                        |
| `maxReplicas`                          | integer      | No       | Maximum number of replicas. Defaults to `maxReplicas` in `hpa_defaults`.                                        |
| `targetApiVersion`                     | string       | No       | API version of the scale target. Defaults to `targetApiVersion` in `hpa_defaults`.                              |
| `targetKind`                           | string       | No       | Kind of the scale target. Defaults to `targetKind` in `hpa_defaults`.                                           |
| `targetName`                           | string       | Yes      | Name of the scale target.                                                                                       |
| `targetCPUUtilizationPercentage`       | integer      | No       | Target CPU utilization percentage. Defaults to `targetCPUUtilizationPercentage` in `hpa_defaults`.              |
| `targetMemoryUtilizationPercentage`    | integer      | No       | Target memory utilization percentage.                                                                           |
| `extraMetrics`                         | List of maps | No       | Additional custom metrics passed directly to the `metrics` field.                                               |

## Example of a Simple HPA

```yaml
hpas:
  - name: api-hpa
    namespace: my-namespace
    minReplicas: 2
    maxReplicas: 10
    targetName: api-deployment
    targetCPUUtilizationPercentage: 70
    targetMemoryUtilizationPercentage: 80
```
