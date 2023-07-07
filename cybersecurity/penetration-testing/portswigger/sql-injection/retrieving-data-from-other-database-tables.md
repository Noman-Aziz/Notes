# Retrieving data from other database tables

### Determining the number of columns required in an SQL injection UNION attack

When performing an SQL injection UNION attack, there are two effective methods to determine how many columns are being returned from the original query.

#### Method 1

The first method involves injecting a series of ORDER BY clauses and incrementing the specified column index until an error occurs. For example, assuming the injection point is a quoted string within the WHERE clause of the original query, you would submit:

```sql
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--
etc.
```

When the specified column index exceeds the number of actual columns in the result set, the database returns an error.

#### Method 2

The second method involves submitting a series of UNION SELECT payloads specifying a different number of null values:

```sql
' UNION SELECT NULL--
' UNION SELECT NULL,NULL--
' UNION SELECT NULL,NULL,NULL--
etc.
```

If the number of nulls does not match the number of columns, the database returns an error



### Finding columns with a useful data type in an SQL injection UNION attack

Having already determined the number of required columns, you can probe each column to test whether it can hold string data by submitting a series of UNION SELECT payloads that place a string value into each column in turn.

```sql
' UNION SELECT 'a',NULL,NULL,NULL--
' UNION SELECT NULL,'a',NULL,NULL--
' UNION SELECT NULL,NULL,'a',NULL--
' UNION SELECT NULL,NULL,NULL,'a'--
```

If the data type of a column is not compatible with string data, the injected query will cause a database error. If an error does not occur, and the application's response contains some additional content including the injected string value, then the relevant column is suitable for retrieving string data.

#### The dual table (Oracle)

On Oracle databases, every SELECT statement must specify a table to select FROM. If your UNION SELECT attack does not query from a table, you will still need to include the FROM keyword followed by a valid table name.

There is a built-in table on Oracle called dual which you can use for this purpose. For example: `UNION SELECT 'abc' FROM dual`



### Retrieving multiple values within a single column

You can easily retrieve multiple values together within this single column by concatenating the values together, ideally including a suitable separator to let you distinguish the combined values. For example, on Oracle you could submit the input:

```sql
' UNION SELECT username || '~' || password FROM users--
```

This uses the double-pipe sequence || which is a string concatenation operator on Oracle.

