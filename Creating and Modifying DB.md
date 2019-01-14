# Creating and Modifying a Database
I'll be creating tables to hold information for a concert ticketing system

### Creating Tables
Lets create a concert table to store all the information about the concerts.

[Data Types](https://www.techonthenet.com/sql_server/datatypes.php):
* ID - small int
* DATE - (check date format)
* CITY - VARCHAR()
* STATE - VARCHAR()
* VENUE - VARCHAR()

```sql
CREATE TABLE CONCERTS(
  ID SMALLINT PRIMARY KEY,
  DATE DATE,
  CITY VARCHAR(50),
  STATE VARCHAR(50),
  VENUE VARCHAR(50)
 );
```

### Ticket Holders Table

```sql
CREATE TABLE TICKET_HOLDERS(
  ID INT PRIMARY KEY AUTOINCREMENT,
  FIRST_NAME VARCHAR(50),
  LAST_NAME VARCHAR(50),
  EMAIL VARCHAR(50)
);
```

### Tickets Table
Foreign Keys: A FOREIGN KEY is a key used to link two tables together and is a field (or collection of fields) in one table that refers to the PRIMARY KEY in another table.

The table containing the foreign key is called the child table, and the table containing the candidate key is called the referenced or parent table.

The **FOREIGN KEY constraint** is used to prevent actions that would destroy links between tables and also prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the table it points to.

```sql
CREATE TABLE TICKETS(
  ID INT PRIMARY KEY AUTOINCREMENT,
  CONCERT_ID SMALLINT REFRENCES CONCERTS(ID),
  TICKET_HOLDER_ID INT REFRENCES TICKET_HOLDERS(ID)
);
```
