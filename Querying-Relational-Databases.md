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
SELECT <columns> FROM <table1> INNER JOIN <table2> ON <equality criteria> WHERE <search criteria>
```

ex: Retrieve all Chevy models using make and model tables
```
SELECT mk.MakeName, md.ModelName FROM make AS mk 
  INNER JOIN model AS md ON mk.MakeID = md.MakeID
  WHERE mk.MakeName = "Chevy";
```
retrieves the MakeName from the make table, ModelName FROM the make table aliased as mk and model table aliased as md when the mk.MakeID from Make table matches the md.MakeID from the Model table amd returns only the ones where NameName = "chevy"

### Outer Join
An outer join, unmatched rows in one or both tables can be returned. There are a few types of outer joins:

* LEFT JOIN returns only unmatched rows from the left table.
* RIGHT JOIN returns only unmatched rows from the right table.
* FULL OUTER JOIN returns unmatched rows from both tables.

![Joins Chart](https://community.modeanalytics.com/images/intermediate/visual-join.png)


