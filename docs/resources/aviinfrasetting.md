# AviInfraSetting

## Parameters for `aviinfrasettings`

| Parameter          | Type         | Required | Description                                                                                              |
| ------------------ | ------------ | -------- | -------------------------------------------------------------------------------------------------------- |
| `aviinfrasettings` | List of maps | Yes      | A list containing AviInfraSetting configurations. Each item in the list defines an AviInfraSetting.      |
| `name`             | string       | Yes      | The name of the AviInfraSetting.                                                                         |
| `disabled`         | boolean      | No       | If true, disables the AviInfraSetting.                                                                   |
| `labels`           | map          | No       | Custom labels for the AviInfraSetting.                                                                   |
| `annotations`      | map          | No       | Annotations for the AviInfraSetting metadata.                                                            |
| `...`              | any          | No       | All other fields are passed directly to the resource `spec`. See AKO documentation for available fields. |

## Example of a Simple AviInfraSetting

```yaml
aviinfrasettings:
  - name: example-aviinfrasetting
    sepiVipNetworkList:
      - networkName: vip-network
        cidr: 10.0.0.0/24
    enableRhi: false
```
