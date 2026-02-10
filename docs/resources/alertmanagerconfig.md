# AlertmanagerConfig

## Parameters for `alertmanagerconfigs`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `alertmanagerconfigs` | Map of maps | Yes | A map containing AlertmanagerConfig configurations. Each key defines an AlertmanagerConfig. |
| `name` | string | Yes | The name of the AlertmanagerConfig. |
| `disabled` | boolean | No | If true, disables the AlertmanagerConfig. |
| `namespace` | string | Yes | The namespace in which the AlertmanagerConfig should be created. |
| `labels` | map | No | Custom labels for the AlertmanagerConfig. |
| `annotations` | map | No | Annotations for the AlertmanagerConfig metadata. |
| `route` | map | No | Routing tree configuration. Passed through as-is. |
| `receivers` | list of maps | No | List of receiver configurations. Passed through as-is. |
| `inhibitRules` | list of maps | No | List of inhibit rule configurations. Passed through as-is. |
| `timeIntervals` | list of maps | No | List of time interval configurations. Passed through as-is. |

## Example

```yaml
alertmanagerconfigs:
  my-alerts:
    name: my-alertmanager-config
    namespace: my-namespace
    route:
      receiver: default
      groupBy:
        - alertname
        - namespace
      routes:
        - receiver: critical
          matchers:
            - name: severity
              value: critical
    receivers:
      - name: default
        webhookConfigs:
          - url: http://webhook.example.com/alerts
      - name: critical
        webhookConfigs:
          - url: http://webhook.example.com/critical-alerts
    inhibitRules:
      - sourceMatch:
          - name: severity
            value: critical
        targetMatch:
          - name: severity
            value: warning
        equal:
          - alertname
          - namespace
```
