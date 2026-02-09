# KafkaConnector

## Parameters for `kafkaconnectors`

| Parameter         | Type         | Required | Description                                                                                            |
| ----------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------------ |
| `kafkaconnectors` | List of maps | Yes      | A list containing KafkaConnector configurations. Each item in the list defines a KafkaConnector.       |
| `name`            | string       | Yes      | The name of the KafkaConnector.                                                                        |
| `disabled`        | boolean      | No       | If true, disables the KafkaConnector.                                                                  |
| `namespace`       | string       | Yes      | The namespace in which the KafkaConnector should be created.                                           |
| `labels`          | map          | No       | Custom labels for the KafkaConnector. The `strimzi.io/cluster` label is set automatically.             |
| `annotations`     | map          | No       | Annotations for the KafkaConnector metadata.                                                           |
| `clusterRef`      | string       | Yes      | The name of the KafkaConnect cluster. Used to set the `strimzi.io/cluster` label.                      |
| `...`             | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields. |

## Example of a Simple KafkaConnector

```yaml
kafkaconnectors:
  - name: my-connector
    namespace: my-namespace
    clusterRef: my-connect
    class: org.apache.kafka.connect.file.FileStreamSourceConnector
    tasksMax: 1
    config:
      file: /opt/kafka/LICENSE
      topic: my-topic
```
