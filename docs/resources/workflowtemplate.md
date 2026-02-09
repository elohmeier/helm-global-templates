# WorkflowTemplate (Argo Workflows)

## Parameters for `workflowtemplates`

| Parameter            | Type         | Required | Description                                                                                                  |
| -------------------- | ------------ | -------- | ------------------------------------------------------------------------------------------------------------ |
| `workflowtemplates`  | List of maps | Yes      | A list containing WorkflowTemplate configurations. Each item in the list defines a WorkflowTemplate.         |
| `name`               | string       | Yes      | The name of the WorkflowTemplate.                                                                            |
| `disabled`           | boolean      | No       | If true, disables the WorkflowTemplate.                                                                      |
| `namespace`          | string       | Yes      | The namespace in which the WorkflowTemplate should be created.                                               |
| `labels`             | map          | No       | Custom labels for the WorkflowTemplate.                                                                      |
| `annotations`        | map          | No       | Annotations for the WorkflowTemplate metadata.                                                               |
| `spec`               | map          | Yes      | The full WorkflowTemplate spec. Supports automatic conversions (see below).                                  |

## Automatic Conversions

The template applies several convenience transformations to the `spec`:

- **`spec.templates`**: Can be provided as a map (keyed by name) instead of a list. Map keys are used as template names.
- **`spec.volumes`**: Can be provided as a map (keyed by name) instead of a list. Map keys are used as volume names.
- **`container.env`**: Within each template, environment variables can be provided as a map (`key: value` or `key: {valueFrom: ...}`) instead of a list.
- **`container.image`**: Can be provided as a structured object (`registry`, `repository`, `tag`) instead of a string. The registry defaults to `ghcr.io`.

## Example of a Simple WorkflowTemplate

```yaml
workflowtemplates:
  - name: my-workflow
    namespace: my-namespace
    spec:
      entrypoint: main
      templates:
        main:
          container:
            image:
              registry: docker.io
              repository: busybox
              tag: latest
            command: ["echo", "hello"]
            env:
              MESSAGE: "Hello World"
```
