# CNPG Cluster

## Parameters for `cnpgclusters`

| Parameter                     | Type         | Required | Description                                                                                  |
| ----------------------------- | ------------ | -------- | -------------------------------------------------------------------------------------------- |
| `cnpgclusters`                | List of maps | Yes      | A list containing CNPG Cluster configurations. Each item in the list defines a CNPG Cluster. |
| `name`                        | string       | Yes      | The name of the Cluster.                                                                     |
| `disabled`                    | boolean      | No       | If true, disables the Cluster.                                                               |
| `namespace`                   | string       | Yes      | The namespace in which the Cluster should be created.                                        |
| `labels`                      | map          | No       | Custom labels for the Cluster.                                                               |
| `annotations`                 | map          | No       | Annotations for the Cluster metadata.                                                        |
| `instances`                   | integer      | No       | The number of PostgreSQL instances. Defaults to `instances` in `cnpgcluster_defaults`.       |
| `imageName`                   | string       | No       | The PostgreSQL image name. Defaults to `imageName` in `cnpgcluster_defaults`.                |
| `enableSuperuserAccess`       | boolean      | No       | Enable superuser access. Defaults to `enableSuperuserAccess` in `cnpgcluster_defaults`.      |
| `superuserSecret.name`        | string       | No       | The name of the secret containing superuser credentials.                                     |
| `bootstrap.initdb.database`   | string       | Yes      | The name of the database to create during bootstrap.                                         |
| `bootstrap.initdb.owner`      | string       | Yes      | The owner of the database created during bootstrap.                                          |
| `bootstrap.initdb.secret.name`| string       | No       | The name of the secret for the bootstrap database owner credentials.                         |
| `managed.roles`               | List of maps | No       | A list of managed database roles.                                                            |
| `postgresql.parameters`       | map          | No       | PostgreSQL configuration parameters.                                                         |
| `resources`                   | map          | No       | Resource requests and limits for the PostgreSQL instances.                                   |
| `storage.size`                | string       | No       | The size of the persistent storage. Defaults to `storage.size` in `cnpgcluster_defaults`.    |
| `storage.storageClass`        | string       | No       | The storage class for the persistent volume.                                                 |

## Example of a Simple CNPG Cluster

```yaml
cnpgclusters:
  - name: my-postgres
    namespace: my-namespace
    instances: 3
    bootstrap:
      initdb:
        database: mydb
        owner: myuser
        secret:
          name: myuser-credentials
    storage:
      size: 10Gi
      storageClass: standard
```
