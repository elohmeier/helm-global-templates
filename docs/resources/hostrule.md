# HostRule

## Parameters for `hostrules`

| Parameter     | Type         | Required | Description                                                                                      |
| ------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `hostrules`   | List of maps | Yes      | A list containing HostRule configurations. Each item in the list defines a HostRule.              |
| `name`        | string       | Yes      | The name of the HostRule.                                                                        |
| `disabled`    | boolean      | No       | If true, disables the HostRule.                                                                  |
| `namespace`   | string       | Yes      | The namespace in which the HostRule should be created.                                           |
| `labels`      | map          | No       | Custom labels for the HostRule.                                                                  |
| `annotations` | map          | No       | Annotations for the HostRule metadata.                                                           |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple HostRule

```yaml
hostrules:
  - name: example-hostrule
    namespace: my-namespace
    virtualhost:
      fqdn: app.example.com
      tls:
        sslKeyCertificate:
          name: example-cert
          type: secret
```
