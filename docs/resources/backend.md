# Backend

## Parameters for `backends`

| Parameter                       | Type         | Required | Description                                                                        |
| ------------------------------- | ------------ | -------- | ---------------------------------------------------------------------------------- |
| `backends`                      | List of maps | Yes      | A list containing Backend configurations. Each item in the list defines a Backend. |
| `name`                          | string       | Yes      | The name of the Backend.                                                           |
| `disabled`                      | boolean      | No       | If true, disables the Backend.                                                     |
| `namespace`                     | string       | Yes      | The namespace in which the Backend should be created.                              |
| `labels`                        | map          | No       | Custom labels for the Backend.                                                     |
| `annotations`                   | map          | No       | Annotations for the Backend metadata.                                              |
| `endpoints`                     | List of maps | No       | A list of backend endpoints. Each endpoint uses either `fqdn` or `ip`.             |
| `endpoints[].fqdn.hostname`    | string       | No       | The FQDN hostname for the endpoint.                                                |
| `endpoints[].fqdn.port`        | integer      | No       | The port for the FQDN endpoint.                                                    |
| `endpoints[].ip.address`       | string       | No       | The IP address for the endpoint.                                                   |
| `endpoints[].ip.port`          | integer      | No       | The port for the IP endpoint.                                                      |
| `tls`                           | map          | No       | TLS configuration for the Backend.                                                 |
| `tls.insecureSkipVerify`       | boolean      | No       | If true, skips TLS certificate verification.                                       |
| `tls.certificateRef.name`      | string       | No       | The name of the TLS certificate reference.                                         |
| `tls.certificateRef.namespace` | string       | No       | The namespace of the TLS certificate reference.                                    |

## Example of a Simple Backend

```yaml
backends:
  - name: example-backend
    namespace: my-namespace
    endpoints:
      - fqdn:
          hostname: api.example.com
          port: 443
    tls:
      insecureSkipVerify: false
      certificateRef:
        name: api-cert
```
