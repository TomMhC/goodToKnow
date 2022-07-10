# MariaDB

## Databases

```sql
SHOW DATABASES;
```

```sql
CREATE DATABASE [database_name];
```

## Tables

```sql
SHOW TABLES FROM [table_name];
```

```sql
DESC [database_name].[table_name]; # toont table schema
```

## Users

```sql
SELECT User, Host FROM mysql.user;
```

```sql
SELECT user(); # toont current user info
```

```sql
SHOW GRANTS FOR [account_name];
SHOW GRANTS FOR [account_name]@[host_name];
```

```sql
DROP USER [account_name] [,account_name2];
```

```sql
CREATE USER [account_name]@[host_name] IDENTIFIED BY 'password';
CREATE USER [IF NOT EXISTS] account_name IDENTIFIED BY 'password'; # %
```

```sql
GRANT ALL PRIVILEGES ON [table_name].* TO account_name@host_name
```


