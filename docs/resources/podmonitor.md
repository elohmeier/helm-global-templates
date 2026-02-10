# PodMonitor

## Parameters for `podmonitors`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `podmonitors` | Map of maps | Yes | A map containing PodMonitor configurations. Each key defines a PodMonitor. |
| `name` | string | Yes | The name of the PodMonitor. |
| `disabled` | boolean | No | If true, disables the PodMonitor. |
| `namespace` | string | Yes | The namespace in which the PodMonitor should be created. |
| `labels` | map | No | Custom labels for the PodMonitor. |
| `annotations` | map | No | Annotations for the PodMonitor metadata. |
| `jobLabel` | string | No | The label whose value will be used as the `job` label. |
| `podTargetLabels` | list of strings | No | Labels to transfer from the Pod onto the scraped metrics. |
| `sampleLimit` | integer | No | Per-scrape limit on number of scraped samples. |
| `targetLimit` | integer | No | Limit on number of scraped targets. |
| `attachMetadata` | map | No | Metadata to attach to scraped targets (e.g., `node: true`). |
| `selector` | map | Yes | Label selector for selecting Pods. Supports `matchLabels` and `matchExpressions`. |
| `namespaceSelector` | map | No | Namespace selector. Defaults to the PodMonitor's namespace. Set `any: true` for all namespaces. |

### Pod Metrics Endpoint Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `podMetricsEndpoints` | list of maps | Yes | A list of pod metrics endpoint configurations. |
| `podMetricsEndpoints[].port` | string | Yes | Name of the Pod port to scrape. |
| `podMetricsEndpoints[].path` | string | No | HTTP path to scrape. Defaults to `/metrics`. |
| `podMetricsEndpoints[].interval` | string | No | Scrape interval. Defaults to `30s`. |
| `podMetricsEndpoints[].scrapeTimeout` | string | No | Scrape timeout. Defaults to `10s`. |
| `podMetricsEndpoints[].scheme` | string | No | HTTP scheme (`http` or `https`). |
| `podMetricsEndpoints[].honorLabels` | boolean | No | Whether to honor metrics labels over target labels. |
| `podMetricsEndpoints[].honorTimestamps` | boolean | No | Whether to honor metrics timestamps. |
| `podMetricsEndpoints[].params` | map | No | URL parameters to add to the scrape request. |
| `podMetricsEndpoints[].basicAuth` | map | No | BasicAuth credentials for scraping. |
| `podMetricsEndpoints[].authorization` | map | No | Authorization header configuration. |
| `podMetricsEndpoints[].oauth2` | map | No | OAuth2 configuration for scraping. |
| `podMetricsEndpoints[].tlsConfig` | map | No | TLS configuration for scraping. |
| `podMetricsEndpoints[].bearerTokenSecret` | map | No | Secret containing the bearer token. |
| `podMetricsEndpoints[].proxyUrl` | string | No | Proxy URL for scraping. |
| `podMetricsEndpoints[].followRedirects` | boolean | No | Whether to follow HTTP redirects. |
| `podMetricsEndpoints[].enableHttp2` | boolean | No | Whether to enable HTTP2 for scraping. |
| `podMetricsEndpoints[].filterRunning` | boolean | No | Whether to filter out non-running pods. |
| `podMetricsEndpoints[].metricRelabelings` | list of maps | No | Metric relabeling configurations. |
| `podMetricsEndpoints[].relabelings` | list of maps | No | Relabeling configurations. |

## Example

```yaml
podmonitors:
  my-pods:
    name: my-pod-monitor
    namespace: my-namespace
    selector:
      matchLabels:
        app: my-app
    podMetricsEndpoints:
      - port: http-metrics
        path: /metrics
        interval: 30s
        honorLabels: true
        tlsConfig:
          insecureSkipVerify: true
```
