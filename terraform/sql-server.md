# SQL Server

### SQL server configuration
```
  sku {
    name     = "GP_Gen5"
    tier     = "GeneralPurpose"
    family   = "Gen5"
    capacity = 6
  }
  per_database_settings {
    min_capacity = 0.25
    max_capacity = 6
  }
```

[source](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
[source](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)


### Database/elastic pool configuration
```
  sku {
    name     = "BasicPool"
    capacity = 50
    tier     = "Basic”å
    family   = "Gen5"
  }

  per_database_settings {
    min_capacity = 0
    max_capacity = 5
  }
```

```
az sql elastic-pool list --resource-group <resource-group-name> --server <sql-server-name>
```

