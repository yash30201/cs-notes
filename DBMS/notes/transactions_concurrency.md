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
<br>

> Locks are implemented using linked list

Though concurrent and interleaving execution of transactions may lead to problems like irrecoverable schedule, inconsistency and many more threats.

But the effect in efficiency is huge to dive into this paradigm. So for concurrency, we need protocols so that ACID properties are strictly followed. So we use concurrency control protocols : 

+ Lock Based Protocols
    + Basic 2-Phase Locking
    + Conservative 2-PL
    + Strict 2-PL
    + Rigorous 2-PL
+ Graph Based Protocols
+ Timestamp based protocols
+ Multiple granularity protocol
+ Multi-version protocol

<br>

---
<br>

## Lock Based Protocols
<br>

They allow accessing and owning of database items by concurrently executing transactions in mutually exclusive manner. There are two types of lock normally - 

Let A be a data item then 

**Shared Lock - S(A)** : Read-only lock.
**eXclusive lock - X(A)** : Read-write lock.

Locks can be upgraded from shared to exclusive and downgraded from exclusive to shared.

### Problems in basic / simple locking (Binary locking)

#### Deadlock

#### Starvation

To overcome these, we use further more sound protocols

<br>

---
<br>

## Two Phase Locking
<br>

A transaction is said to follow 2-PL is the locking and unlocking are done in separate two ways, namely growing phase and shrinking phase.

> **LOCK POINT** : for a transaction, lock point is the point where growing phase ends

**Advantages** : Ensured conflict serialisability.

**Disadvantages** : Cascade rollback is possible, deadlocks and starvations are possible


Categories of 2-PL - 

<br>

### Strict 2-PL
<br>

Required all the exclusive locks held by the transaction to be released only after commit.

Thus makes transactions recoverable and cascadeless. Deadlocks are still possible.

<br>

### Rigorous 2-PL
<br>

Required all the exclusive as well as shared locks held by the transaction to be released only after commit.

Thus makes transactions recoverable and cascadeless. Deadlocks are still possible.

<br>

### Conservative 2-PL (static 2-PL)

This protocol requires the transaction to lock all the items it access before the Transaction begins execution by pre-declaring its read-set and write-set. If any of the predeclared items needed cannot be locked, the transaction does not lock any of the items, instead, it waits until all the items are available for locking. 

Thus, its deadlock free, but cascading rollback and starvation is still possible.


<br>

---
<br>

## Timestamp ordering protocols
<br>

**TS(T)** : Timestamp of transaction T

Here, main idea is to order transactions on the basis of their timestamps.

Let, 

**W_TS(X)** : be the largest timestamp of any transaction that executed write(X) successfully.

**R_TS(X)** : be the largest timestamp of any transaction that executed read(X) successfully. 

Basic time stamp ordering protocol states : 

Try to serialise all the operations and resolve conflicts according to the timestamps of their transaction. 

Whenever a Transaction T issues a W_item(X) operation, check the following conditions: 
+ If R_TS(X) > TS(T) or if W_TS(X) > TS(T), then abort and rollback T and reject the operation. else,
+ Execute W_item(X) operation of T and set W_TS(X) to TS(T).


Whenever a Transaction T issues a R_item(X) operation, check the following conditions: 
+ If W_TS(X) > TS(T), then abort and reject T and reject the operation, else
+ If W_TS(X) <= TS(T), then execute the R_item(X) operation of T and set R_TS(X) to the larger of TS(T) and current R_TS(X). 

<br>

---
<br>

## Deadlock prevention protocols
<br>

### Wait-die

If older has problems, then he waits.

If younger has problems, then he dies.

<br>

### Wound-wait

If older has problems, then he kills younger.

If younger has problems, then he waits.
<br>

Both schemes put the younger ones at disadvantage!!


<br>

---
<br>

## Transaction isolation levels

General transaction isolation levels : 

### Dirty Read

Its a situation when a transactions reads a data that has been modified but not yet committed.

### Non Repeatable read

It occurs when a transaction reads the same row twice and gets a different value each time.

Eg : R<sub>T1</sub>(X) -> W<sub>T2</sub>(X) -> commit(T2) -> R<sub>T1</sub>(X)

### Phantom read

This happens when two same queries fetch different rows.

Eg : due to the search criteria being changed

<br>

Based on these, SQL defines standard four isolation levels(in increasing level of isolation) :

### Read uncommitted 

+ Lowest level of isolation.
+ Allows dirty read

### Read Committed

+ Dirty read not allowed
+ Transactions holds the write locks until they commit to facilitate this

### Repeatable read 

+ Both read and write locks are help until commit.

### Serialisable

A schedule of operations such that concurrent operations are guaranteed to be serialisable and appear to serially executing.






