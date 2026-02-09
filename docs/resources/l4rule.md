# L4Rule

## Parameters for `l4rules`

| Parameter     | Type         | Required | Description                                                                                      |
| ------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `l4rules`     | List of maps | Yes      | A list containing L4Rule configurations. Each item in the list defines an L4Rule.                |
| `name`        | string       | Yes      | The name of the L4Rule.                                                                          |
| `disabled`    | boolean      | No       | If true, disables the L4Rule.                                                                    |
| `labels`      | map          | No       | Custom labels for the L4Rule.                                                                    |
| `annotations` | map          | No       | Annotations for the L4Rule metadata.                                                             |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple L4Rule

```yaml
l4rules:
  - name: example-l4rule
    backendProperties:
      - port: 80
        protocol: TCP
        loadBalancerIP: 10.0.0.1
    listeners:
      - port: 80
        protocol: TCP
```
