# Gateway

## Parameters for `gateways`

| Parameter                                              | Type         | Required | Description                                                                           |
| ------------------------------------------------------ | ------------ | -------- | ------------------------------------------------------------------------------------- |
| `gateways`                                             | List of maps | Yes      | A list containing Gateway configurations. Each item in the list defines a Gateway.    |
| `name`                                                 | string       | Yes      | The name of the Gateway.                                                              |
| `disabled`                                             | boolean      | No       | If true, disables the Gateway.                                                        |
| `namespace`                                            | string       | Yes      | The namespace in which the Gateway should be created.                                 |
| `labels`                                               | map          | No       | Custom labels for the Gateway.                                                        |
| `annotations`                                          | map          | No       | Annotations for the Gateway metadata.                                                 |
| `gatewayClassName`                                     | string       | No       | The GatewayClass name. Defaults to `gatewayClassName` in `gateway_defaults`.          |
| `addresses`                                            | List of maps | No       | A list of addresses for the Gateway.                                                  |
| `addresses[].type`                                     | string       | No       | The address type. Defaults to `IPAddress`.                                            |
| `addresses[].value`                                    | string       | Yes      | The address value. Supports global value rendering.                                   |
| `listeners`                                            | List of maps | No       | A list of listeners for the Gateway.                                                  |
| `listeners[].name`                                     | string       | Yes      | The name of the listener.                                                             |
| `listeners[].protocol`                                 | string       | No       | The protocol for the listener. Defaults to `HTTP`.                                    |
| `listeners[].port`                                     | integer      | Yes      | The port for the listener.                                                            |
| `listeners[].hostname`                                 | string       | No       | The hostname for the listener. Supports global value rendering.                       |
| `listeners[].tls`                                      | map          | No       | TLS configuration for the listener.                                                   |
| `listeners[].tls.mode`                                 | string       | No       | The TLS mode. Defaults to `Terminate`.                                                |
| `listeners[].tls.certificateRefs`                      | List of maps | No       | A list of certificate references.                                                     |
| `listeners[].tls.certificateRefs[].kind`               | string       | No       | The kind of the certificate reference. Defaults to `Secret`.                          |
| `listeners[].tls.certificateRefs[].name`               | string       | Yes      | The name of the certificate reference.                                                |
| `listeners[].tls.certificateRefs[].namespace`          | string       | No       | The namespace of the certificate reference.                                           |
| `listeners[].tls.options`                              | map          | No       | Additional TLS options passed directly to the spec.                                   |
| `listeners[].allowedRoutes`                            | map          | No       | Route allowance configuration for the listener.                                       |
| `listeners[].allowedRoutes.namespaces.from`            | string       | No       | Namespace selection strategy. Defaults to `Same`.                                     |
| `listeners[].allowedRoutes.namespaces.selector`        | map          | No       | Label selector for namespace matching.                                                |
| `listeners[].allowedRoutes.kinds`                      | List of maps | No       | A list of allowed route kinds.                                                        |
| `listeners[].allowedRoutes.kinds[].kind`               | string       | Yes      | The kind of route allowed (e.g., `HTTPRoute`).                                        |
| `listeners[].allowedRoutes.kinds[].group`              | string       | No       | The API group of the route kind.                                                      |

## Example of a Simple Gateway

```yaml
gateways:
  - name: example-gateway
    namespace: my-namespace
    gatewayClassName: envoy
    listeners:
      - name: http
        protocol: HTTP
        port: 80
      - name: https
        protocol: HTTPS
        port: 443
        hostname: "*.example.com"
        tls:
          mode: Terminate
          certificateRefs:
            - name: example-tls
        allowedRoutes:
          namespaces:
            from: All
```
