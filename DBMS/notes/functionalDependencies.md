# Functional Dependencies

<br>

## Functional Dependencies and attribute closure
<br>

### Introduction

Functional dependency set_of_attributes(A) -> set_of_attribute(B) implies that for each unique value of A, the value of B will always be the same.

> General examples are - <br>
STUD_NO->STUD_NAME, STUD_NO->STUD_PHONE **hold**<br>
STUD_NAME->STUD_ADDR **do not hold**

#### Trivial vs Non-trivial FD vs Semi Non Trivial
Trivial example : {Email id, Name} -> { EMail id}<br>
Semi Non Trivial : AB -> BC

<br>

### Properties of Functional Dependencies

These several properties of functional dependencies which always hold in R are known as **Armstrong Axioms** : 

#### Reflexivity : 
If set_of_attributes(Y) is a subset of set_of_attributes(X) then X -> Y, i.e. trivial FD.

#### Augmentation : 
If X -> Y => XZ -> YZ

#### Transitivity : 
If X -> Y and Y -> Z => X -> Z


> Armstrong’s Axioms are a set of rules, that when applied repeatedly, generates a closure of functional dependencies.  Armstrong axioms refer to the `sound and complete` set of inference rules that is used to test the logical implication of functional dependencies.



<br>

### Functional Dependency set and attribute closure

This is the set of all FDs present in the relation.

**Attribute Enclosure** is the attribute set for each unique LHS attribute combination in FD set such that all the set of attributes which can be functionally determined from it are on the RHS including the LHS.

In short *The set of attributes that are functionally dependent on the attribute A is called Attribute Closure of A and it can be represented as A<sup>+</sup>.*

For eg <br>

For relation R(EMPLOYEE_ID, EMPLOYEE_NAME, EMPLOYEE_CITY, EMPLOYEE_STATE), the attribute enclosures of all the attributes are : <br>
+ (EMPLOYEE_ID)<sup>+</sup> = { EMPLOYEE_ID, EMPLOYEE_NAME, EMPLOYEE_CITY, EMPLOYEE_STATE}
+ (EMPLOYEE_NAME)<sup>+</sup> = { EMPLOYEE_NAME}
+ (EMPLOYEE_CITY)<sup>+</sup> = { EMPLOYEE_CITY, EMPLOYEE_STATE}
+ (EMPLOYEE_STATE)<sup>+</sup> = { EMPLOYEE_STATE}

If time permits, see these [questions](https://www.geeksforgeeks.org/functional-dependency-and-attribute-closure/) though they are easy and logical.


<br>

---
<br>

## Equivalence of Functional Dependencies

How to find relationship between two FD sets?

Let FD1 and FD2 are two FD sets for a relation R.

+ If all FDs of FD1 can be derived from FDs present in FD2, we can say that FD2 ⊃ FD1.
+ If all FDs of FD2 can be derived from FDs present in FD1, we can say that FD1 ⊃ FD2.
+ If 1 and 2 both are true, FD1=FD2.

<br>

---
<br>

## Canonical Cover

This is the most reduced form of the set of functional dependencies of a relation such that all the properties of original set of FD are followed and this has no extraneous attributes.



