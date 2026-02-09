# KafkaUser

## Parameters for `kafkausers`

| Parameter     | Type         | Required | Description                                                                                          |
| ------------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------- |
| `kafkausers`  | List of maps | Yes      | A list containing KafkaUser configurations. Each item in the list defines a KafkaUser.               |
| `name`        | string       | Yes      | The name of the KafkaUser.                                                                           |
| `disabled`    | boolean      | No       | If true, disables the KafkaUser.                                                                     |
| `namespace`   | string       | Yes      | The namespace in which the KafkaUser should be created.                                              |
| `labels`      | map          | No       | Custom labels for the KafkaUser. The `strimzi.io/cluster` label is set automatically.                |
| `annotations` | map          | No       | Annotations for the KafkaUser metadata.                                                              |
| `clusterRef`  | string       | Yes      | The name of the Kafka cluster. Used to set the `strimzi.io/cluster` label.                           |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields. |

## Example of a Simple KafkaUser

```yaml
kafkausers:
  - name: my-user
    namespace: my-namespace
    clusterRef: my-kafka
    authentication:
      type: tls
    authorization:
      type: simple
      acls:
        - resource:
            type: topic
            name: my-topic
            patternType: literal
          operations:
            - Read
            - Describe
```
