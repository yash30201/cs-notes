# Relational Algebra

## Introduction to relational algebra in DBMS
<br>

Relational Algebra is a procedural query language which takes relations as an input and returns relation as an output.

Basically......function(relation) to relation. The following are the basic relational operators - 

### Projection

Symbol - ∏

This is used to project / select required column data from a relation(Table). By default, this operator removes redundant copies of same data after applyling the operation.

Usage : ∏<sub>(column_name1 column_name2)</sub> relation_name 

<br>

### Selection

Symbol - (sigma) => σ

This is user to select required tuple(rows) from the relation. To display the data, projection operator is required.

Usage : π( σ<sub>(\<condition like (column_name \> value)\>)</sub> Relation_name) 

<br>

### Union

Symbol - (capital u) => U

This operator take the union of the value to two relations. **The relations must have same attributes** It takes all the distinct tuples from the two relations

<br>

### Set Difference

Symbol - (minus) => -

This works just like set difference incase of sets, the tuples not present in other relation are taken up from current relation.

<br>

### Rename

Symbol - (rho) => ρ

This allows us to rename a relation.

Usage : ρ(new_relation_name / old_relation_name)
> Special usage - to create a new relation being a projection of an existing with a particular new name 
`ρ(new_relation_name, ∏(Column_1, Column_2..)(Existing_relation_name))`

<br>

### Cross Product

Symbol - (cross) => X

Cross Product between two relations (let them be `A` with `n` entries & `B` with `m` entries) will be new relation (`Z` with `n*m` entries) such that for each tuple of relation `A` , there will be `m` entries of relation `B` i.e common tuple `A` +  tuples of B.

<br>

---
<br>


## Extended Operators

These are the operators derived from basic relational operators. Mainly they can be categorised as Intersection, Join and Divide.

<br>

### Intersection

Symbol - (ulta u) => ∩

This is a binary operator applied on two union compatible relations. It can be inferred as common tuples in both relations.

> In terms of basic operators <br>
Relation_1 ∩ Relation_2 = Relation_1 + Relation_2 - (Relation_1 U Relation_2)

<br>

### Join

#### Conditional Join

Symbol - ⋈<sub>c</sub>

Conditional join is used when you want to join two or more relation based on some conditions

Usage : Relation_1 ⋈<sub>c \<condition\></sub> Relation_2

> In-terms of basic operations<br>
σ<sub>(\<Condition\>)</sub>(Relation1 X Relation2)

#### Equijoin

Symbol - ⋈

This is a special case of conditional join where only equality condition holds between a pair of attributes. As they are joined, only one attribute will appear in result, for eg if profit and bank balance are equalised, then only profil attribute will appear.

Usage : Relation_1 ⋈<sub>\<Equality Condition\></sub>  Relation_2

>In-terms of basic operators<br>
∏<sub>(\<All the attributes of cross product except matching attribute of Relation_2\>)</sub> σ<sub>(\<Equality Condition\>)</sub>(Relation1 X Relation2)

#### Natural join

Symbol -  ⋈

This is a special case of equijoin in which equality condition holds true on all the attributes which have same name in Relation_1 and Relation_2. Thus while writing, there is no need to write equality condition explicitly.

Usage : Relation_1 ⋈ Relation_2

> Inner join vs outer join -> Inner join only returns data which are satisfied by the conditions where as outer join also returns dissatisfied data.

#### Outer joins - 

There are 3 types of outer joins - Left join(⟕), right join(⟖) and Full outer join(⟗). Here, the field value which are absent are put to be NULL.

<br>

### Division operator 

Division operator A÷B can be applied if and only if:

+ Attributes of B is proper subset of Attributes of A.
+ The relation returned by division operator will have attributes = (All attributes of A – All Attributes of B)
+ The relation returned by division operator will return those tuples from relation A which are associated to every B’s tuple.

Example - 

Relation 1

**Roll No** | **Sports**
--- | ---
1 | Badminton
2 | Cricket
2 | Badminton
4 | Cricket

Relation 2

| **Sports** |
| --- |
| Badminton |
| Cricket |

Then Relation_1 ÷ Relation_2 = 

| **Roll_no** |
---
2

Because only roll no 2 is associated with all the tuples of sports in relation 2

<br>

---
<br>

## Join Operation vs Nested Query

+ In same system, the difference is negligible but incase of distributed system, 
    + In nested query, we only extract the relevant info from each table(located on different computers) and then merge the tuples obtained to get the result.
    + In join, we would be required to fetch the whole table from each system and then create a large table from which the filtering will occur, hence more time will be required.

+ Regarding optimisation, Joins are universally understood thus no optimisation issues arise whereas its not he case for nested queries, so avoid them incase of portable system to dodge bugs
    + Subqueries mau take long time to execute depending on how the database optimiser treats it(as it may or may not treat it as join resulting in may ot may not fastness).

+ Queries have no cache facility. If any constant subquery is there multiple times in the whole query, then it will be evaluated as many time as encountered. This becomes a problem is the constant subquery has large number of tuples. Subqueries return a set of data whereas join returns a necessarily indexed dataset. Incase of large results, working on index data in better.

+ Subqueries are easier to read, understand and to evaluate than joins. Also subqueries each are isolated and thus allow a bottom up approach.

<br>

---
<br>

## Tuple relational calculus

<br>

Tuple calculus is a non-procedural query language. Unlike relational algebra, this only provides the description of the query but it does no provides the methods to solve it. i.e., It explains what to do but not how to do.

In tuple calculus, a query is expressed as

```
{ t | P(t) }, where
t = resulting tuples
P(t) = Conditions that are used to fetch resulting tuples
```

P(t) or predicate may have various conditions logically combined with OR (∨), AND (∧), NOT(¬)

It also uses quantifiers - 

∃ t ∈ r (Q(t)) = ”there exists” a tuple in t in relation r such that predicate Q(t) is true.

∀ t ∈ r (Q(t)) = Q(t) is true “for all” tuples in relation r.

See these [examples](https://www.geeksforgeeks.org/tuple-relational-calculus-trc-in-dbms/#1b4172cd-acc7-4363-9184-3fadd3cdabcf)

<br>

---
<br>

## Row vs column oriented data stores in dbms

If time permits, then only read [this](https://www.geeksforgeeks.org/difference-between-row-oriented-and-column-oriented-data-stores-in-dbms/)

<br>

---
<br>

## Questions

The questions are easy. Agar time bohot hai to dekh lena [ye](https://www.geeksforgeeks.org/how-to-solve-relational-algebra-problems-for-gate-2/)


