# ScaledObject (KEDA)

## Parameters for `scaledobjects`

| Parameter                             | Type         | Required | Description                                                                                           |
| ------------------------------------- | ------------ | -------- | ----------------------------------------------------------------------------------------------------- |
| `scaledobjects`                       | List of maps | Yes      | A list containing ScaledObject configurations. Each item in the list defines a ScaledObject.          |
| `name`                                | string       | No       | The name of the ScaledObject.                                                                         |
| `disabled`                            | boolean      | No       | If true, disables the ScaledObject.                                                                   |
| `namespace`                           | string       | Yes      | The namespace in which the ScaledObject should be created.                                            |
| `labels`                              | map          | No       | Custom labels for the ScaledObject.                                                                   |
| `annotations`                         | map          | No       | Annotations for the ScaledObject metadata.                                                            |
| `reloaderEnabled`                     | boolean      | No       | If true, enables reloader annotations.                                                                |
| `minReplicas`                         | integer      | No       | Minimum number of replicas. Defaults to `minReplicas` in `scaledobjects_defaults`.                    |
| `maxReplicas`                         | integer      | No       | Maximum number of replicas. Defaults to `maxReplicas` in `scaledobjects_defaults`.                    |
| `pollingInterval`                     | integer      | No       | Polling interval in seconds. Defaults to `pollingInterval` in `scaledobjects_defaults`.               |
| `targetApiVersion`                    | string       | No       | API version of the scale target. Defaults to `targetApiVersion` in `scaledobjects_defaults`.          |
| `targetKind`                          | string       | No       | Kind of the scale target. Defaults to `targetKind` in `scaledobjects_defaults`.                       |
| `targetName`                          | string       | Yes      | Name of the scale target.                                                                             |
| `triggers`                            | List of maps | No       | A list of KEDA triggers.                                                                              |
| `triggers[].type`                     | string       | Yes      | The trigger type (e.g., `kafka`, `prometheus`, `cron`).                                               |
| `triggers[].metadata`                 | map          | Yes      | Metadata for the trigger. Values support global value rendering.                                      |
| `triggers[].authenticationRef.name`   | string       | No       | Name of the TriggerAuthentication resource for this trigger.                                          |

## Example of a Simple ScaledObject

```yaml
scaledobjects:
  - name: api-scaler
    namespace: my-namespace
    targetName: api-deployment
    minReplicas: 1
    maxReplicas: 20
    pollingInterval: 15
    triggers:
      - type: prometheus
        metadata:
          serverAddress: http://prometheus:9090
          metricName: http_requests_total
          threshold: "100"
          query: sum(rate(http_requests_total[2m]))
```
