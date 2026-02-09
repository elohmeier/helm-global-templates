# NetworkPolicy

## Parameters for `networkpolicies`

| Parameter         | Type         | Required | Description                                                                                              |
| ----------------- | ------------ | -------- | -------------------------------------------------------------------------------------------------------- |
| `networkpolicies` | List of maps | Yes      | A list containing NetworkPolicy configurations. Each item in the list defines a NetworkPolicy.           |
| `name`            | string       | Yes      | The name of the NetworkPolicy.                                                                           |
| `disabled`        | boolean      | No       | If true, disables the NetworkPolicy.                                                                     |
| `namespace`       | string       | No       | The namespace in which the NetworkPolicy should be created. Defaults to the release namespace.           |
| `labels`          | map          | No       | Custom labels for the NetworkPolicy.                                                                     |
| `annotations`     | map          | No       | Annotations for the NetworkPolicy metadata.                                                              |
| `spec`            | map          | Yes      | The full NetworkPolicy spec. Passed directly and supports template rendering.                            |

## Example of a Simple NetworkPolicy

```yaml
networkpolicies:
  - name: allow-web-traffic
    namespace: my-namespace
    spec:
      podSelector:
        matchLabels:
          app: web
      policyTypes:
        - Ingress
      ingress:
        - from:
            - namespaceSelector:
                matchLabels:
                  purpose: web
          ports:
            - protocol: TCP
              port: 80
```
