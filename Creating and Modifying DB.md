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

