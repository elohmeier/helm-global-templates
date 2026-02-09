# KafkaConnect

## Parameters for `kafkaconnects`

| Parameter               | Type         | Required | Description                                                                                                    |
| ----------------------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------------- |
| `kafkaconnects`         | List of maps | Yes      | A list containing KafkaConnect configurations. Each item in the list defines a KafkaConnect.                   |
| `name`                  | string       | Yes      | The name of the KafkaConnect.                                                                                  |
| `disabled`              | boolean      | No       | If true, disables the KafkaConnect.                                                                            |
| `namespace`             | string       | Yes      | The namespace in which the KafkaConnect should be created.                                                     |
| `labels`                | map          | No       | Custom labels for the KafkaConnect.                                                                            |
| `annotations`           | map          | No       | Annotations for the KafkaConnect metadata.                                                                     |
| `useConnectorResources` | boolean      | No       | If true, adds `strimzi.io/use-connector-resources: true` annotation to enable KafkaConnector resource support. |
| `...`                   | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields.   |

## Example of a Simple KafkaConnect

```yaml
kafkaconnects:
  - name: my-connect
    namespace: my-namespace
    useConnectorResources: true
    replicas: 1
    bootstrapServers: my-kafka-kafka-bootstrap:9092
    config:
      group.id: connect-cluster
      offset.storage.topic: connect-offsets
      config.storage.topic: connect-configs
      status.storage.topic: connect-status
```
