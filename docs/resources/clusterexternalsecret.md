# ClusterExternalSecret

## Parameters for `clusterexternalsecrets`

| Parameter                                          | Type            | Required | Description                                                                                                     |
| -------------------------------------------------- | --------------- | -------- | --------------------------------------------------------------------------------------------------------------- |
| `clusterexternalsecrets`                           | List of maps    | Yes      | A list containing ClusterExternalSecret configurations. Each item in the list defines a ClusterExternalSecret.  |
| `name`                                             | string          | Yes      | The name of the ClusterExternalSecret. Also used as `externalSecretName`.                                       |
| `disabled`                                         | boolean         | No       | If true, disables the ClusterExternalSecret.                                                                    |
| `namespaces`                                       | List of strings | Yes      | The namespaces in which the ExternalSecret should be created.                                                   |
| `refreshTime`                                      | string          | No       | How often to refresh the namespaces. Defaults to `refreshTime` in `clusterexternalsecret_defaults`.             |
| `externalSecretSpec.secretStoreRef.name`           | string          | Yes      | The name of the SecretStore reference.                                                                          |
| `externalSecretSpec.secretStoreRef.kind`           | string          | No       | The kind of the SecretStore reference. Defaults to `secretStoreRef.kind` in `externalsecret_defaults`.          |
| `externalSecretSpec.refreshInterval`               | string          | No       | How often to refresh the secret. Defaults to `refreshInterval` in `externalsecret_defaults`.                    |
| `externalSecretSpec.target.name`                   | string          | Yes      | The name of the target Kubernetes Secret.                                                                       |
| `externalSecretSpec.target.creationPolicy`         | string          | No       | The creation policy for the target Secret. Defaults to `target.creationPolicy` in `externalsecret_defaults`.    |
| `externalSecretSpec.data`                          | List of maps    | Yes      | A list of secret key mappings.                                                                                  |
| `externalSecretSpec.data[].secretKey`              | string          | Yes      | The key in the Kubernetes Secret.                                                                               |
| `externalSecretSpec.data[].remoteRef.key`          | string          | Yes      | The key in the remote secret store.                                                                             |
| `externalSecretSpec.data[].remoteRef.version`      | string          | No       | The version of the remote secret.                                                                               |
| `externalSecretSpec.data[].remoteRef.property`     | string          | No       | The property within the remote secret.                                                                          |
| `externalSecretSpec.data[].remoteRef.decodingStrategy` | string      | No       | Decoding strategy. Must be one of `Base64`, `Base64URL`, `Auto`, `None`.                                        |
| `externalSecretSpec.data[].remoteRef.conversionStrategy` | string    | No       | Conversion strategy. Defaults to `remoteRef.conversionStrategy` in `clusterexternalsecret_defaults`.            |
| `externalSecretSpec.data[].remoteRef.metadataPolicy` | string       | No       | Metadata policy. Defaults to `remoteRef.metadataPolicy` in `clusterexternalsecret_defaults`.                    |
| `externalSecretSpec.dataFrom`                      | List of maps    | No       | A list of bulk data fetch configurations.                                                                       |
| `externalSecretSpec.dataFrom[].key`                | string          | Yes      | The key to fetch from the remote store.                                                                         |
| `externalSecretSpec.dataFrom[].version`            | string          | No       | The version of the remote data.                                                                                 |
| `externalSecretSpec.dataFrom[].property`           | string          | No       | The property within the remote data.                                                                            |

## Example of a Simple ClusterExternalSecret

```yaml
clusterexternalsecrets:
  - name: shared-credentials
    namespaces:
      - namespace-a
      - namespace-b
    refreshTime: "1m"
    externalSecretSpec:
      secretStoreRef:
        name: vault-backend
      refreshInterval: "1h"
      target:
        name: shared-credentials
        creationPolicy: Owner
      data:
        - secretKey: password
          remoteRef:
            key: secret/data/credentials
            property: password
```
