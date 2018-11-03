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
