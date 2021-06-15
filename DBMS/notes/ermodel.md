# Entity Relationship Model

## Introduction to ER Model

It consists of three components - entity, entity type and entity set.

### Entity
Akin to an object of a class. It is represented by variable.

<br>

### Entity Type
Akin to class. It is represented by rectangle with the entity type name inside the rectangle.

<br>

### Entity set
As evident by the name, it is basically set of entities of a particular entity type. It represented by an vertical oval with variable names inside it.

<br>

### Attributes
Akin to properties in a class. They are represented in an horizontal-oval with its name inside it.

There are four types of attributes - 

#### Key Attribute
Akin to primary key. Represented with an underline below its name inside oval.
#### Composite attribute
Akin to object attribute have many attributes inside it. Represented by attributes sticking out of composite attribute oval.
#### Multivalued attribute
Akin to vector in c++. Can store multiple values and are represented by double oval outline
#### Derived attribute
Akin to local variables which are derived from state variables in a flutter widget. Represented by dashed oval border

<br>

### Relationships

These are the relations between entity types(i.e. between class definitions). These are represented as a diamond with relation ship name inside it with two outward lines connecting two entity types in context.

#### Degree of relationship set 
This is the number of  **different** entity types participating the relationship. There are three types -
+ Unary(eg married To between persons)
+ Binary(eg married to between a man and woman)
+ N-ary

#### Cardinality
This is the number of times an entity can participate. It can be at most once or more than once. The types are as - 
+ One to one : for eg male married to female
+ Many to one/one to many : People with religion
+ Many to many : Students with course

This is represented by numbers beside the line connecting the entity type with relation. Let the number be x, then x => that x entity can have same relation.

#### Participation constraints

These are the constraints applied on the entity set participating in the relationship.

##### Total participation
=> Each entity in the set **must** participate in the relationship. This is depicted by double parallel lines joining the entity type with relation diamond.

##### Partial participation
=> Each entity in the set **may or may not** participate in the relationship. This is depicted by single parallel lines joining the entity type with relation diamond.

#### Weak Entity type
These are the entity type which do not have a primary key, have no independent existence and are always dependent on an **identifying type**. These are represented by double outline rectangle with weak entity name inside it.

#### Identifying Relationship
These are the relationships which identify the weak entities and shows their dependency on identifying entity type. They required total participation of weak entity set and are depicted by double outline diamond.

---

## Enhanced ER model

