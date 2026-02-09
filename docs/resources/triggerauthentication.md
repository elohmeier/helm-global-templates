# TriggerAuthentication (KEDA)

## Parameters for `triggerauthentications`

| Parameter                        | Type         | Required | Description                                                                                                       |
| -------------------------------- | ------------ | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `triggerauthentications`         | List of maps | Yes      | A list containing TriggerAuthentication configurations. Each item in the list defines a TriggerAuthentication.    |
| `name`                           | string       | No       | The name of the TriggerAuthentication.                                                                            |
| `disabled`                       | boolean      | No       | If true, disables the TriggerAuthentication.                                                                      |
| `namespace`                      | string       | Yes      | The namespace in which the TriggerAuthentication should be created.                                               |
| `labels`                         | map          | No       | Custom labels for the TriggerAuthentication.                                                                      |
| `annotations`                    | map          | No       | Annotations for the TriggerAuthentication metadata.                                                               |
| `reloaderEnabled`                | boolean      | No       | If true, enables reloader annotations.                                                                            |
| `secretTargetRef`                | List of maps | Yes      | A list of secret target references for authentication.                                                            |
| `secretTargetRef[].name`         | string       | Yes      | The name of the Kubernetes Secret.                                                                                |
| `secretTargetRef[].key`          | string       | Yes      | The key within the Secret.                                                                                        |
| `secretTargetRef[].parameter`    | string       | Yes      | The parameter name exposed to the trigger.                                                                        |

## Example of a Simple TriggerAuthentication

```yaml
triggerauthentications:
  - name: kafka-auth
    namespace: my-namespace
    secretTargetRef:
      - name: kafka-credentials
        key: username
        parameter: username
      - name: kafka-credentials
        key: password
        parameter: password
```
