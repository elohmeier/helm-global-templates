# VMServiceScrape (VictoriaMetrics)

## Parameters for `vmservicescrapes`

| Parameter                                | Type         | Required | Description                                                                                                |
| ---------------------------------------- | ------------ | -------- | ---------------------------------------------------------------------------------------------------------- |
| `vmservicescrapes`                       | List of maps | Yes      | A list containing VMServiceScrape configurations. Each item in the list defines a VMServiceScrape.         |
| `name`                                   | string       | Yes      | The name of the VMServiceScrape.                                                                           |
| `disabled`                               | boolean      | No       | If true, disables the VMServiceScrape.                                                                     |
| `namespace`                              | string       | Yes      | The namespace in which the VMServiceScrape should be created.                                              |
| `labels`                                 | map          | No       | Custom labels for the VMServiceScrape.                                                                     |
| `annotations`                            | map          | No       | Annotations for the VMServiceScrape metadata.                                                              |
| `selector.matchLabels`                   | map          | Yes      | Label selector to match target services.                                                                   |
| `namespaceSelector`                      | map          | No       | Namespace selector. Defaults to the resource's own namespace.                                              |
| `endpoints`                              | List of maps | Yes      | A list of scrape endpoint configurations.                                                                  |
| `endpoints[].port`                       | string       | Yes      | The named port to scrape.                                                                                  |
| `endpoints[].path`                       | string       | No       | The metrics path. Defaults to `path` in `vmservicescrape_defaults`.                                        |
| `endpoints[].interval`                   | string       | No       | The scrape interval. Defaults to `interval` in `vmservicescrape_defaults`.                                 |
| `endpoints[].scrapeTimeout`              | string       | No       | The scrape timeout. Defaults to `scrapeTimeout` in `vmservicescrape_defaults`.                             |
| `endpoints[].scheme`                     | string       | No       | The scrape scheme (e.g., `http`, `https`).                                                                 |
| `endpoints[].tlsConfig`                  | map          | No       | TLS configuration for the endpoint.                                                                        |
| `endpoints[].bearerTokenSecret`          | map          | No       | Bearer token secret reference for authentication.                                                          |
| `endpoints[].metricRelabelings`          | List of maps | No       | Metric relabeling configurations.                                                                          |
| `endpoints[].relabelings`                | List of maps | No       | Relabeling configurations.                                                                                 |

## Example of a Simple VMServiceScrape

```yaml
vmservicescrapes:
  - name: api-scrape
    namespace: my-namespace
    selector:
      matchLabels:
        app: api
    endpoints:
      - port: metrics
        path: /metrics
        interval: 30s
```
