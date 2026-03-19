# CiliumNetworkPolicy

## Parameters for `ciliumnetworkpolicies`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `ciliumnetworkpolicies` | Map of maps | Yes | A map containing CiliumNetworkPolicy configurations. Each entry defines one policy. |
| `name` | string | No | The policy name. Defaults to the map key when omitted. |
| `disabled` | boolean | No | If true, disables the policy. |
| `namespace` | string | No | The namespace in which the policy should be created. Defaults to the release namespace. |
| `labels` | map | No | Custom labels for the policy. |
| `annotations` | map | No | Custom annotations for the policy. |
| `spec` | map | No | Full raw `spec` to render. Use this when you need fields beyond the helper shortcuts. Supports template rendering. |
| `endpointSelector` | map | Conditionally | Endpoint selector for the policy. Required when `spec` is not provided. Supports template rendering. |
| `ingress` | list | No | Ingress rules. Supports template rendering. |
| `egress` | list | No | Egress rules. Supports template rendering. |

## Example

```yaml
ciliumnetworkpolicies:
  app-egress:
    namespace: my-namespace
    endpointSelector:
      matchLabels:
        app: my-app
    egress:
      - toFQDNs:
          - matchName: api.stripe.com
        toPorts:
          - ports:
              - port: "443"
                protocol: TCP
```
