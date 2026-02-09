# KafkaMirrorMaker2

## Parameters for `kafkamirrormaker2s`

| Parameter            | Type         | Required | Description                                                                                                |
| -------------------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------------- |
| `kafkamirrormaker2s` | List of maps | Yes      | A list containing KafkaMirrorMaker2 configurations. Each item in the list defines a KafkaMirrorMaker2.     |
| `name`               | string       | Yes      | The name of the KafkaMirrorMaker2.                                                                         |
| `disabled`           | boolean      | No       | If true, disables the KafkaMirrorMaker2.                                                                   |
| `namespace`          | string       | Yes      | The namespace in which the KafkaMirrorMaker2 should be created.                                            |
| `labels`             | map          | No       | Custom labels for the KafkaMirrorMaker2.                                                                   |
| `annotations`        | map          | No       | Annotations for the KafkaMirrorMaker2 metadata.                                                            |
| `...`                | any          | No       | All other fields are passed directly to the resource `spec`. See Strimzi documentation for available fields.|

## Example of a Simple KafkaMirrorMaker2

```yaml
kafkamirrormaker2s:
  - name: my-mirror-maker
    namespace: my-namespace
    connectCluster: target-cluster
    clusters:
      - alias: source-cluster
        bootstrapServers: source-kafka:9092
      - alias: target-cluster
        bootstrapServers: target-kafka:9092
    mirrors:
      - sourceCluster: source-cluster
        targetCluster: target-cluster
        sourceConnector: {}
```
