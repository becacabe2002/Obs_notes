## I. Approaches
* Top-down:
  - Entity-Relationship
* Bottom-up
  - Functional Dependency
  - Normalization

## II. Indentifying Entities
4 kinds of entity: 
   + People 
   + Things
   + Events
   + Locations

*If it doesn't fit -> Proprerty of an entity (also called "an attribute")*

## III. Indentifying Relationships
+ 1 : N or M : 1
+ 1 : 1
+ M : N

### ***Recursive Relationships***(Quan hệ truy hồi):
- Entities return to themselves
- In ERD, this type of relationship is a line go out of the entity and returns with a loop.
Redundant Relationships (Quan hệ dư thừa)
- The relationships are already indicated by other relationships, directly or through other entities.

### ✅***Sloving Many-to-Many Relationships***
* Not possible in a db

=> Split (M : N) = (1 : M) + (N : 1)
* Create a new entity that is in between the related entities. (called link table, intersection table or junction table)

## IV. Indetifying Attributes
- Find the data elements saved for each entity.

## V. Derived Data (điền nốt các thông tin dựa trên các dữ liệu có sẵn)

## VI. Entity Relationship Diagram (ERD) - Sơ đồ thực thể quan hệ

## VII. 🔑 Assigning Keys
***Primary Keys***
> One or more data attributes that uniquely identify an entity.
+ If primary key has more than one attribute 
-> ***Composite key***
+ Link-entities usually refer to the primary key attributes of the entities that they link.

***Foreign Keys***
> An attribute that refer to the primary key of another entity.

⚠️ <mark style='background-color:#FFFFA7'>It is possible to refer from a part of composite key to a primary key, but it is impossible to refer to a part of composite key </mark>.

## VIII. ❔Defining the Attribute's Data Type
* Some db have their own defined data types.

* Standard data types: `CHAR`, `VARCHAR`, `TEXT`, `FLOAT`, `DOUBLE`, `INT` and `DATE`

## IX. Normalization (1F, 2F, 3F)
- Make data more flexible and reliable.
  - **1F**: no repeating groups of columns in an entity.
  - **2F**: All attributes of an entity should be fully dependent on the whole primary key.
  (if they are not -> split entity into two new entities)
  - **3F**: all attributes have to be dependent on the whole primary key, but not other attributes

