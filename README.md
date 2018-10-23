# SQL-Studies
## SQL study notes and example queries.

## The **SELECT** statement

returns a result (column), or a set of results from a query.
 ```
 SELECT <column name> FROM <table name>;
```

ex: `SELECT email FROM users;`
returns all items from the *email* column from the *users* table.

    `SELECT first_name, last_name, address FROM customers;`
 returns all items from *multiple columns* from the *customers* table.
 
 
 
 ## Selecting all COLUMNS and ROWS in a table
 
 The Astrisks means all columns
 
 ```
 SELECT <*> FROM <table name>;
 ```
 ex: `SELECT * FROM phonebook;
 `
returns all columns from the *phonebook* table 

## Selecting ROWS

