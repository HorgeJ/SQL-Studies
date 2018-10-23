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

ex: `SELECT name, continent, region FROM coutry WHERE continent = europe;`

retrieves *name, continent and region* columns from the *country* table where the column *continent is equal to Europe*

