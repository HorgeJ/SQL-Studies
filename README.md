# SQL-Studies
## SQL study notes and example queries.

## The **SELECT** statement

retrieves a result (column), or a set of results from a query.
 ```
 SELECT <column name> FROM <table name>;
```

ex: `SELECT email FROM users;`
returns all items from the *email* column from the *users* table.

    `SELECT first_name, last_name, address FROM customers;`
 returns all items from *multiple columns* from the *customers* table.
 
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

ex: `SELECT * FROM Customers WHERE Country IN ('Germany', 'France', 'UK');`
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
