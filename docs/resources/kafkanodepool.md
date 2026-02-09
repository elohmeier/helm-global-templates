# KafkaNodePool

## Parameters for `kafkanodepools`

| Parameter     | Type         | Required | Description                                                                                              |
| ------------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------- |
| `kafkanodepools` | List of maps | Yes   | A list containing KafkaNodePool configurations. Each item in the list defines a KafkaNodePool.           |
| `name`        | string       | Yes      | The name of the KafkaNodePool. Supports global value rendering.                                          |
| `disabled`    | boolean      | No       | If true, disables the KafkaNodePool.                                                                     |
| `namespace`   | string       | Yes      | The namespace in which the KafkaNodePool should be created.                                              |
| `labels`      | map          | No       | Custom labels for the KafkaNodePool. The `strimzi.io/cluster` label is set automatically.                |
| `annotations` | map          | No       | Annotations for the KafkaNodePool metadata.                                                              |
| `clusterRef`  | string       | Yes      | The name of the Kafka cluster. Used to set the `strimzi.io/cluster` label.                               |
| `roles`       | List of strings | Yes   | The roles for the node pool (e.g., `broker`, `controller`).                                              |
| `storage`     | map          | Yes      | Storage configuration for the node pool.                                                                 |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields. |

## Example of a Simple KafkaNodePool

```yaml
kafkanodepools:
  - name: broker-pool
    namespace: my-namespace
    clusterRef: my-kafka
    roles:
      - broker
    replicas: 3
    storage:
      type: jbod
      volumes:
        - id: 0
          type: persistent-claim
          size: 100Gi
```
