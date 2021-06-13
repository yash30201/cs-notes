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

## 3 - Tier Architecture

