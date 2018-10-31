# Reporting Text
Manipulating text results with functions

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
 
## FUNCTIONS
Can manipulate the results of a query in diffrent ways and can be used in one or more parts of a query 

*Definitions to remember
* Keywords: Commands issued to a database. The data presented in queries is unaltered.
* Operators: Performs comparisons and simple manipulation
* Functions: Presents data differently through more complex manipulation

```
<function name>(<value or column>)
```
ex `UPPER("Horge")` = "HORGE"

## CONCAT FUNCTION CONCAT()
Joins columns together

```
SELECT CONCAT(<value or column>, <value or column>, <value or column>) FROM <table>;
```
ex: `SELECT CONCAT(first_name, " ", last_name) AS "Full Name" FROM customers;`
query retrieves the concatinated result of first_name and last_name as a whole stringaliased as "Full Name"

## LENGTH function
returns int length of string

```
SELECT LENGTH(<value or column>) FROM <tables>;
```

ex:
```
SELECT username, LENGTH(username) AS "Length of Name" FROM customers
ORDER BY "Length of Name" DESC
LIMIT 1;
```
returns the int length of the longest username string in the customers table.

ex: `SELECT username AS length FROM customers WHERE LENGTH(username) < 7`
returns all usernames who length is less than 7.

## TEXT CASE Functions
Changes the case of a string

Could be used to check against case insensitivity
```
SELECT UPPER(<value or column>) FROM <table>;
SELECT LOWER(<value or column>) FROM <table>;
```
ex: `SELECT UPPER(zip) FROM addresses WHERE country = "UK";`
retreives all zip codes from the address table where country is equal to "UK", zips are in all UPPER case

## EXCERPTS From Text
create smaller strings from larger piece of text you can use the SUBSTR() funciton or the substring function.

```
SELECT SUBSTR(<value or column>, <start>, <length>) FROM <table>;
```

ex: `SELECT SUBSTR(first_name, 1, 1) AS initial, last_name FROM customers;`
retrieves the first initial and last name from the customers table.

## REPLACING text
replaces peiece of a string or text in a larger body of text using the REPLACE() function

```
SELECT REPLACE(<original value or column>, <target string>, <replacement string>) FROM <table>;
```

ex: `SELECT REPLACE(email, "@", "<at>") AS obfuscated_email FROM customers;`
returns the email string with the "@" symbol replcaed by "<at>" to look like 'email<at>gmail.com


## REPORTING TEXT PRACTICE QUERIES
ex:
-- Find the actor with the longest name
-- Add the username after the review. e.g. "That was a cool movie - Horge"
-- Uppercase all movie titles
--- In all of the reviews, replace the text "public relations" with "PR"
--- From the actors, truncate names greater than 10 charactor with ... e.g. William Wo...
```
SELECT name FROM actors ORDER BY LENGTH(name) DESC LIMIT 1;
SELECT review || " - " || username FROM reviews;
SELECT UPPER(title) FROM movies;
SELECT REPLACE(review, "public relations", "PR") FROM reviews;
SELECT REPLACE(name, SUBSTR(name, 10, 15), "...") AS truncated 
  FROM actors 
  WHERE LENGTH(name) > 10;
```

# Reporting Numbers
Manipulating numeric reults with functions

## COUNT() Function
COUNT() function is used to count non NULL rows
It can also be used to count unique entries using the *DISTINCT* keyword

```
SELECT (*) FROM <table>;
SELECT COUNT(DISTINCT<column>) FROM <table>;
```

ex:
* Retreive count of books with sci-fi genre and alias the count
* Count the amount of books by J.K. Rowling in the books table, alias the count
```
SELECT COUNT(genre) AS scifi_book_count FROM books WHERE genre = "Science Fiction";
SELECT COUNT(author) AS jk_book_count FROM books WHERE author = "J>K> Rowling";
```

## Counting Groups of Rows | GROUP BY Keyword
The GROUP BY statement is often used with aggregate functions (COUNT, MAX, MIN, SUM, AVG) to group the result-set by one or more columns.

```
SELECT <column> FROM <table> GROUP BY <column with comon value>;
```

ex: Using the Library Database
* Count all books in each genre. Include the genre column first and genre_count as second column of information. USe the books table
* Query to count all UNIQUE genres in the books table. Aliase to total_genres
```
SELECT genre, COUNT(*) AS genre_count FROM books GROUP BY genre;
SELECT COUNT(DISTINCT genre) AS total_genres FROM books;
```
