# SQL Server User Management

### Opvragen users en schema's

```sql
SELECT name, type_desc, default_schema_name
FROM sys.database_principals
WHERE type in ('S', 'U', 'G');
```

### Toekennen schema

```sql
ALTER USER [GVAGROUP\EAN00425] WITH DEFAULT_SCHEMA=[dbo]
```


