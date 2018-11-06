# Relational Databases
A relational database is a set of formally described tables from which data can be accessed or reassembled in many different ways without having to reorganize the database tables. The standard user and application programming interface (API) of a relational database is the Structured Query Language (SQL). SQL statements are used both for interactive queries for information from a relational database and for gathering data for reports.

#### Benefits
* Maxmizing Storage
* Batter Application Functionality
* Cleaner, Richer Data for Business Reporting

## Normalization
the process of restructuring a relational database in accordance with a series of so-called normal forms in order to reduce data redundancy and improve data integrity.

Explained further at this [link](https://www.studytonight.com/dbms/database-normalization.php)

## Set Theory
Set Theory was founded in 1874, and is a relatively new mathematical discipline, as compared to Algebra or Calculus.

[Introduction to Set Theory](https://www.mathsisfun.com/sets/)

Set theory is a branch of mathematical logic that studies sets, which informally are collections of objects. Although any type of object can be collected into a set, set theory is applied most often to objects that are relevant to mathematics. The language of set theory can be used in the definitions of nearly all mathematical objects. [Wikipedia](https://en.wikipedia.org/wiki/Set_theory)

* **SET**: A grouping of things with common properties
* **INTERSECT**: The overlapping of two sets
* **UNION**: Both sets together
* **Except**: Exclusive groups (Remove Union)

## Unique Keys
Keys are very important part of a Relational database model. They are used to establish and identify relationships between tables and also to uniquely identify any record or row of data inside a table. A Key can be a single attribute or a group of attributes, where the combination may act as a key.

#### Types of Keys
* Unique Keys: Specifically configured so that no value can be repeated within it
* Primary Keys: Can never be null and only one per table. Can't be modified. Cant be NULL.
* Foreign Keys: Foreign Keys are a column, or columns, that relate records back to the primary key in another table.

## One-to-Many Relationships
In a one-to-many relationship, one record in a table can be associated with one or more records in another table. For example, each customer can have many sales orders.

![one-to-many](https://fmhelp.filemaker.com/help/17/fmp/en/FMP_Help/images/relational.07.04.2.png)

In this example the primary key field in the Customers table, Customer ID, is designed to contain unique values. The foreign key field in the Orders table, Customer ID, is designed to allow multiple instances of the same value.

This relationship returns related records when the value in the Customer ID field in the Orders table is the same as the value in the Customer ID field in the Customers table.

* remember that the foreign key usually goes on the many side. This helps remember which key is in what table

### Many-to-Many Relationships
A many-to-many relationship refers to a relationship between tables in a database when a parent row in one table contains several child rows in the second table, and vice versa.

![many-to-many](https://fmhelp.filemaker.com/help/17/fmp/en/FMP_Help/images/relational.07.06.1.png)

A typical example of a many-to many relationship is one between students and classes. A student can register for many classes, and a class can include many students.

The following example includes a Students table, which contains a record for each student, and a Classes table, which contains a record for each class. A join table, Enrollments, creates two one-to-many relationships—one between each of the two tables.

The primary key Student ID uniquely identifies each student in the Students table. The primary key Class ID uniquely identifies each class in the Classes table. The Enrollments table contains the foreign keys Student ID and Class ID. [Source](https://fmhelp.filemaker.com/help/17/fmp/en/index.html#page/FMP_Help%2Fmany-to-many-relationships.html%23)


## One-to-One Relationship
A one-to-one relationship in a relational database occurs when one parent record or field has either zero or one child record only. These relationships are the easiest to represent in databases because both the parent and child records may be in the same table.

## Join Queries
A JOIN clause is used to combine rows from two or more tables, based on a related column between them.

![Join](https://image-proxy-cdn.teamtreehouse.com/8e4d3514a77b2bf0f9f8db0f065f86bfa136919a/687474703a2f2f74726565686f7573652d70726f6a6563742d646f776e6c6f6164732e73332e616d617a6f6e6177732e636f6d2f5175657279696e6752656c6174696f6e616c4461746162617365732f636f6d706c65785f76656e6e2e706e67)

#### Inner Join
The INNER JOIN keyword selects records that have matching values in both tables. Most common SQL Join

```
SELECT <columns> 
  FROM <table1> 
  INNER JOIN <table2> ON <equality criteria> 
  WHERE <search criteria>
```

ex: Retrieve all Chevy models using make and model tables
```SQL
SELECT mk.MakeName, md.ModelName 
  FROM make AS mk 
  INNER JOIN model AS md ON mk.MakeID = md.MakeID
  WHERE mk.MakeName = "Chevy";
```
retrieves the MakeName from the make table, ModelName FROM the make table aliased as mk and model table aliased as md when the mk.MakeID from Make table matches the md.MakeID from the Model table amd returns only the ones where NameName = "chevy"

### Outer Join
An outer join, unmatched rows in one or both tables can be returned. There are a few types of outer joins:

* LEFT JOIN returns only unmatched rows from the left table.
* RIGHT JOIN returns only unmatched rows from the right table.
* FULL OUTER JOIN returns unmatched rows from both tables.

```
SELECT <columns> 
  FROM <table1>
  LEFT OUTER JOIN <table2> ON <equality criteria>
  WHERE <search criteria>...
```

![Joins Chart](https://community.modeanalytics.com/images/intermediate/visual-join.png)

```SQL
SELECT mk.MakeID, COUNT(md.ModelID) AS NumberOfModels FROM make AS mk
  LEFT OUTER JOIN model AS md ON.mk.MakeID = md.ModelID
  GROUP BY mk.MakeName;
```

![SQL Joins](https://image-proxy-cdn.teamtreehouse.com/3e9f9c2f5849959e5f2f01e71c16542b4999ae89/687474703a2f2f7777772e636f646570726f6a6563742e636f6d2f4b422f64617461626173652f56697375616c5f53514c5f4a6f696e732f56697375616c5f53514c5f4a4f494e535f6f7269672e6a7067)

## Join Exercises: using books, loans and patrons tables

* Use a JOIN to select all patrons with outstanding books. Select their first name and email address. (i've also included a couple extra columns for verification)
 * Use a JOIN to find out which patrons haven't had any loans. Select their first name and email address.
 * Create a report that shows the title of the book, first and last name of the patron, email and all date fields of the loan.

```SQL
SELECT patrons.first_name, patrons.email, loans.return_by, loans.returned_on
  	FROM patrons
  	INNER JOIN loans ON patrons.id = loans.patron_id
  	WHERE loans.return_by < DATE("NOW") AND returned_on IS NULL
  	GROUP BY patrons.first_name;
  
SELECT patrons.first_name, patrons.email
  	FROM patrons
  	LEFT OUTER JOIN loans ON patrons.id = loans.patron_id
  	WHERE loans.patron_id IS NULL;
  
SELECT books.title, patrons.first_name || " " || patrons.last_name AS full_name, patrons.email, loans.loaned_on, loans.return_by, loans.returned_on
  	FROM patrons
  	INNER JOIN loans ON patrons.id = loans.patron_id
  	INNER JOIN books ON loans.book_id = books.id
  	WHERE books.id = loans.book_id;
```

## MORE EXERCISES W/ JOIN

* In a car database there is a Model table with columns, ModelID, MakeID and ModelName and a Car table with columns, CarID, ModelID, VIN, ModelYear and StickerPrice. For all cars in the database, show Model Name, VIN and Sticker Price in one result set.
* In a car database there is a Make table with columns, MakeID and MakeName, a Model table with columns, ModelID, MakeID and ModelName and a Car table with columns, CarID, ModelID, VIN, ModelYear and StickerPrice. For all cars in the database, show Make Name, Model Name, VIN and Sticker Price from the Model and Car tables in one result set.
* In a car database there is a Sale table with columns, SaleID, CarID, CustomerID, LocationID, SalesRepID, SaleAmount and SaleDate. The database also has a SalesRep table with columns, SalesRepID, FirstName, LastName, SSN, PhoneNumber, StreetAddress, City, State and ZipCode. Show the First and Last Name of each sales rep along with SaleAmount from both the SalesRep and Sale tables in one result set.
* In a car database there is a Model table with columns, ModelID, MakeID and ModelName and a Car table with columns, CarID, ModelID, VIN, ModelYear and StickerPrice. Show all Model names from the Model table along with VIN from the Car table. Make sure models that aren’t in the Car table still show in the results!
* In a car database there is a Sale table with columns, SaleID, CarID, CustomerID, LocationID, SalesRepID, SaleAmount and SaleDate. The database also has a SalesRep table with columns, SalesRepID, FirstName, LastName, SSN, PhoneNumber, StreetAddress, City, State and ZipCode. Show all SaleDate, SaleAmount, and SalesRep First and Last name from Sale and SalesRep. Make sure that all Sales appear in results even if there is no SalesRep associated to the sale.
```SQL
SELECT m.ModelName, c.VIN, c.StickerPrice
	FROM model AS m
  	INNER JOIN car AS c ON m.modelID = c.ModelID;
  
 SELECT Make.MakeName, Model.ModelName, Car.VIN, Car.StickerPrice
	FROM Make
    	INNER JOIN Model ON Make.MakeID = Model.MakeID
    	INNER JOIN Car ON Model.ModelID = Car.ModelID;
    
 SELECT SalesRep.FirstName, SalesRep.LastName, Sale.SaleAmount
 	FROM SalesRep
    	INNER JOIN Sale ON SalesRep.SalesRepID = Sale.SalesRepID; 
	
SELECT Model.ModelName, Car.VIN
	FROM Model
  	LEFT OUTER JOIN car ON Model.ModelID = Car.ModelID;
	
SELECT Sale.SaleDate, Sale.SaleAmount, SalesRep.FirstName, SalesRep.LastName
	FROM Sale
  	LEFT OUTER JOIN SalesRep ON Sale.SalesRepID = SalesRep.SalesRepID;
```

## SET Operations

#### UNION
The UNION operator is used to combine the result-set of two or more SELECT statements.
The UNION operator selects only distinct values by default. 
* Each SELECT statement within UNION must have the same number of columns
* The columns must also have similar data types
* The columns in each SELECT statement must also be in the same order

```
SELECT <column name(s)> FROM <table1>
UNION
SELECT <column name(s)> FROM <table2> 
```

#### UNION ALL
Like UNION but allows duplicates

```
SELECT <column name(s)> FROM <table1>
UNION ALL
SELECT <column name(s)> FROM <table2> 
```

#### INTERECT
The SQL INTERSECT operator is used to return the results of 2 or more SELECT statements. However, it only returns the rows selected by all queries or data sets. If a record exists in one query and not in the other, it will be omitted from the INTERSECT results.

```
SELECT <column(s) FROM <table1>
WHERE <condition>
INTERSECT
SELECT <column(s) FROM <table2>
WHERE <condition>
```

#### EXCEPT
The SQL EXCEPT clause/operator is used to combine two SELECT statements and returns rows from the first SELECT statement that are not returned by the second SELECT statement. This means EXCEPT returns only rows, which are not available in the second SELECT statement.

```
SELECT <column(s) FROM <table1>
WHERE <condition>
EXCEPT
SELECT <column(s) FROM <table2>
WHERE <condition>
```

## SET Operation Exercises | Using Library DB

* Create a list of all books in both north and south locations
* Create a list of unique books. Books that are in the north or south location, but not in both locations.
* Create a list of duplicate books. Book titles that exist in BOTH north AND south locations
* 

```SQL
SELECT * FROM books_north
	UNION ALL
	SELECT * FROM books_south
	ORDER BY title;
	
SELECT title FROM books_north
	UNION
	SELECT title FROM books_south
	ORDER BY title;
	
SELECT title FROM books_north
	INTERSECT
	SELECT title FROM books_south
	ORDER BY title;
```

* There are two tables Fruit and Vegetable table. The Fruit table has a FruitID and a Name column and the Vegetable table has a VegetableID and Name column. Create a distinct result set of fruit and vegetable names.
* Create a list of all fruits and vegetables starting with the letters A through K . In other words all fruit and vegetables that don't start with the letter L to Z.
* Create a list of fruits and vegetables that includes any potential duplicate values. Ensure that it is in alphabetical order so that the duplicates are next to each other!
* Create an alphabetical list of produce that is considered both a fruit and a vegetable.
* Create an alphabetical list of fruits that are NOT considered a vegetable.
* Create an alphabetical list of vegetables that are NOT considered a fruit.

```SQL
SELECT Name FROM Fruit 
	UNION 
	SELECT Name FROM Vegetable;

SELECT Name FROM Fruit 
	WHERE Name < "L" 
	UNION 
	SELECT Name FROM Vegetable 
	WHERE Name < "L";
	
SELECT Name FROM Fruit
	UNION ALL
	SELECT Name FROM Vegetable
	ORDER BY Name;
	
SELECT Name FROM Fruit
	INTERSECT 
  	SELECT Name FROM Vegetable
  	ORDER BY Name;
	
SELECT Name FROM Fruit
	INTERSECT 
  	SELECT Name FROM Vegetable
  	ORDER BY Name;
	
SELECT Name FROM Vegetable
	INTERSECT 
  	SELECT Name FROM Fruit
  	ORDER BY Name;
```

## Subquieries (Derived Table)
 Subquery or Inner query or a Nested query is a query within another SQL query and embedded within the WHERE clause.

A subquery is used to return data that will be used in the main query as a condition to further restrict the data to be retrieved.

Subqueries can be used with the SELECT, INSERT, UPDATE, and DELETE statements along with the operators like =, <, >, >=, <=, IN, BETWEEN, etc.

There are a few rules that subqueries must follow:

* Subqueries must be enclosed within parentheses.
* A subquery can have only one column in the SELECT clause, unless multiple columns are in the main query for the subquery to compare its selected columns.
* An ORDER BY command cannot be used in a subquery, although the main query can use an ORDER BY. The GROUP BY command can be used to perform the same function as the ORDER BY in a subquery.
* Subqueries that return more than one row can only be used with multiple value operators such as the IN operator.
* The SELECT list cannot include any references to values that evaluate to a BLOB, ARRAY, CLOB, or NCLOB.
* A subquery cannot be immediately enclosed in a set function.
* The BETWEEN operator cannot be used with a subquery. However, the BETWEEN operator can be used within the subquery.

```
SELECT <Columns>
 FROM <Table1>
 WHERE Column1 IN (
  SELECT Column1
  FROM <Table2>
  WHERE <search criteria>
);
```

```
SELECT <Columns>
FROM <table>
<INNER | OUTER> JOIN
(SELECT <columns> FROM Mtable> WHERE <Search criteria>) AS <Alias>
ON <Join Criteria>
```

ex: All sales w/ 2015 Model
```SQL
SELECT * FROM Sale 
	WHERE CarID IN (
	SELECT CarID FROM Car WHERE ModelYear = 2015
	);
	
// OR w/ Derived Table

SELECT * FROM Sale AS s
	INNER JOIN (SELECT CarID FROM Car WHERE ModelYear = 2015) AS t
	ON s.CarID = t.CarID;
```
ex: Get a list of user's names and emails for users who have spent over 100 dollars in a single transaction.
```SQL
SELECT name, email FROM users 
    WHERE id IN (SELECT DISTINCT(user_id) FROM sales WHERE saleAmount > 100);
    // OR w/ Derived Table
 SELECT name, email FROM users
    INNER JOIN (SELECT DISTINCT(user_id) FROM sales WHERE saleAmount > 100) AS best_customers
    ON users.id = best_customers.user_id; 
```

ex: Sum of all sales by rep and location
```SQL
 SELECT sr.LastName, Loc1.StLouisAmount, Loc2.ColumbiaAmount FROM SalesRep AS sr
 	LEFT OUTER JOIN (
		SELECT SalesRepID, SUM(SaleAmount) AS StLouisAmount
		FROM Sale AS s WHERE s.LocationID = 1
	) AS Loc1 ON sr.SalesRepID = Loc1.SalesRepID
	LEFT OUTER JOIN (
		SELECT SalesRepID, SUM(SaleAmount) AS ColumbiaAmount
		FROM Sale AS s WHERE s.locationID = 2
		GROUP BY SalesRepID
	) AS Loc2 ON sr.SalesRepID = Loc2.SalesRepID;
```

## SubQueries Exercises
In a car database there is a Model table with columns, ModelID, MakeID and ModelName and a Car table with columns, CarID, ModelID, VIN, ModelYear and StickerPrice.

* Use a subquery along with IN to list all the Model Names with a Sticker Price greater than $30000
* Use a subquery along with IN to list all sales of cars with Sticker Price greater than $30000. Include all columns.
* In a car database there is a Sale table with columns, SaleID, CarID, CustomerID, LocationID, SalesRepID, SaleAmount and SaleDate and a Customer table with columns, CustomerID, FirstName, LastName, Gender and SSN. Use a subquery along with IN to list all sales to female customers. (Gender = 'F') Select all columns.
* Use a subquery as a derived table to show all sales to female ('F') customers. Select all columns from the Sale table only.

```
SELECT ModelName FROM Model 
	WHERE ModelID IN (SELECT ModelID FROM Car WHERE StickerPrice > 30000);

SELECT * FROM Sale 
	WHERE CarID IN (SELECT CarID FROM Car WHERE StickerPrice > 30000);
	
SELECT * FROM Sale 
	WHERE CustomerID IN (SELECT CustomerID FROM Customer WHERE Gender = "F");

SELECT * FROM Sale 
	INNER JOIN (SELECT CustomerID FROM Customer WHERE gender = "F") AS female_customers
  ON female_customers.CustomerID = Sale.CustomerID;
```
