# Probe

## Parameters for `probes`

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `probes` | Map of maps | Yes | A map containing Probe configurations. Each key defines a Probe. |
| `name` | string | Yes | The name of the Probe. |
| `disabled` | boolean | No | If true, disables the Probe. |
| `namespace` | string | Yes | The namespace in which the Probe should be created. |
| `labels` | map | No | Custom labels for the Probe. |
| `annotations` | map | No | Annotations for the Probe metadata. |
| `jobName` | string | No | Custom job name for the probe. |
| `module` | string | No | Prober module to use (e.g., `http_2xx`). |
| `interval` | string | No | Scrape interval. Defaults to `30s`. |
| `scrapeTimeout` | string | No | Scrape timeout. Defaults to `10s`. |
| `scrapeClassName` | string | No | Scrape class name. |
| `sampleLimit` | integer | No | Per-scrape limit on number of scraped samples. |
| `targetLimit` | integer | No | Limit on number of scraped targets. |
| `metricRelabelings` | list of maps | No | Metric relabeling configurations. |

### Prober Parameters

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `prober.url` | string | Yes | URL of the prober (e.g., `blackbox-exporter:9115`). |
| `prober.scheme` | string | No | HTTP scheme for the prober. |
| `prober.path` | string | No | HTTP path for the prober. Defaults to `/probe`. |
| `prober.proxyUrl` | string | No | Proxy URL for the prober. |

### Targets

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `targets` | map | No | Targets configuration. Passed through as-is. Supports `staticConfig` and `ingress`. |

## Example

```yaml
probes:
  website-probe:
    name: website-probe
    namespace: monitoring
    prober:
      url: blackbox-exporter.monitoring:9115
    module: http_2xx
    targets:
      staticConfig:
        static:
          - https://example.com
          - https://example.org
        labels:
          environment: production
    interval: 60s
    scrapeTimeout: 30s
```
