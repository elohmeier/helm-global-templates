# SSORule

## Parameters for `ssorules`

| Parameter     | Type         | Required | Description                                                                                      |
| ------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `ssorules`    | List of maps | Yes      | A list containing SSORule configurations. Each item in the list defines an SSORule.               |
| `name`        | string       | Yes      | The name of the SSORule.                                                                         |
| `disabled`    | boolean      | No       | If true, disables the SSORule.                                                                   |
| `labels`      | map          | No       | Custom labels for the SSORule.                                                                   |
| `annotations` | map          | No       | Annotations for the SSORule metadata.                                                            |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple SSORule

```yaml
ssorules:
  - name: example-ssorule
    fqdn: app.example.com
    ssoPolicyRef: example-sso-policy
```
