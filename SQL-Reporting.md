## ORDER BY Keyword | Organizing Information by Rows: Single Criteria
The ORDER BY keyword is used to sort the result-set in ascending or descending order.

The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

```
SELECT <col1>, <col2>, ... FROM <table> ORDER BY <col1>, <col2>, ... ASC|DESC;
```
ex:
```
SELECT name FROM books ORDER BY title ASC;
SELECT product FROM products WHERE price > 9.99 ORDER BY price DESC;
SELECT * FROM countries ORDER BY population DESC;
SELECT * FROM reviews ORDER BY username;
```

## Ordering Rows: Multiple Criteria
```
SELECT * FROM <table name> ORDER BY <column> [ASC|DESC],
                                    <column 2> [ASC|DESC],
                                    ...,
                                    <column n> [ASC|DESC];
```

ex:
```
SELECT * FROM books ORDER BY    genre ASC, 
                                title ASC;

SELECT * FROM books ORDER BY    genre ASC,
                                year_published DESC;

SELECT * FROM users ORDER BY    last_name ASC,
                                first_name ASC;
```

## LIMIT Keyword | Limiting the Number of Results
The SQL SELECT LIMIT statement is used to retrieve records from one or more tables in a database and limit the number of records returned based on a limit value. 

```
SELECT <columns> FROM <table> LIMIT <# of rows>; 
SELECT TOP <# of rows> <columns> FROM <table>; // MS SQL
```

ex:
```
SELECT * FROM books WHERE genre = "Fantasy" ORDER BY first_published ASC LIMIT 5;
```
This query retrieves only the top 5 results

## OFFSET Keyword | Paging Results

* OFFSET excludes the first set of records.
* OFFSET can only be used with an ORDER BY clause.
* OFFSET with FETCH NEXT returns a defined window of records.
* OFFSET with FETCH NEXT is great for building pagination support.

```
SELECT <columns> FROM <table> LIMIT <# of skipped rows>, <# of rows>;
SELECT <columns> FROM <table> LIMIT <# of rows> OFFSET <# of skipped rows>;

```
 ### MS SQL & MySQL
 ```
 SELECT <columns> FROM <table> OFFSET <skipped rows> ROWS FETCH NEXT <# of rows> ROWS ONLY;
 ```
 
 ex: `SELECT * FROM books ORDER BY title LIMIT 10 OFFSET 10;`
 This query retrieves all columns from the books table sorted by title and only displays 10 srtarting from book 11.
 
 ex: `SELECT * FROM reviews ORDER BY rating DESC LIMIT 3;`
 This query retrieves top 3 highest rating reviews
 
