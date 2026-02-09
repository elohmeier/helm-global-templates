# KafkaRebalance

## Parameters for `kafkarebalances`

| Parameter         | Type         | Required | Description                                                                                            |
| ----------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------------ |
| `kafkarebalances` | List of maps | Yes      | A list containing KafkaRebalance configurations. Each item in the list defines a KafkaRebalance.       |
| `name`            | string       | Yes      | The name of the KafkaRebalance.                                                                        |
| `disabled`        | boolean      | No       | If true, disables the KafkaRebalance.                                                                  |
| `namespace`       | string       | Yes      | The namespace in which the KafkaRebalance should be created.                                           |
| `labels`          | map          | No       | Custom labels for the KafkaRebalance. The `strimzi.io/cluster` label is set automatically.             |
| `annotations`     | map          | No       | Annotations for the KafkaRebalance metadata.                                                           |
| `clusterRef`      | string       | Yes      | The name of the Kafka cluster. Used to set the `strimzi.io/cluster` label.                             |
| `...`             | any          | No       | All other fields are passed directly to the resource `spec` (if any are provided). See Strimzi documentation for available fields. |

## Example of a Simple KafkaRebalance

```yaml
kafkarebalances:
  - name: my-rebalance
    namespace: my-namespace
    clusterRef: my-kafka
    goals:
      - RackAwareGoal
      - ReplicaCapacityGoal
```
