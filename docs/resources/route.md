# Route (OpenShift)

## Parameters for `routes`

| Parameter                            | Type         | Required | Description                                                                        |
| ------------------------------------ | ------------ | -------- | ---------------------------------------------------------------------------------- |
| `routes`                             | Map of maps  | Yes      | A map containing Route configurations. The map key is used as the default name.    |
| `name`                               | string       | No       | The name of the Route. Defaults to the map key.                                    |
| `disabled`                           | boolean      | No       | If true, disables the Route.                                                       |
| `namespace`                          | string       | Yes      | The namespace in which the Route should be created.                                |
| `labels`                             | map          | No       | Custom labels for the Route.                                                       |
| `annotations`                        | map          | No       | Annotations for the Route metadata.                                                |
| `host`                               | string       | No       | The hostname for the Route. Supports global value rendering.                       |
| `subdomain`                          | string       | No       | The subdomain for the Route. Supports global value rendering.                      |
| `path`                               | string       | No       | The path for the Route.                                                            |
| `port.targetPort`                    | string/int   | No       | The target port on the backend service.                                            |
| `to.kind`                            | string       | No       | The kind of the target. Defaults to `Service`.                                     |
| `to.name`                            | string       | Yes      | The name of the target service.                                                    |
| `to.weight`                          | integer      | No       | The weight for traffic distribution to the primary backend.                        |
| `wildcardPolicy`                     | string       | No       | The wildcard policy (e.g., `None`, `Subdomain`).                                   |
| `alternateBackends`                  | List of maps | No       | A list of alternate backend services.                                              |
| `alternateBackends[].kind`           | string       | No       | The kind of the alternate backend. Defaults to `Service`.                          |
| `alternateBackends[].name`           | string       | Yes      | The name of the alternate backend.                                                 |
| `alternateBackends[].weight`         | integer      | No       | The weight for the alternate backend.                                              |
| `tls`                                | map          | No       | TLS configuration for the Route.                                                   |
| `tls.termination`                    | string       | Yes      | TLS termination type (`edge`, `reencrypt`, `passthrough`). Required when tls is set.|
| `tls.insecureEdgeTerminationPolicy`  | string       | No       | Policy for insecure traffic (e.g., `Redirect`, `Allow`, `None`).                   |
| `tls.certificate`                    | string       | No       | PEM-encoded certificate.                                                           |
| `tls.key`                            | string       | No       | PEM-encoded private key.                                                           |
| `tls.caCertificate`                  | string       | No       | PEM-encoded CA certificate.                                                        |
| `tls.destinationCACertificate`       | string       | No       | PEM-encoded CA certificate for the backend (re-encrypt).                           |
| `tls.externalCertificate.name`       | string       | No       | The name of an external certificate Secret.                                        |
| `httpHeaders`                        | map          | No       | HTTP header configuration passed directly to the spec.                             |

## Example of a Simple Route

```yaml
routes:
  example-route:
    namespace: my-namespace
    host: app.example.com
    to:
      name: my-service
    port:
      targetPort: 8080
    tls:
      termination: edge
      insecureEdgeTerminationPolicy: Redirect
```
