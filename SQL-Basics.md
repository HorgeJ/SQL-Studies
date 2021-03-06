# SQL-Studies
## SQL study notes and example queries.

## The **SELECT** statement

retrieves a result (column), or a set of results from a query.
 ```
 SELECT <column name> FROM <table name>;
```

ex: `SELECT email FROM users;`

retrieves all items from the *email* column from the *users* table.

    `SELECT first_name, last_name, address FROM customers;`
 retrieves all items from *multiple columns* from the *customers* table.
 
 ## The **FROM** Statement
 
the table we wish to retrieve our information from
 
 
 ## Selecting all COLUMNS and ROWS in a table
 
 The Astrisks means all columns
 
 ```
 SELECT <*> FROM <table name>;
 ```
 ex: `SELECT * FROM phonebook;`
 
retrieves all columns from the *phonebook* table 

## Renaming Column Names
Using the **AS** keyword renames a column to a prefered name

```SELECT <column name> AS <alias> FROM <table name>```

ex: `SELECT last_name AS "Last Name" FROM customers;`

renames the last_name column to "Last Name" to help with readability. String literals must be in double quotes

## Counting Rows
using the **COUNT()** function will returns the int number of rows that matches a specified criteria.

ex: ` SELECT COUNT(*) FROM country `

will return a number equal to the total number of rows in the country table

## The **WHERE** statement

selects specific ROWS from a table

`SELECT <columns> FROM <table> WHERE <condition>;`

ex: `SELECT name, continent, region FROM coutry WHERE continent = europe;`

ex: `SELECT title FROM books WHERE publish_date = "2018-10-23";`

retrieves *name, continent and region* columns from the *country* table where the column *continent is equal to Europe*

## Inequality Operator **!=**

finds rows where the given value does not match

ex: `SELECT name FROM users WHERE name != "Bob";`

retrieves all rows where name does not equal "Bob"

## Comparing Values

comparing expressions can be done using relational operators

```
SELECT <columns> FROM <table> WHERE <column name> < <value>;
SELECT <columns> FROM <table> WHERE <column name> <= <value>;
SELECT <columns> FROM <table> WHERE <column name> > <value>;
SELECT <columns> FROM <table> WHERE <column name> >= <value>;
```

ex: `SELECT item_name FROM products WHERE price < 19.99;`

ex: `SELECT first_name, last_name FROM customers WHERE age >= 21;`

## Multiple Conditions

The **AND** & **OR** keywords are used to compare more than one value. Resolves to a bool value.

```
SELECT <columns> FROM <table> WHERE <column name> = <value> AND <column name> = <value>
SELECT <columns> FROM <table> WHERE <column name> != <value> OR <column name> = <value>

```

ex: `SELECT username FROM users WHERE location = "United States" AND age >= 21;`
retrieve usernames from the users table where location is United States AND age is 21 or over

ex: `SELECT name FROM products WHERE price < 10.95 OR price > 99.99;`
retrieve name from products table where price is less than 10.95 Or price is greater than 99.99

ex: `SELECT name FROM users WHERE date_of_birth < '1988-10-04';`

## Searching a Set of Values | the **IN** operator

the **IN** operator allows you to specify multiple values in a WHERE clause.

It is the shorthand for multiple OR conditions

```
SELECT <columns> FROM <table> WHERE <column> IN (<value 1>, <value 2>, ...);
```

ex: `SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');`
this statement retreives all customers where the Country value is equal to Germany, France and UK

ex: `SELECT * FROM Customers WHERE Country NOT IN ('Germany', 'France', 'UK');`
this statement retreives all customers where the Country value is NOT equal to Germany, France and UK

## The **WHERE** Keyword | Searching Within a Range

The BETWEEN operator selects values within a given range. The values can be numbers, text, or dates

The smallest value must come first, followed by the larger value

```
SELECT <columns> FROM <table> WHERE <column> BETWEEN <lesser value> AND <greater value>;
```
ex: `SELECT * FROM Products WHERE Price BETWEEN 9.99 AND 11.99;`
retrieves all products from the Products table where price is BETWEEN 9.99 and 11.99

## The **LIKE** Keyword | Finding Data that Matches a Pattern

The **LIKE** operator is used in a WHERE clause to search for a specified pattern in a column.

