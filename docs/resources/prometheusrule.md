# PrometheusRule

## Parameters for `prometheusrules`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `prometheusrules` | Map of maps | Yes | A map containing PrometheusRule configurations. Each key defines a PrometheusRule. |
| `name` | string | Yes | The name of the PrometheusRule. |
| `disabled` | boolean | No | If true, disables the PrometheusRule. |
| `namespace` | string | Yes | The namespace in which the PrometheusRule should be created. |
| `labels` | map | No | Custom labels for the PrometheusRule. |
| `annotations` | map | No | Annotations for the PrometheusRule metadata. |
| `groups` | list of maps | Yes | Rule groups containing alerting and/or recording rules. Passed through as-is. |

### Rule Group Structure

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `groups[].name` | string | Yes | Name of the rule group. |
| `groups[].interval` | string | No | Evaluation interval for the group. |
| `groups[].rules` | list of maps | Yes | List of alerting or recording rules. |
| `groups[].rules[].alert` | string | No | Name of the alerting rule. |
| `groups[].rules[].record` | string | No | Name of the recording rule. |
| `groups[].rules[].expr` | string | Yes | PromQL expression. |
| `groups[].rules[].for` | string | No | Duration before an alert fires (alerting rules only). |
| `groups[].rules[].labels` | map | No | Labels to attach to the rule. |
| `groups[].rules[].annotations` | map | No | Annotations to attach to the rule (alerting rules only). |

## Example

```yaml
prometheusrules:
  my-rules:
    name: my-prometheus-rules
    namespace: my-namespace
    groups:
      - name: my-alerts
        rules:
          - alert: HighErrorRate
            expr: rate(http_requests_total{status="500"}[5m]) > 0.1
            for: 10m
            labels:
              severity: critical
            annotations:
              summary: "High error rate detected"
      - name: my-recordings
        rules:
          - record: job:http_requests_total:rate5m
            expr: rate(http_requests_total[5m])
```
