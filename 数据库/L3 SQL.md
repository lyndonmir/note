# Data Definition Language
## Domain types in SQL
- char(n): Fixed length character string
- varchar(n): Variable length character strings
- int : Interger
- smallint : Small integer
- numeric(p,d) : p->total length; d->fraction length
- real,double precision: machine-dependent precision
- float(n): user-specified precision of at least n digits
- Null value
- date: "2007-2-27"
- Time: "11:18:16:28"
- timestamp: "2011-2-12 11:11:11:11"
- may vary in different sql server
## Create table 
- constraints
- Not null
- Primary key()
- Check(P) P is a predicate
## Drop and alter table
### drop
- drop table t
### alter
- add
- drop
- modify: only modify type or constraints of an attribute, no brackets
## Create index
- create index
- create unique index
- drop an index: drop index $<i-name>$ on table_name
# Basic Structure
## Select clause
- distinct-> no duplicates
- $*$ -> all attributes
- can contain arithmetic expressions
- if more than one tables have the same attribure, add "select A.a"
## Where clause
- combined  with AND,OR,NOT and BETWEEN
## From clause
- Cartesian, so if we need natural joint, add "A.a = B.a"
## Rename operation
- If we want attribute's name"A" is replaced by "B" in the result, use"Select A as B"
- If table name is too long, use "From a1 as a,  b1 as b" , and statement after select and where should be substituted along with
- when self-comparision, eliminate discrimination
## String operation
- LIKE
- `WHERE title LIKE '%computer%'` finds all book titles with the word `computer` anywhere in the book title.
- `   WHERE au_fname LIKE '_ean'` finds all four-letter first names that end with `ean` (`Dean`, `Sean`, and so on).(notice "four", '-' determine bits number of target result)
- match the name"main%" : like "main\\%" escape '\\'
- other functions
## Ordering the display of tuples
- order by attribute_name
- desc: hign to low
- asc: low to high
- ascending is the default
## Duplicates
- to forbid duplicate-> add distinct
# Set Operations
- UNION, INTERSECT, EXCEPT
- automatically eliminates duplicates
- if not use "all": UNION ALL, INTERSECT ALL, EXCEPT ALL
# Aggregate Functions
## Functions
- operate on multiset values
- avg(col)  average
- min(col) minimum
- max(col) max
- sum(col) sum of values
- count(col) number of values: can add "distinct" to be deal with different requirements
- rename like "avg(balance) avg_bal"
## Group by
- attributes in select clause outside of aggregate functions must appear in group by list
- to understand group by, if select a,avg(x), then
avg is operated on a0, a1..... respectively; if select avg(x), then avg is operated on all
- group by's content doesn't need to be write in select clause
## Having
- followed by a condition contained aggregate function
- attributes in having clause outside of aggregate functions must appear in group by list
- inside having clause can't exist non-aggregate variables
## Summary
- select distinct c1,c2
from r1,r2
where condition1
group by c1,c2 having condition2
order by c1 desc c2 desc
- order: from->where->group(aggregate)->having->select->distinct->order by
- aggregate functions cannot be used in where clause directly
# Null values
- missing or inapplicable
- arithmetic of null is null
- comparison->null
- logic 
- aggregate functions ignore nulls except "count"
- where amount is null
# Nested Subqueries
## Example
### Condition
- loan(loan-number,branch-name,account)
- borrower(customer-name,loan-number)
- branch(branch-name, branch-city, assets)
- depositor(customer-name, account-number)
- account(account-number, branch-name, balance)
- keep in mind this two examples, first double set condition, second compare itself
### Key word
- in
- not in
### Idea
- If there are two sets of conditions, commonly we use "and" to solve it, but subqueries work as well; in the ppt's example, loan and borrower is one set, account and depositor is another set; we can solve one in the query and another one in the subquery
- multi attributes before "in" to omit conditions in nested statements' where clause. Such rule is  available when main statement and nested statement have the same condition(31,32state in vscode)
-  main statement's rename is available in nested
- can be used in where clause
- eliminate group by in nested statement by adding main-attribute.a = nested-attribute.a(36);
## Set Comparison
- some
- all
- equal to min or max
- two ways to complish, first use renaming, another is using subqueries
## Test for empty relations
- exists
- not exists
- notice the example in ppt
## Test for absence of duplicate tuples
- unique
- not unique
- in where clause
- main statement and nested statement should match, because where clause is an constraint of main statement, but attribute in main statement is not connected to constraint without matching
- in from clause and can be rename
# Views
## Operation
- create
- drop
## application
- Provide a mechanism to hide certain data form the view of certain
- security
- easy to use, support logic independent
- view just display data, has nothing to do with table's inner structure

# Derived Relations
## As result() clause
- set nested statement in from clause and use "as result()" to rename can make nested statement equivalent to the local view  so that renamed attribute can be used in main statement
## With Clause
- Allow views to be defined locally for a query rather than globally
- Define a local view then use it
## Examples
# Modification of the Database
## Deletion
### basic sentence
- delete from where...
### multi-tables
- multi-talbes:be careful about the order to delete differents tables
### subquery
- execute nested sentences for only one time
- If nested sentence include variables in the main sentence, execute nested sentence each time when execute main sentences
## Insertion
### Basic sentence
### Combined with selection
## Updates
### case-end
- similar to delete's order problem
- case{when then else} end
### Update of view
- only can update simple views defined on a single relation and without aggregates
- all operations on views will be executed on the original tables
## Indexes
- Indices are data structures used to speed up access to records with specified values for index attributes
## Transaction
### General
- A transaction is a sequence of queries and data update statements executed as a single logical unit
- COMMIT WORK: makes all updates of the transaction permanent in the database
- ROLLBACK WORK : undoes all updates performed by the transaction
### Keys
- If any step of a transaction fails, all work done by the transaction can be undone by rollback work
- Rollback is done automatically
- Commit automatically
- turn off automatic commit: Set autocommit = 0
- syntax: set autocommit = 0; statement1, statement2; commit; statement3 ,statement4, commit
### Example
# Joined Relations
## Join Conditions
### Definition
- Defines which tuples in the two relations match
- Defines what attributes are present in the result of the join
### Classification
- natural
- on $<predicate>$
- using($A_{1},A_{2},....,A_{n}$);
## Join Types
### Definition
- Defines how tuples in each relation that do not match any tuple in the other relatiion are treated
### Classification
- Inner join
- left outer join
- right outer join
- full outer join
## Combination of Join Type and Join Condition
### Natural join
- $R\: natural\lbrace {inner\:join,left\:join,right\:join,full\:join}\rbrace S$
### Unnatural join
-  $R\lbrace {inner\:join,left\:join,right\:join,full\:join}\rbrace S \begin{cases}on \\ using \\ \end{cases}$
- on: unnatural connection, allow comparision between different attributes,  and won't eliminate duplicated attributes in the result.
- ![[Pasted image 20230328185555.png]]
- using: similar to natural connection, but only care about attributes in using list.
## Syntax
### SQL Server
- $*=$denotes left join
- equals to: from a left outer join b on a.loan_number = b.loan_number
### Oracle
- where loan.loan_number = borrower.loan_number(+) denotes left join
