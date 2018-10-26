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
