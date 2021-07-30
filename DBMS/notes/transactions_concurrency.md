# Transactions and Concurrency Control

<br>

## Introduction
<br>

Transaction = set of logically related operations. They consists of -
+ Read(A)
+ Write(A)

**Commit** : When the changes are put permanently in DB after the transaction completes

**Rollback** : When the changes made by transactions are undone

<br>

---
<br>

## ACID Properties in DBMS

A transaction should follow certain properties in order to be consistent. These are called **A**tomicity, **C**onsistency, **I**solation and **D**urable.

### Atomicity
<br>

This implies that a transaction either takes place at once or doesn't takes place at all. There is no midway => they don't occur partially. Hence here, two operations are used - 
<br>

**Abort** : evident by name
**Commit** : evident by name

<br>

### Consistency 
<br>

This means that integrity constrains must be maintained so that DB is consistent after the transaction.

For eg, Account balance and debited sheet sum should be constant under the condition that no credit happens.

<br>

### Isolation

This ensures that multiple transactions can occur concurrently without leading to the inconsistency. Changes occurring in a particular transaction will not be visible to any other transactions.

<br>

### Durability

This ensures that once the transaction has completed its execution, the updates and modifications are stored in and written to non volatile memory...i.e. disk from RAM.

<br>

---
<br>

## Types of Schedules in DBMS
<br>

### Serial Schedules
 
Schedules in which transactions are executed in independent/ non-interleaved manner. In short, no other schedule start until current schedules completes its execution.

### Non-Serial Schedules

They are the schedules where the operations of multiple transactions are interleaved thus leading to concurrency(=> concurrent execution of multiple transactions)

Non-serial schedules can be further classified into serialisable and non-serialisable.

<br>

---
<br>

## Conflict serialisability
<br>

### Conflicting operations

+ R<sub>1</sub>(A) , W<sub>2</sub>(A)
+ W<sub>1</sub>(A) , R<sub>2</sub>(A)
+ W<sub>1</sub>(A) , W<sub>2</sub>(A)

For operations to be conflicting, they should belong to different transactions and should operate on same data item.

### Conversion to conflict serialisable

Given an interleaving to two transactions, swap non conflicting operations to convert it to the form T1->T2 or T2->T1.

<br>

---
<br>

## View serialisability
<br>

Conditions for two schedule to be view equal to each other are - 

Let the schedules be S1 and S2. Then

+ **Initial read** : If a transaction T1 reads data object A in S1, then in S2 also T1 should read it.
+ **Update Read** : If object a is read and then updated by Ti and Tj respectively in S1, then in S2 also these two should do the same.
+ **Final Write Operation** : The final write for any data object in both the schedules should be done by same transaction in both of them.

<br>

---
<br>


## Serialisable Schedules (in non-serial schedules)
<br>

They are of two types, conflict serialisable and view serialisable.

### Conflict Serialisable

It means that the transactions operations can be transformed into serial schedule(of operations, not transactions) by swapping non-conflicting operations.

### View Serialisable

If a schedule is view equal to a serial schedule, then Its called view serialisable. A conflict schedule is view serialisable schedule but vice versa may not be true.

<br>

---
<br>

## Non-Serialisable schedules
<br>

These are further divided into recoverable and non-recoverable types.

### Recoverable Schedules

Recoverable schedules are classified into three different types in increasing strictness, Cascading < Cascadeless < Strict

#### Cascading schedule

Here dirty read is allowed, which results in complete schedule chain rollback if parent schedule aborts.

#### Cascadeless schedule

Here, a data item is read only when its previous write is committed thus resulting in single transaction aborting in a transaction chain incase of failure.

#### Strict Schedule

In cascadeless schedule, here the condition is applied for both, read and write in comparison to only read in cascadeless.

<br>

### Non-recoverable schedule

Example

T1 | T2
--- | ---
| R(A) | |
| W(A) | |
| | W(A) |
| | R(A) |
| | commit |
| abort | |

<br>

---
<br>

## Lock based concurrency control protocols



