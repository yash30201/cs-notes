# Relational Model
<br>

## Introduction
<br>

### Terminologies
<br>

#### Relational model
Representation of data in the form of relations or tables

#### Relational Schema
Represents the structure of the relation

#### Relational Instance
Equivalent to Table

#### Domain of an attribute
The range of values which the attribute can possibly take. For eg, in AGE, the domain can be 18 to 45.

#### Tuple
Each row of a table is called tuple.

#### NULL values
The unknown, missing or undefined values of attribute of a tuple are represented by NULL.
> Two NULL values are considered different from each other in relation

<br>

---
<br>

## Relational Model
<br>

### Constraints in Relational Model
<br>

While defining the model, we define some constrains which are checked before performing any operation(like update, delete and insert). If there is a violation then the operation fails and nothing happens.

#### Domain Constraints
 > These are attribute level constrains
 They enforce the range of values the attribute can take.

#### Key integrity
Every relation in the database should have atleast one set of attributes which define the tuple/row uniquely.

+ It should be unique for all the tuples
+ It can't have NULL values

#### Referential integrity
Its the integrity between the relation between two attributes i.e. when one of the two can only take value available in the other.

Examples is abbreviation in one table and its full form in another...like
<br>

**STUDENT**

ROLL_NO | NAME | BRANCH_CODE
--- | --- | ---
953 | Yash | ECE

**BRANCH**

BRANCH_CODE | BRANCH_NAME
--- | ---
ECE | Electronics and communication engineering

Here the first table(STUDENT) is called `Referencing relation` and the second one(BRANCH) is called `Referenced relation`.

<br>

### Anomalies

These are the irregularities which arise when doing some operation in referenced relation's attribute. These are 

<br>

### Super Keys
These are the set of attributes that allows us to identify unique rows(tuples) in a given relation. Out of these keys, we can always choose a proper subset among these to be used at `primary key`. Such subsets are called `candidate keys`. If there is a combination of two or more attributes in primary key then we call it `composite key`.


<br>

---
<br>

## Types of keys in relational model
<br>

There are five terminologies related to keys - 

### Candidate Keys

It is the **minimial** set of attributes which can uniquely identify a tuple(*row*) in a relation(*table*).
+ There can be more than one candidate keys.
+ Its value is unique and not-null for every tuple.
+ It can be simple as well as composite.

> In sql server, `UNIQUE` differs from `PRIMARY KEY` because the former allows a null at most once but the latter has no possibility of being null.
<br>

### Super Key

Adding one or zero attributes to candidate keys generates super key. Each candidate key is a super key but the vice-versa is not true.

<br>

### Primary Key

One of the candidate keys can be chosen as primary key.
> Only one primary key exits in a relation

<br>

### Alternate Key

A chosen candidate key other than primary key is called alternate key.
> Only one alternate key **can** exits.

<br>

### Foreign Key

If an attribute can only take values which are present as values of some other attribute then it's called a foreign key.

> Referencing relation ---> Referenced relation

<br>

---
<br>

## Strategies for Schema designing
<br>

### Strategies

#### Top-down
In this, we start by defining the high level entities then going on creating new low level entities based on them. Entity relationship model is example to this.

#### Bottom-up
In this, we start by defining most fundamental entities and then go on creating new high level entities.

#### Inside-out strategy
This is a special case of bottom up strategy where sole focus is on creating some set of central entities and then expanding in the vicinity of these entities. Contrary to bottom up, where we just create all the fundamental entities as and when required, here we start by first creating all the entities which we deem as central.

#### Mixed strategy
Mixed = requirements are partitions according to top-down and then each part of this schema is designed according to bottom-up strategy.

<br>

---
<br>

## Schema integration 
<br>

It is a common practice in real-world scenarios where we design and develop different individual schemas and then integrate and merge them into one. This task is divided into following subtasks - 

### Identifying conflicts

There may occur the following types if conflicts - 

#### Naming conflict
Two types of naming conflicts may arise, *synonyms and homonyms* - 
+ Synonyms - Two entities with different names may represent same data(redundancy arise)
+ Homonyms - Same name represents different concepts.

#### Type conflicts
A type name in one schema can be some other concept apart from *type* in the other schema.

#### Domain Conflicts
Evident by name.

<br>

### Modifying views to conform to one another

Still independent modification done to as to comply with other schemas rules as closest as possible

<br>

### Merging and restructuring of views

The global schemas are created by merging these individual schemas.This is the hardest part in real-world databases and involve considerable amount og human intervention and negotiation to resolve conflicts to settle on most reasonable and acceptable solution.

> After this, restructuring can also be down to remove redundancies and any unnecessary complexity.

<br>

---
<br>

## 









