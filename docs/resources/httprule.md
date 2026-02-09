# HTTPRule

## Parameters for `httprules`

| Parameter     | Type         | Required | Description                                                                                      |
| ------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `httprules`   | List of maps | Yes      | A list containing HTTPRule configurations. Each item in the list defines an HTTPRule.             |
| `name`        | string       | Yes      | The name of the HTTPRule.                                                                        |
| `disabled`    | boolean      | No       | If true, disables the HTTPRule.                                                                  |
| `namespace`   | string       | Yes      | The namespace in which the HTTPRule should be created.                                           |
| `labels`      | map          | No       | Custom labels for the HTTPRule.                                                                  |
| `annotations` | map          | No       | Annotations for the HTTPRule metadata.                                                           |
| `...`         | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple HTTPRule

```yaml
httprules:
  - name: example-httprule
    namespace: my-namespace
    fqdn: app.example.com
    paths:
      - target: /api
        healthMonitors:
          - example-health-monitor
        loadBalancerPolicy:
          algorithm: LB_ALGORITHM_ROUND_ROBIN
```
