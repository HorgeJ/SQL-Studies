## SQL Queries with MySQL
MySQL is the world's most popular open source database. With its proven performance, reliability and ease-of-use, MySQL has become the leading database choice for web-based applications, used by high profile web properties including Facebook, Twitter, YouTube, Yahoo! and many more.

Oracle drives MySQL innovation, delivering new capabilities to power next generation web, cloud, mobile and embedded applications.

### Create Database
Create a database with a specified name if it does not exist in database server
```
CREATE DATABASE <database_name>;
```

### Use Database
Use database or change current database to another database you are working with
```
USE <database_name>;
```

### Drop Database
Drop a database with specified name permanently. All physical file associated with the database is no longer exists.
```
DROP DATABASE <database_name>;
```

### Show Databases
Show databases
```
SHOW DATABASES
```

## Tables
SQL database table. The foundation of every Relational Database Management System is a database object called table. Every database consists of one or more tables, which store the database’s data/information. Each table has its own unique name and consists of columns and rows.

### Creating Tables
Usually name tables with plural spelling

```
CREATE TABLE tablename
(
  column_name data_type,
  column_name data_type
);
```
ex:
```SQL
CREATE TABLE dogs
(
  name VARCHAR(100),
  age int
);
```

### Show Tables
SHOW TABLES lists the non-TEMPORARY tables in a given database. You can also get this list using the mysqlshow db_name command. The LIKE clause, if present, indicates which table names to match.


```
SHOW TABLES
```

```
SHOW COLUMNS FROM <table name>;
```


