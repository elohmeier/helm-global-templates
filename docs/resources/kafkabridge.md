# KafkaBridge

## Parameters for `kafkabridges`

| Parameter      | Type         | Required | Description                                                                                          |
| -------------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------- |
| `kafkabridges` | List of maps | Yes      | A list containing KafkaBridge configurations. Each item in the list defines a KafkaBridge.           |
| `name`         | string       | Yes      | The name of the KafkaBridge.                                                                         |
| `disabled`     | boolean      | No       | If true, disables the KafkaBridge.                                                                   |
| `namespace`    | string       | Yes      | The namespace in which the KafkaBridge should be created.                                            |
| `labels`       | map          | No       | Custom labels for the KafkaBridge.                                                                   |
| `annotations`  | map          | No       | Annotations for the KafkaBridge metadata.                                                            |
| `...`          | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields. |

## Example of a Simple KafkaBridge

```yaml
kafkabridges:
  - name: my-bridge
    namespace: my-namespace
    replicas: 1
    bootstrapServers: my-kafka-kafka-bootstrap:9092
    http:
      port: 8080
```