Placing the percent symbol (%) any where in a string in conjunction with the LIKE keyword will operate as a wildcard. Meaning it can be substituted by any number of characters, including zero.

```
SELECT <columns> FROM <table> WHERE <column> LIKE <pattern>;
```

ex: `SELECT * FROM customers WHERE name LIKE "a%";`
retrieves all customers whos names start with "a"

ex: `SELECT * FROM customers WHERE name LIKE "%a"`
retrieves all customers whos names end with "a"

ex: `SELECT * FROM customers WHERE name LIKE "%or%"`
retrieves all customers who name contains "or" at any position

ex: `SELECT * FROM customers WHERE name LIKE "a%f"`
retrieves all customers where name stars with "a" and ends with "f"

ex: `SELECT * FROM customers WHERE name NOT LIKE "a%"`
retrieves all customers where the name DOES NOT start with "a"

## **NULL** Values | Filtering Out Missing Values

A field with a NULL value is a field with no value.

If a field in a table is optional, it is possible to insert a new record or update a record without adding a value to this field. Then, the field will be saved with a NULL value.

```
SELECT <column> FROM <table> WHERE <column value> IS NULL;
SELECT <column> FROM <table> WHERE <column value> IS NOT NULL;
```

ex: `SELECT name, address FROM customers WHERE address IS NULL;`
retrieve name and address columns where the address value is NULL


## **INSERT INTO** Keyword | Adding a ROW to a TABLE

The INSERT INTO statement is used to insert new records in a table.

```
INSERT INTO <table> VALUES (<value 1>, <value 2>, <value 3>, etc...);
```

ex: `INSERT INTO movies VALUES (3, "Starman", "Science Fiction", 1984);`
inserts the values 3, "Starman", "Science Fiction", 1984 into the movies table.

```
INSERT INTO (<table> <column 1>, <column 2>) VALUES (<value 1>, <value 2>);
```
INSERT INTO the columns we want to enter values into and then specify the values in that same order


ex: `INSERT INTO users (username, first_name, last_name) VALUES ("Bloodweiser", "Horge", "Jorge");`
Inserts into the users table, the columns username, first_name and last_name and gives them the corresponding values.

### Multiple Rows

```
INSERT INTO <table> (<column 1>, <column 2>, ...) 
             VALUES 
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...),
                    (<value 1>, <value 2>, ...);
```
short cut for adding multiple rows without making individual queries to the database for each

## **UPDATE** Statement | Updating Rows in a Table
Used to modify existing records in a table

```
UPDATE <table> SET <column> = <value> WHERE <condition> ;
```
any number of condistions may be used and all matching rows will be updated


ex: `UPDATE Customers SET Name = 'Alfred' WHERE CustomerID = 1;`

This statement updates the customers name where the CustomerID field is equal to '1'

ex:
```
UPDATE users SET password = "thisisabadidea" WHERE id = 3;
UPDATE blog_posts SET view_count = 1923 WHERE title = "SQL is Awesome";
```
Updating multiple cloumns in a specific row

```
UPDATE <table> SET <column 1> = <value 1>, <column 2> = <value 2> WHERE <condition>;
```

ex:
```
UPDATE users SET entry_url = "/home", last_login = "2016-01-05" WHERE id = 329;
UPDATE products SET status = "SOLD OUT", availability = "In 1 Week" WHERE stock_count = 0;
```

## The **DELETE** Statement | Removing Data
Used to delete existing records in a table. ***WARNING***: Omiting the WHERE clause will delete all records in a table. ALWAYS HAVE A BACKUP!!!!

```
DELETE FROM <table> WHERE <condition>;
```

ex: 
```
DELETE FROM users WHERE email = "badEmail@funnymail.com";
DELETE FROM books WHERE genre = "Mystery";
DELETE FROM products WHERE stock_count = 0;
```

## Transactions

**Autocommit** - every statement you write gets saved to disk
**Seeding** - populating a database for the first time.
**Script file** - a file containing SQL statements.

```
BEGIN TRANSACTION;
```
This switches autocommit off and begins transaction

```
COMMIT;
```
This saves all the results of the statements after the start transaction to disk

```
ROLLBACK;
```
This resets the state of the database to before the beginning of the transaction
