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

### Dropping Tables (Deleting)
In MySQL, DROP TABLE command removes one or more tables from an existing database. 

```
DROP TABLE <table name>;
```

### INSERT INTO
To insert data into a MySQL table, you would need to use the SQL INSERT INTO command. You can insert data into the MySQL table by using the mysql> prompt or by using any script like PHP.
```
INSERT INTO table_name ( field1, field2,...fieldN )
   VALUES
   ( value1, value2,...valueN );
```

ex:
```SQL
INSERT INTO cats(name, age)
VALUES ('Jetson', 3);
```

### Multiple INSERT
We can use a comma spereated list to insert multiple rows into table.
```
INSERT INTO table_name (<column name>, <column name>) 
VALUES      (value, value), 
            (value, value), 
            (value, value);
```

ex: 
```SQL
CREATE TABLE people(
  first_name VARCHAR(20),
  last_name VARCHAR(20),
  age int
);

INSERT INTO people(first_name, last_name, age)
VALUES('Tina', 'Belcher', 13);

INSERT INTO people(first_name, last_name, age)
VALUES('Linda', 'Belcher', 45),
      ('Phillip', 'Frond'),
      ('Calvin', 'Fischoeder', 70);
```

### NOT NULL
When storing data, when a value isnt specified, a cell will be populated with a NULL value, which is NOT 0 but a value with no value? 

We can specify in the table creation to not allow NULL values for specific columns.

ex:
```SQL
CREATE TABLE cats (
  name VARCHAR(20) NOT NULL,
  age INT NOT NULL
);
```
In this example the inlcusion of NOT NULL atfer the datatype specifies that an actual value must be provided when inserting a row.

Creating a row without specifying values, a default value will be inserted instead of NULL.

### DEFAULT 
We can specify default values to be used in the case that one is not provided upon creation of row.

ex:
```SQL
CREATE TABLE cats(
  name VARCHAR(20) DEFAULT 'unnamed',
  age INT DEFAULT 99
);
```

### Primary Keys
A primary key is a column or a set of columns that uniquely identifies each row in the table. You must follow the rules below when you define a primary key for a table: ... Because MySQL works faster with integers, the data type of the primary key column should be the integer e.g., INT, BIGINT.You can choose a smaller integer type: TINYINT, SMALLINT, etc.

ex: Define a table with a PRIMARY KEY constraint and AUTO INCREMENT
```sql
CREATE TABLE unique_cats (
    cat_id INT NOT NULL AUTO_INCREMENT,
    name VARCHAR(100),
    age INT,
    PRIMARY KEY (cat_id)
);
```

Define an Employees table, with the following fields:\
* id - number(automatically increments), mandatory, primary key
* last_name - text, mandatory
* first_name - text, mandatory 
* middle_name - text, not mandatory 
* age - number mandatory 
* current_status - text, mandatory, defaults to 'employed'

```SQL
CREATE TABLE Employees (
  id INT NOT NULL AUTO_INCERMENT,
  last_name VARCHAR(25) NOT NULL,
  first_name VARCHAR(25) NOT NULL,
  middle_name VARCHAR(25),
  age INT NOT NULL,
  current_status VARVCHAR(25) NOT NULL DEFAULT 'employed',
  PRIMARY KEY(id)
);
```

### INSERT INTO
INSERT inserts new rows into an existing table

```
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```

ex: creating new table and inserting data
