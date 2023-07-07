# SQL Data Types and Schemas
## Types
### User-defined types
- create type
- create domain
- domain vs type: type is strong, domain is weak
### Large-object types
- blob: binary large object
- clob: character large object
- pointer is returned
## Schemas
- schema: database
# Integrity Constraints
## Domain Constraints
### syntax
- in create statement
- Constraint value-test check(value >=4 )
## Referential Integrity
### Formal Definition
- Let r1(R1) and r2(R2) be the relations with primary keys K1 and K2 respectively
- The subset $\alpha$ of R2 is a foreign key referencing K1 in relation r1, if for every t2 in r2 there must be a tuple t1 in r1 such that t1\[K1\] = t2\[$\alpha$].
- Referential integrity constraint also called subset dependency$$ \Pi _{\alpha} (r_{2}) \subseteq \Pi  _{K_{1}} (r_{1})$$
- $\alpha$ must have corresponding values in R1, if not ,set null
### Checking Referential Integrity on Database Modification
- Insert
- Delete
- Update
### Syntax
- foreign key(account-number) references account
- account-number char(10) references account
- foreign key(account-number) references account(account-number): name could be different but not type
### Cascading Actions is SQL
- foreign key (branch-name) references branch on delete cascade on update cascade
- After one operation on a certain relation, other relations associated with it by referential integrity must execute same operation, it's across the entire chain
- But if some violatioin can't be handled in the chain, just undo all operations, aborts the transaction
- Alternative to cascading: on delete set null, on delete set default
- A constraints can alternatively be specified as not deferrable
## Assertions
### Definition
- a predicate expressing a condition that we widh the database always to satisfy
### Syntax
- Create assertion \<assertion-name> check \<predicate>
- often with "not exist" statement
### Effect
- test it for validtity on every update
- may introduce as significant amount of overhead
## Triggers
### Definition
- A trigger is a statement that is executed automatically by the system as a side-effect of a modification to the database
### Syntax
- condition
- actions
- Create trigger overdraft-trigger after update on account referencing... as... when... begin... end
### Trigger Events and Actions in SQL
- insert, delete or update
- Triggers on update can be restricted to specified attributes: after update of balance on account
- Values of attributes before and after an update can be referenced
### Statement Level Triggers
### External Word Actoins
- cannot be used to directly implement external-world actions
- can be used to record actions-to-be taken in a separate table
- an external process execute this table
### When not to use triggers
### Examples
# Authorization
## Security
- Database system level
- Operating system level
- Network level
- Physical level
- Humal level
## Forms of authorization on parts of the database
- Read authorization
- Insert authorization
- Updata authorization
- Delete authorization
## Forms of authorization to modify the database schema
- Index authorization
- Resourses authorization: allows creation of new relations
- Alteration authorization: allows addition or modifying of attributes in a relation
- Drop authorization: allows deletion of relations
## Authorization on Views
- Creation of view doesn't require resources authorization
- The creator of a view gets only thoes privileges that provide no additional authorization beyond that he already had
## Granting of Privileges
### Graph
- all edges msut be part of some path originating with the database administrator
- revoke chain
- prevent cycles of grants with no path from the root
### Syntax
- Grant \<privilege list> on \<table | view> to \<user list>
- with grant option: pass on
### Privileges in SQL
- Select
- insert
- update
- delete
- references
- all privileges
### Roles
- create role teller
- grant select on branch to teller
- grant teller to alice, bob
## Revoking Authorization in SQL
### Syntax
- revoke \<privilege list> on \<table | view> from \<user list> \[restrict | cascade]
### notes
- \<privilege-list> may be all, to revoke all privileges the revokee may hold
- if \<revokee-list> incluses PUBLIC, all users lose the privilege except those granted it explicity
- if the same privilege was grantted twice to the same user by different grantees, the user may retain the privilege after the revocation
- All privileges that depend on the privilege being revoked are alse revoked
## Limitations of SQL Authorization
## Audit Trails
### Defintion
- a log of all changes to the database 
- used to track erroneous/fraudulent updates
- can be implemented using triggers
# Embedded SQL
# Dynamic SQL
# ODBC and JDBC

