# Normalisation

## Normal Forms in DBMS
<br>

Some key words : <br> 
+ Prime attribute :  Attribute which is a part of a candidate key
+ Partial Dependency => There exist a non Prime attribute which is dependent on any **sub set** of candidate key<br>
For eg here, Course fee is partially dependent on course no which is a subset of a candidate key {student_no, course_no}.

> STUD_NO | COURSE_NO | COURSE_FEE
> --- | --- | ---
> 1 | C1 | 1000
> 2 | C2 | 1500
> 1 | C4 | 2000
> 4 | C3 | 1000
> 4 | C1 | 1000
> 2 | C5 | 2000

+ Transitive Dependency => X -> Y and Y -> Z then X->Z is called transitive dependency

<br>

### First Normal Form
<br>

=> The relation should not contain any multivalued attribute. Every attribute should be single valued.

Every relation in a relational database is always at-least in 1NF. 

<br>

### Second Normal Form
<br>

Every 1NF relation where it doesn't has any partial dependency is called to be in 2NF.

2NF tries to reduce the redundant data getting stored in memory. For eg in above example table, we can separate the data into STUDENT(STUD_NO, COURSE_NO) and COURSE (COURSE_NO, COURSE_FEE). The course fee table will have not have any redundant data.

<br>

### Third Normal Form
<br>

Every 2NF having no transitive dependency is in 3NF. 

In other words a relation is in 3NF if at-least one the following holds true for every non-trivial dependency X->Y: 
+ X is a super key
+ Y is a primary attribute(i.e each element of Y is in some candidate key)

<br>

### Boyce-Codd Normal Form(BCNF)
<br>

Every 3NF relation is said to be in BCNF if for every FD in 3NF, the LHS is a super key.

+ Every binary relation(i.e binary table) is always in BCNF.
+ Sometimes going for BCNF may not preserve the functional dependency.

> To check highest NF of a relation with given functional dependencies, start checking from BCNF to 3NF to 2NF , if any is true then no need to check for lower forms.

<br>

---
<br>

## Minimum relations satisfying 1NF

Rules - 

+ If there is total participation in both sides
    + Merge both the entities and the relation between then into a single table.
+ If there is total participation at one end
    + M:N Merge the relationship to the total participation side
    + 1 : N - Merge the relationship into the total participation side
    + 1 : 1 - Merge both the entities and the relation into 1 table
+ If both sides have partial participation
    + M : N - Have 3 separate tables 
    + 1 : N - Merge the relationship to the N-side
    + 1 : 1 - Merge the relationship to one the entity
