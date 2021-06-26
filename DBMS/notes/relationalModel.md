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

