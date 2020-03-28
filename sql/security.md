# Security


### Get users in database
```sql
SELECT DISTINCT pr.principal_id, pr.name, pr.type_desc, 
    pr.authentication_type_desc, pe.state_desc, pe.permission_name
FROM sys.database_principals AS pr
JOIN sys.database_permissions AS pe
    ON pe.grantee_principal_id = pr.principal_id;
```

[source](https://stackoverflow.com/questions/31120912/how-to-view-the-roles-and-permissions-granted-to-any-database-user-in-azure-sql)

![Security overview](sql-security-overview.jpg)