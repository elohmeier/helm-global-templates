# KafkaTopic

## Parameters for `kafkatopics`

| Parameter     | Type         | Required | Description                                                                                          |
| ------------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------- |
| `kafkatopics` | List of maps | Yes      | A list containing KafkaTopic configurations. Each item in the list defines a KafkaTopic.             |
| `name`        | string       | Yes      | The name of the KafkaTopic resource.                                                                 |
| `disabled`    | boolean      | No       | If true, disables the KafkaTopic.                                                                    |
| `namespace`   | string       | Yes      | The namespace in which the KafkaTopic should be created.                                             |
| `labels`      | map          | No       | Custom labels for the KafkaTopic. The `strimzi.io/cluster` label is set automatically.               |
| `annotations` | map          | No       | Annotations for the KafkaTopic metadata.                                                             |
| `clusterRef`  | string       | Yes      | The name of the Kafka cluster. Used to set the `strimzi.io/cluster` label.                           |
| `topicName`   | string       | No       | The topic name in Kafka. If not provided, defaults to the resource `name`.                           |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields. |

## Example of a Simple KafkaTopic

```yaml
kafkatopics:
  - name: my-topic
    namespace: my-namespace
    clusterRef: my-kafka
    partitions: 3
    replicas: 3
    config:
      retention.ms: "604800000"
      segment.bytes: "1073741824"
```
