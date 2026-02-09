# HTTPRoute

## Parameters for `httproutes`

| Parameter                                    | Type            | Required | Description                                                                                    |
| -------------------------------------------- | --------------- | -------- | ---------------------------------------------------------------------------------------------- |
| `httproutes`                                 | Map of maps     | Yes      | A map containing HTTPRoute configurations. The map key is used as the default name.            |
| `name`                                       | string          | No       | The name of the HTTPRoute. Defaults to the map key.                                            |
| `disabled`                                   | boolean         | No       | If true, disables the HTTPRoute.                                                               |
| `namespace`                                  | string          | Yes      | The namespace in which the HTTPRoute should be created.                                        |
| `labels`                                     | map             | No       | Custom labels for the HTTPRoute.                                                               |
| `annotations`                                | map             | No       | Annotations for the HTTPRoute metadata.                                                        |
| `parentRefs`                                 | List of maps    | No       | A list of parent Gateway references.                                                           |
| `parentRefs[].name`                          | string          | Yes      | The name of the parent Gateway.                                                                |
| `parentRefs[].namespace`                     | string          | No       | The namespace of the parent Gateway.                                                           |
| `parentRefs[].sectionName`                   | string          | No       | The section name (listener) on the parent Gateway.                                             |
| `parentRefs[].port`                          | integer         | No       | The port on the parent Gateway.                                                                |
| `hostnames`                                  | List of strings | No       | A list of hostnames for the HTTPRoute. Supports global value rendering.                        |
| `rules`                                      | List of maps    | No       | A list of routing rules.                                                                       |
| `rules[].matches`                            | List of maps    | No       | A list of match conditions for the rule.                                                       |
| `rules[].matches[].path.type`               | string          | No       | The path match type. Defaults to `PathPrefix`.                                                 |
| `rules[].matches[].path.value`              | string          | No       | The path value. Defaults to `/`.                                                               |
| `rules[].matches[].headers`                 | List of maps    | No       | Header match conditions.                                                                       |
| `rules[].matches[].queryParams`             | List of maps    | No       | Query parameter match conditions.                                                              |
| `rules[].matches[].method`                  | string          | No       | HTTP method match (e.g., `GET`, `POST`).                                                       |
| `rules[].filters`                            | List of maps    | No       | A list of filters for the rule.                                                                |
| `rules[].filters[].type`                    | string          | Yes      | Filter type: `RequestHeaderModifier`, `ResponseHeaderModifier`, `RequestRedirect`, `URLRewrite`, `RequestMirror`, or `ExtensionRef`. |
| `rules[].backendRefs`                        | List of maps    | No       | A list of backend references.                                                                  |
| `rules[].backendRefs[].name`                | string          | Yes      | The name of the backend service.                                                               |
| `rules[].backendRefs[].namespace`           | string          | No       | The namespace of the backend service.                                                          |
| `rules[].backendRefs[].port`                | integer         | No       | The port on the backend service.                                                               |
| `rules[].backendRefs[].weight`              | integer         | No       | Traffic weight for the backend.                                                                |
| `rules[].backendRefs[].kind`                | string          | No       | The kind of the backend (e.g., `Service`, `Backend`).                                          |
| `rules[].backendRefs[].group`               | string          | No       | The API group of the backend.                                                                  |
| `rules[].timeouts`                           | map             | No       | Timeout configuration for the rule.                                                            |
| `rules[].timeouts.request`                  | string          | No       | Timeout for the entire request.                                                                |
| `rules[].timeouts.backendRequest`           | string          | No       | Timeout for the backend request.                                                               |

## Example of a Simple HTTPRoute

```yaml
httproutes:
  example-route:
    namespace: my-namespace
    parentRefs:
      - name: example-gateway
        namespace: gateway-namespace
    hostnames:
      - app.example.com
    rules:
      - matches:
          - path:
              type: PathPrefix
              value: /api
        backendRefs:
          - name: api-service
            port: 8080
```
