# Kafka

## Parameters for `kafkas`

| Parameter          | Type         | Required | Description                                                                                                                      |
| ------------------ | ------------ | -------- | -------------------------------------------------------------------------------------------------------------------------------- |
| `kafkas`           | List of maps | Yes      | A list containing Kafka configurations. Each item in the list defines a Kafka cluster.                                           |
| `name`             | string       | Yes      | The name of the Kafka cluster.                                                                                                   |
| `disabled`         | boolean      | No       | If true, disables the Kafka cluster.                                                                                             |
| `namespace`        | string       | Yes      | The namespace in which the Kafka cluster should be created.                                                                      |
| `labels`           | map          | No       | Custom labels for the Kafka cluster.                                                                                             |
| `annotations`      | map          | No       | Annotations for the Kafka cluster metadata.                                                                                      |
| `nodePoolsEnabled` | boolean      | No       | If true (default), adds `strimzi.io/node-pools: enabled` and `strimzi.io/kraft: enabled` annotations.                           |
| `...`              | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields.                     |

## Example of a Simple Kafka Cluster

```yaml
kafkas:
  - name: my-kafka
    namespace: my-namespace
    nodePoolsEnabled: true
    kafka:
      version: 3.7.0
      listeners:
        - name: plain
          port: 9092
          type: internal
          tls: false
    entityOperator:
      topicOperator: {}
      userOperator: {}
```
