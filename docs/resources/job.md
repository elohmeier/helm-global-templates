# Job

## Parameters for `jobs`

| Parameter                               | Type                | Required | Description                                                                         |
| --------------------------------------- | ------------------- | -------- | ----------------------------------------------------------------------------------- |
| `jobs`                                  | List of maps        | Yes      | A list containing Job configurations. Each item in the list defines a Job.          |
| `name`                                  | string              | No       | The name of the Job.                                                                |
| `disabled`                              | boolean             | No       | If true, disables the Job.                                                          |
| `namespace`                             | string              | Yes      | The namespace in which the Job should be created.                                   |
| `labels`                                | map                 | No       | Custom labels for the Job.                                                          |
| `annotations`                           | map                 | No       | Annotations for the Job metadata.                                                   |
| `activeDeadlineSeconds`                 | integer             | No       | Maximum duration in seconds for the Job to run.                                     |
| `backoffLimit`                          | integer             | No       | Number of retries before marking the Job as failed. Defaults to `6`.                |
| `completions`                           | integer             | No       | Number of successful completions required.                                          |
| `parallelism`                           | integer             | No       | Maximum number of pods running in parallel.                                         |
| `completionMode`                        | string              | No       | Completion mode (e.g., `NonIndexed`, `Indexed`).                                    |
| `ttlSecondsAfterFinished`              | integer             | No       | Time to live after the Job finishes.                                                |
| `podAnnotations`                        | map                 | No       | Annotations for the pod template.                                                   |
| `podLabels`                             | map                 | No       | Custom labels for the pod template.                                                 |
| `restartPolicy`                         | string              | No       | The restart policy. Defaults to `Never`.                                            |
| `serviceAccountName`                    | string              | No       | The service account name for the pod.                                               |
| `imagePullSecrets`                      | List of maps        | No       | Image pull secrets for the pod.                                                     |

## Container-Level Parameters

| Parameter                               | Type                | Required | Description                                                                         |
| --------------------------------------- | ------------------- | -------- | ----------------------------------------------------------------------------------- |
| `containers`                            | List of maps        | Yes      | A list of container configurations.                                                 |
| `containers[].name`                     | string              | Yes      | The name of the container.                                                          |
| `containers[].image`                    | object              | Yes      | Container image details (`registry`, `repository`, `tag`).                          |
| `containers[].imagePullPolicy`          | string              | No       | The pull policy for the image.                                                      |
| `containers[].command`                  | List of strings     | No       | The command to run in the container.                                                |
| `containers[].args`                     | List of strings     | No       | Arguments for the container's command.                                              |
| `containers[].env`                      | List of maps        | No       | Environment variables for the container.                                            |
| `containers[].envFrom`                  | List of maps        | No       | Environment sources (e.g., `configMapRef`, `secretRef`).                            |
| `containers[].resources`                | object              | No       | Resource requests and limits.                                                       |
| `containers[].securityContext`          | object              | No       | Security settings for the container.                                                |
| `containers[].volumeMounts`             | List of maps or map | No       | Volume mounts for the container.                                                    |

## Other Parameters

| Parameter                         | Type                | Required | Description                                                     |
| --------------------------------- | ------------------- | -------- | --------------------------------------------------------------- |
| `volumes`                         | List of maps or map | No       | Volumes available to containers (secret, configMap, emptyDir, hostPath, PVC, image). |
| `affinity`                        | object              | No       | Affinity rules for scheduling.                                  |
| `nodeSelector`                    | map                 | No       | Node selection criteria.                                        |
| `tolerations`                     | List of maps        | No       | Tolerations for pod scheduling.                                 |
| `securityContext`                 | object              | No       | Pod-level security settings.                                    |

## Example of a Simple Job

```yaml
jobs:
  - name: db-migration
    namespace: my-namespace
    backoffLimit: 3
    ttlSecondsAfterFinished: 3600
    containers:
      - name: migrate
        image:
          registry: docker.io
          repository: myapp/migrate
          tag: "1.0.0"
        command: ["./migrate", "up"]
        envFrom:
          - secretRef:
              name: db-credentials
```
