# Introduction

## Introduction of DBMS

### Database 
Database is a collection of inter-related data which helps in efficient retrieval, insertion, update and deletion of data from database and allows us to organise data in tables,views,schemas,reports, etc.

<br>

### DDL (Data Definition Language)
Deals with database schemas and descriptions. Example : 
+ CREATE
+ ALTER
+ DROP
+ TRUNCATE - *removes all the records from the structure*
+ COMMENT
+ RENAME

<br>

### DML (Data Manipulation Language)
Deals with the data manipulation and is used to store, modify, retrieve, delete and update data in already defined database
+ SELECT
+ INSERT
+ UPDATE
+ DELETE
+ MERGE
+ CALL
+ EXPLAIN PLAN - *Interpretation of the data access path*
+ LOCK TABLE - *Concurrency control*

<br>

### DBMS
Software user to manage a database of called DBMS. It allows the following tasks : 
#### Data Definition
Helps in creation, modification and removal of definition of data in the organisation of the data in database.
#### Data update
Helps in insertion, modification of deletion of actual data in the database.
#### Data Retrieval
Helps in retrieving data
#### User Administration
Concurrency control, Error handling, registering and monitoring users, data security, data integrating and monitoring performance

<br>

### Problems with file system
Let us take the example of my college
+ Redundancy of data - Mera ek hi phone number har jagah baar baar likha hota hai
+ Inconsistency of data - Admin office me and hostel me alag alag number hona
+ Difficult data access 
    + Meko office ka exact location cahiye enquiry karne ke liye
    + Ek file me mere details khojne ke liye hazaaro panne khojne padenge
+ Unauthorized access - agar test file mil gayi..to bas...dassi pakki
+ No concurrent access - Ek baar me ek hi ko answer sheet dikhate 
+ No Backup and recovery - agar file ghum gayi to kaam khatam

---

## 3 - Tier ~~Architecture~~ Model in DBMS

### DBMS 3-Tier ~~Architecture~~ Model

Here, database is divided into three interrelated + independent modules

**Physical Level** <--------> **Conceptual Level** <----------> **External Level**

> The first two boast physical data independence while latter two boast logical data independence

#### Physical Level
At this level, info about the location of database objects in the physical data store is kept.

#### Conceptual Level
At conceptual level, data is stored in various interrelated data collections/tables - Complete data is stored here in logical+conceptual form.

#### External Level
This offers different views of the data in terms of conceptual level data tables. This level caters to the specific needs of the user requiring data.

<br>

### Data abstraction

DBMS comprises of complex data-structures. In order to make system efficient in terms of data retrieval and to reduce complexity in terms of usability of users, abstraction is user, i.e irrelevant details are hidden from the users. 

> The main purpose of data abstraction is to achieve data independence

It simplifies dbms design. There are 3 levels of abstraction.

#### Physical
Lowest level of data abstraction. Access methods (sequential or random access), object organisation methods(B+ trees, hashing, etc), size of memory are only needed while designing the database and this are hidden from users.
#### Logical 
Here, the information available to the user in view level is unknown and its only task is to serve the external view level.
#### View
This is the highest level of abstraction. Only a part of the actual database is shows to the users in the form of rows and columns. Users can interact with the database via methods but storage and implementation details are hidden from them

<br>

### Data independence

This means change at one level of the architecture should not affect another level. 

#### Physical Date Independence
Change in physical location of data should not affect conceptual level or external view, i.e., changing data structures used for hashing, indexing methods or size of server should not affect conceptual/logical structure. Its easy to achieve

#### Conceptual Data Independence
Change in conceptual schema should not affect external view. This is hard to achieve as changes in conceptual schema are reflected in the user's view.

<br>

### Phases of database design

There are four phases of database designing - 

+ Requirements : *Gather requirements of the database*
+ Conceptual Design : *Requirements of database are captured using high level conceptual data model. For eg: ER model*
+ Logical Design : *Data is represented in logical form. For eg : ER diagram is generated from ER model to signify logical relations*
+ Physical Design : *Implementation using DBMS like oracle, DB2, MySQL, MongoDB*

<br>

### Advantages of DBMS

Opposite of all the points in [problems in file system](#Problems-with-file-system) and :
+ Object management instead of file management
+ Multiple data views
+ Query processing
+ Efficient memory management and indexing - fast retrieval due to indexing
+ Transaction management(linked with concurrency control) - ACID Implemented and maintained
+ Easy searching
+ Data integrity constraints - *like this field is necessary types..*
+ Multiple user interfaces
+ Data scalability, expandability and flexibility
+ Security and access control for every single part of data.
---

## DBMS Architecture 2-Level vs 3 Level

### 2-tier architecture

This is a basic client - server architecture. Client side handles UI and application programs whereas server side handles query processing and transaction management.

Advantage > easy maintenance and understanding

Disadvantage > Poor performance incase of large number of users

<br>

### 3-Tier architecture

There comes another layer between client and server to act as a medium.

Advantage > Enhanced scalability, data integrity(since data corruption is removed) and improved security

Disadvantage > More implementation complexity

---

## Database objects in DBMS

### Database object

It is any defined object which is used to store / reference data. *Anything we create using `CREATE` command is knows as database object. Some examples - 

#### Table
This is basic storage unit. Composed of rows and columns.
```sql
CREATE TABLE tableName
(
    fieldName1 variableType(defaultValue),
    fieldName2 variableType(defaultValue),
    fieldName3 variableType(defaultValue)
);
```

#### View
This creates a view bases on another table/view. The tables on which a view is based is called `base tables`
```sql
CREATE VIEW viewName
AS SELECT originalFieldName1 aliasFieldName1, originalFieldName2 aliasFieldName2
-- for examples employee_id ID_NUMBER, last_name NAME, salary*12 ANN_SALARY
FROM employees
WHERE department_id = 50;
```

#### Sequence
This is used to create a sequence (database object) in database.
```sql
CREATE SEQUENCE dept_deptId_seq
        INCREMENT BY 10
        START WITH 120
        MAXVALUE 9999
        NOCACHE
        NOCYCLE;
```

#### Index
Creates a database schema object which allows fast retrieval of rows using pointers. If index on a column is absent then a full table scan occurs. It decreases the I/O by using an indexed path to locate data quickly.
```sql
CREATE INDEX indexName
ON  tableName(fieldName);
```

#### Synonym
This allows us to create alias to access objects. Used when object to access have very length names.
```sql
CREATE SYNONYM synonymName FOR objectName;
```

---

## Multimedia Database

Read the [article](https://www.geeksforgeeks.org/multimedia-database/) itself in geeks if you have time otherwise skip this

---

## Use of DBMS in system software

> > > > To start from here
