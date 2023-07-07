# Entity Sets
## Entity Sets
- Entity
- Relations
- row : entity
- column: attribute
## Attributes
### Domain
- the set of permitted values for each attribute
### Attribute types
- Simple and composite attributes, like sex and name
- Single-valued and multi-valued
- Derived attributes<-> base attributes or stored attributes
# Relationship Sets
## Relationship Sets
### definition
- relationship(composed of primary keys of two entities and other attributes)-> between two or more entities
- relationship set->between two or more entity sets
### formal description
## Degree of a Relationship Set
### definition
- the number of entity sets in a relationship set
### types
- binary
- more than two, but rare
## Mappping Cardinalities
### defintion
- the number of entities to which another entity can be associated via a relationship set
### types
- one to one
- one to many
- many to one
- many to many
# Keys
## Keys for Entity Sets
### Super key
- a set of one or more attributes whose values determine each entity
### Candidate key
- a minimal super key
## Keys for Relationship Sets
### Super key
- can be formed with the  combination of primary keys of the participating entity sets
### Primary key
- one to one: each primary key from entity set itself is a primary key of the relationship set
- one to many: select primary key from the "many" entity
- many to one: select primary key from the "many" entity
- many to many: combination of two primary keys from entity sets
# E-R Diagram
## Symbols
## Concept
### Recursive relationship set
- Entity sets of a relationship need not be distinct， which means there exists a relationship over one entity set itself
### Role
- the function that an entity plays in a relationship
## Relationship Constraints
### Express the Cardinality Constraints
- one to one: E<-R->E
- one to many: E<-R--E
- many to one: E--R->E
- many to many: E--R--E
### Participation Constraints
- Total participation: double line
- Partial participation: single line
### Alternative Notion for Relationship Constraints
- upper bound: from cardinality constraints
- lower bound: from participation constraints
-  format: a..b or a..\*(infinite)
## Degree 
### Binary vs Non-Binary Relationships
- sometimes binary is wrong
### Converting Non-Binary to Binary
- by creating an artificial entity set 
- by using a known entity set which can form relationship with other entity sets
# Weak Entity Sets
## Definition
- an entity set without a primary key
## Concepts
### dependence
- a weak entity set must depend on a identifying entity set or owner entity set
- via a total, one-to-many relationship set from the identifying to the weak one
- the related relationship is called identifying relationship
### discriminator or partial key
- the set of attributes that distinguishes among entities in a weak entity set that depend on one particular strong entity
### primary key of weak entity
- combination of strong set's primary key and weak one's discriminator
### store
- primary key of strong entity set is not explicitly stored with the weak entity set
# Extended E-R Features
## Stratum of the entity set
### Specialization
- Top-down
- Attribute inheritance
- Lower-level set has attributes that don't apply to higher-level entity set
- symbol
### Generalization
- bottom-up
- inversions of specialization
## Design Constraints
### Constraint on which entites can be members of a given lower-level entity set
- condtion-defined
- user-defined
### Constraints on whether or not entities may belong to more than one lower-level entity set within a single generalizatiion
- Disjoint
- Overlapping
### Completeness constraint
- Total: each entity(or all entites) must belong to one of the lower-level entity sets
- Partial: an entity need not belong o one of the lower-level entity sets
## Aggregation
### Basic Idea
- Treat relationship as an abstract entity
- Allows relationships between relationships or relationship and entity
- Abstraction of relationship into new entity
# Summary of Symbols
## Old
## New
# Design of an E-R Database Schema
## E-R Design Decisions zhiyunkk
### 1) Use an attribute or entity set to represent an object
- entity set can only correspond with another entity set but not attributes of another entity set
- an object can be either attribute or entity set but not both
- decides upon number of attributes of the object
### 2) Use it as an entity set or relationship set
- action->relationship set: verb
### 3) Use it as attribute of an entity or a relationship
### 4) Ternary or n-ary relationship versus binary relationships
### 5) strong or weak entity set
### 6) specialization or generalization
### 7) aggregation
# Reduction of an E-R Schema to Tables
## Representing Enity Sets as Tables
### strong entity sets
- to a table with the same attributes
### composite attributes
- create a separate table
### multivalued attributes
- represented by a separate table
### weak entity sets
- include a column for the primary key of the identifying strong entity set
## Representing Relationship Sets as Tables
### column 
- include primary keys of two participating entity sets(not simple combination, but see the situation like one to one, one to many, etc) and any descriptive attributes of the relationship set itself
### primary key
- one to one
- one to many
- many to one
- many to many
## Redundancy of Tables
### Rule1
- Many-to-one and one-to-many relationship sets that are total on the many-side can be represented by adding an extra attribute to the "many" side, containing the primary key of the one side, thus eliminate the relation table, note that it's not to eliminate the one-side entity but the relationship between one-side entity and many-side entity
- if partial, it causes null
- For one-to-one, either side can be chosen as the "many" side
### Rule2
- the identifying relationship is redundant
## Representing Specialization as Tables
### method1
- form a table for the higher level entity
- form a table for each lower level entity set, including primary key of higher level entity set and local attributes
- getting information from a lower level requires accessing two tables: lower level itself and higher level
### method2
- Form a table for each entity set with all local and inherited attributes
- If specialization is total, table for generalized entity not required to store information, instead use a view
- may cause redundantly
# Example 3
- Student(S-ID, name, age, gender)
- Undergraduate(S-ID,year,GPA,email)
- Graduate(S-ID,advisor,email)
- Take(S-ID,C-ID,score)
- TA(S-ID,C-iD,Start_t,End_t)
- Course(C-ID,name,credits,room)
- ** Email(S-ID,email)
- -------
- Course(C-ID,name,credits,room,S-ID,Start_t,End_t)







