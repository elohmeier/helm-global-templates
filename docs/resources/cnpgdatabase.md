# CNPG Database

## Parameters for `cnpgdatabases`

| Parameter          | Type         | Required | Description                                                                                      |
| ------------------ | ------------ | -------- | ------------------------------------------------------------------------------------------------ |
| `cnpgdatabases`    | List of maps | Yes      | A list containing CNPG Database configurations. Each item in the list defines a CNPG Database.   |
| `name`             | string       | Yes      | The name of the Database resource.                                                               |
| `disabled`         | boolean      | No       | If true, disables the Database.                                                                  |
| `namespace`        | string       | Yes      | The namespace in which the Database should be created.                                           |
| `labels`           | map          | No       | Custom labels for the Database.                                                                  |
| `annotations`      | map          | No       | Annotations for the Database metadata.                                                           |
| `databaseName`     | string       | No       | The name of the database in PostgreSQL. Defaults to `name` if not provided.                      |
| `owner`            | string       | Yes      | The owner role of the database.                                                                  |
| `cluster.name`     | string       | Yes      | The name of the CNPG Cluster this database belongs to.                                           |
| `encoding`         | string       | No       | The character encoding for the database.                                                         |
| `locale`           | string       | No       | The locale for the database.                                                                     |
| `lcCollate`        | string       | No       | The LC_COLLATE setting for the database.                                                         |
| `lcCtype`          | string       | No       | The LC_CTYPE setting for the database.                                                           |
| `isTemplate`       | boolean      | No       | If true, marks the database as a template.                                                       |
| `allowConnections` | boolean      | No       | If false, prevents connections to the database.                                                  |
| `connectionLimit`  | integer      | No       | The maximum number of concurrent connections to the database.                                    |
| `tablespace`       | string       | No       | The default tablespace for the database.                                                         |

## Example of a Simple CNPG Database

```yaml
cnpgdatabases:
  - name: mydb
    namespace: my-namespace
    owner: myuser
    cluster:
      name: my-postgres
    encoding: UTF8
    locale: en_US.UTF-8
```
