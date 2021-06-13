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

## 3 - Tier Architecture in DBMS

### DBMS 3-Tier Architecture

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

### Data independence

This means change at one level of the architecture should not affect another level.

#### Physical Date Independence
Change in physical location of data should not affect conceptual level or external view. Its easy to achieve

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
+  Multiple data views

---


