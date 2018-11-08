# SQL Reporting Examples

### Reports will be made by querying a middle schools database with 7 tables for Students table, Teachers table, Subjects table, Rooms table, Periods table, Classes table, Schedule table.

**STUDENTS TABLE
```
CREATE TABLE STUDENTS (
    ID INT PRIMARY KEY,
    FIRST_NAME TEXT,
    LAST_NAME TEXT,
    GRADE INT
)
```

**TEACHERS TABLE
```
CREATE TABLE TEACHERS (
    ID INT PRIMARY KEY,
    FIRST_NAME TEXT,
    LAST_NAME TEXT,
)
```

**SUBJECTS TABLE
```
CREATE TABLE SUBJECTS (
    ID INT PRIMARY KEY,
    NAME TEXT,
    GRADE TEXT,
    DESCRIPTION TEXT
)
```

**ROOMS TABLE
```
CREATE TABLE ROOMS (
    ID INT PRIMARY KEY,
    CAPACITY INT
)
```

**PERIODS TABLE
```
CREATE TABLE PERIODS (
    ID INT PRIMARY KEY,
    START_TIME TEXT,
    DURATION INT
)
```

**CLASSES TABLE
```
CREATE TABLE TEACHERS (
    ID INT PRIMARY KEY,
    SUBJECT_ID INT,
    PERIOD_ID INT,
    TEACHER_ID INT,
    ROOM_ID INT,
    FOREIGN KEY(SUBJECT_ID) REFRENCES SUBJECTS(ID),
    FOREIGN KEY(PERIOD_ID) REFRENCES PERIODS(ID),
    FOREIGN KEY(TEACHER_ID) REFRENCES TEACHERS(ID),
    FOREIGN KEY(ROOM_ID) REFRENCES ROOMS(ID)
)
```

**SCHEDULE TABLE
```
CREATE TABLE SCHEDULE (
    ID INT PRIMARY KEY,
    STUDENT_ID INT,
    FOREIGN KEY(CLASS_ID) REFRENCES CLASSES(ID),
    FOREIGN KEY(STUDENT_ID) REFRENCES STUDENTS(ID)
)
```

* Which subjects are taught at the middle school?
```SQL
SELECT * FROM SUBJECTS;
```

* How many students do they have at the middle school?
```SQL
SELECT COUNT(*) FROM STUDENTS;
```

* What's Yvette Levy's student ID number?
```SQL
SELECT ID FROM STUDENTS 
WHERE FIRST_NAME = "Yvette" 
AND LAST_NAME = "Levy";
```

* Generate a list of teachers sorted alphabetically by last name.
```SQL
SELECT FIRST_NAME, LAST_NAME FROM TEACHERS
ORDER BY LAST_NAME ASC;
```

* Which students have last names starting with 'A'?
```SQL
SELECT ID, FIRST_NAME, LAST_NAME FROM STUDENTS
WHERE LAST_NAME LIKE 'A%';
```

* What's the total capacity of the school?
```SQL
SELECT SUM(CAPACITY)AS School_Capacity FROM ROOMS;
```

* Which room has the largest capacity?
```SQL 
SELECT SUM(CAPACITY)AS School_Capacity FROM ROOMS;
```

