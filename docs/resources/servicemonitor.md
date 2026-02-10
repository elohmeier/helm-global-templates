# ServiceMonitor

## Parameters for `servicemonitors`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `servicemonitors` | Map of maps | Yes | A map containing ServiceMonitor configurations. Each key defines a ServiceMonitor. |
| `name` | string | Yes | The name of the ServiceMonitor. |
| `disabled` | boolean | No | If true, disables the ServiceMonitor. |
| `namespace` | string | Yes | The namespace in which the ServiceMonitor should be created. |
| `labels` | map | No | Custom labels for the ServiceMonitor. |
| `annotations` | map | No | Annotations for the ServiceMonitor metadata. |
| `jobLabel` | string | No | The label whose value from the selected Service will be used as the `job` label. |
| `targetLabels` | list of strings | No | Labels to transfer from the Service onto the scraped metrics. |
| `podTargetLabels` | list of strings | No | Labels to transfer from the Pod onto the scraped metrics. |
| `sampleLimit` | integer | No | Per-scrape limit on number of scraped samples. |
| `targetLimit` | integer | No | Limit on number of scraped targets. |
| `attachMetadata` | map | No | Metadata to attach to scraped targets (e.g., `node: true`). |
| `selector` | map | Yes | Label selector for selecting Services. Supports `matchLabels` and `matchExpressions`. |
| `namespaceSelector` | map | No | Namespace selector. Defaults to the ServiceMonitor's namespace. Set `any: true` for all namespaces. |

### Endpoint Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `endpoints` | list of maps | Yes | A list of endpoint configurations. |
| `endpoints[].port` | string | Yes | Name of the Service port to scrape. |
| `endpoints[].path` | string | No | HTTP path to scrape. Defaults to `/metrics`. |
| `endpoints[].interval` | string | No | Scrape interval. Defaults to `30s`. |
| `endpoints[].scrapeTimeout` | string | No | Scrape timeout. Defaults to `10s`. |
| `endpoints[].scheme` | string | No | HTTP scheme (`http` or `https`). |
| `endpoints[].honorLabels` | boolean | No | Whether to honor metrics labels over target labels. |
| `endpoints[].honorTimestamps` | boolean | No | Whether to honor metrics timestamps. |
| `endpoints[].params` | map | No | URL parameters to add to the scrape request. |
| `endpoints[].basicAuth` | map | No | BasicAuth credentials for scraping. |
| `endpoints[].authorization` | map | No | Authorization header configuration. |
| `endpoints[].oauth2` | map | No | OAuth2 configuration for scraping. |
| `endpoints[].tlsConfig` | map | No | TLS configuration for scraping. |
| `endpoints[].bearerTokenSecret` | map | No | Secret containing the bearer token. |
| `endpoints[].proxyUrl` | string | No | Proxy URL for scraping. |
| `endpoints[].followRedirects` | boolean | No | Whether to follow HTTP redirects. |
| `endpoints[].enableHttp2` | boolean | No | Whether to enable HTTP2 for scraping. |
| `endpoints[].filterRunning` | boolean | No | Whether to filter out non-running pods. |
| `endpoints[].metricRelabelings` | list of maps | No | Metric relabeling configurations. |
| `endpoints[].relabelings` | list of maps | No | Relabeling configurations. |

## Example

```yaml
servicemonitors:
  my-service:
    name: my-service-monitor
    namespace: my-namespace
    jobLabel: app
    targetLabels:
      - instance
    selector:
      matchLabels:
        app: my-app
    endpoints:
      - port: http-metrics
        path: /metrics
        interval: 30s
        honorLabels: true
        tlsConfig:
          insecureSkipVerify: true
        metricRelabelings:
          - sourceLabels: [__name__]
            regex: "expensive_.*"
            action: drop
```
