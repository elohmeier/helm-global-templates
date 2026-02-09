# L7Rule

## Parameters for `l7rules`

| Parameter     | Type         | Required | Description                                                                                      |
| ------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `l7rules`     | List of maps | Yes      | A list containing L7Rule configurations. Each item in the list defines an L7Rule.                |
| `name`        | string       | Yes      | The name of the L7Rule.                                                                          |
| `disabled`    | boolean      | No       | If true, disables the L7Rule.                                                                    |
| `labels`      | map          | No       | Custom labels for the L7Rule.                                                                    |
| `annotations` | map          | No       | Annotations for the L7Rule metadata.                                                             |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple L7Rule

```yaml
l7rules:
  - name: example-l7rule
    allowInvalidClientCert: false
    closeConnectionOnVsMatchFail: false
    hostNameXlate: ""
```
