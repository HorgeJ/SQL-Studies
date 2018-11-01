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

## The Grand Total | SUM Function
The SUM() function returns the total sum of a numeric column.
The HAVING clause was added to SQL because the WHERE keyword could not be used with aggregate functions. (like WHERE keyword)

```
SELECT SUM(<numeric column>) FROM <table>;
SELECT SUM(<numeric column>) AS <alias> FROM <table>
                                        GROUP BY <another column>
                                        HAVING <alias> <operator> <value>;
```

ex: Using Orders table
* Find the customers who have spent more than $250
```
SELECT SUM(cost) AS total_spend, user_id FROM orders
                                         GROUP BY user_id
                                         HAVING total_spend > 250
                                         ORDER BY total_spend DESC
```

ex: Using Movie database
* Write a query that totals up all ratings for the movie "Starman" (id = 6) in the reviews table and alias it.

```
SELECT SUM(rating) AS starman_total_ratings FROM reviews WHERE movie_id = 6;
```

## Calculating Averages | AVG() Function
The AVG() function returns the average value of a numeric column.

```
SELECT AVG(<numeric column>) FROM <table>;
SELECT AVG(<numeric column>) FROM <table> GROUP BY <another column>;
```

ex:
* Retrieve the average spend per customer and order from highest to lowest
```
SELECT AVG(cost) AS average, user_id FROM orders GROUP BY user_id ORDER BY average DESC;
```
ex:
* retrieve the average rating for "Starman"
```
SELECT AVG(rating) AS average_rating FROM reviews WHERE movie_id = 6;
```

## MIN and MAX values | MAX() & MIN()
The MIN() function returns the smallest value of the selected column.
The MAX() function returns the largest value of the selected column.

```
SELECT MAX(<numeric column>) FROM <table>;
SELECT MAX(<numeric column>) FROM <table> GROUP BY <other column>;

SELECT MIN(<numeric column>) FROM <table>;
SELECT MIN(<numeric column>) FROM <table> GROUP BY <other column>;
```
ex: Using reviews table
* Calculate the minimum and max of the starman ratings
```
SELECT MIN(rating) AS star_min, MAX(rating) AS star_max FROM reviews WHERE movie_id = 6;
```

## Arithmetic on Numeric Types | * / + -

* `*` Multiply
* `/` Divide
* `+` Add
* `-` Subtract

```
SELECT <numeric column> <arithmetic  operator> <numeric value> FROM <table>;
```

The ROUND() function rounds a number to a specified number of decimal places.
```
SELECT ROUND(<decimal value>, <number of decimal places>) AS <alias>;
```
ex: Using a products table
* Write a query that returns the product name and price in Pounds Sterling (GBP). The current exchange rate is 1.4 USD to every 1 GBP. Alias the calculated price to price_gbp. Round to two decimal places.

```
SELECT name, ROUND(price / 1.4, 2) AS price_gbp FROM products;
```

## EXAMPLES [Using Actors, Movies and Reviews tables]

* Count all the movies in the Musical genre
* Calculate the average rating given by a user across all movies
* Calculate the average rating for each movie and round it to one decimal place
* Calculate the minimum and maximum rating for every movie
```
SELECT COUNT(*) FROM movies;
SELECT AVG(rating) AS avg_user_rating, username FROM reviews GROUP BY username;
SELECT ROUND(AVG(rating),1) AS avg_movie_rating, username FROM reviews GROUP BY movie_id;
SELECT MIN(rating) AS min_rating, MAX(rating) AS max_rating, movie_id FROM reviews GROUP BY movie_id;
```

# DATES | Principles
Different SQL databeses handle dates differently. Refer to your version of SQL's documentation for more information.

## Todays Date and Time
Various ways to work with current date and time in on different databases

### MS SQL
* Current Date: `CONVERT(date, GETDATE())`
* Current Time: `CONVERT(time, GETTIME())`
* Current date time: `GETDATE();`

### SQLite
* Current Date: `DATE("NOW")`
* Current Time: `TIME("NOW")`
* Current date time: `DATETIME("NOW")`

### MySQL
* Current Date: `CURDATE()`
* Current Time: `CURTIME()`
* Current date time: `NOW()`

ex: get all orders placed on todays date
```
SELECT * FROM orders WHERE status = "placed" AND ordered_on = DATE("NOW")
```
