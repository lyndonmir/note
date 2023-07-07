# Transaction Concept
## Definition
- A transaction is a unit of program execution that accesses and possibly updates various data items
## ACID Properties
- Atomicity
- Consistency
- Isolation
- Durability
# Transaction State
- Active
- Partially committed
- Failed
- Aborted
- Committed
# Implementation of Atomicity and Durability
## Implementation
- recovery-management component: shadow-database scheme
1. a pointer called db_pointer points to the current consistent copy of the database
2. all updates are made on a newly created copy of the database. The original copy--shadow copy is untouched--pointed by db_ppointer
- if aborted: merely delete the new copy
- if commited:
- 1> Put all pagaes in memory of the new copy to disk
- 2> db_pointer is changed to point to the new copy--become the current copy nad at the same time the old copy is then deleted
## Required
- update db_pointer atomically
- no concurrent transactions
- assume disks not to fail
# Concurrent Executions
## Definition
## Advantages
## Problems
## Concurrency control schemes
## Schedules
- sequences that indicate the chronological order in which instructions of concurrent transactionis are executed
- must consist of all instructions of the transactions
- must preserve the order in which the instructions appear in each individual transaction
- consistency!
# Serializability
## Basic Assumption
- Each transaction preserves database consistency
- seerial execution of a set of transactions preserves database consistency
- A schedule is serializable (possibly concurrent) if it's equivalent to a serial schedule. (Conflict serializability, view serializability)
- simplified: consist only read and write instructions
## Conflicting Instructions
- read and write
- write and read
- write and write
- forces a (logical )tmporal order between conflicted instructions
## Conflict Serializability
- conflict equivalent
- confict serializable
# Recoverability
## Recoverable Schedules
- to address the effect of transactioin failures on concurrently running transactions
- recoverable schedule: if a transaction $T_{j}$ reads a data item previously written by a transaction $T_{i}$ ,then the commit operation of $T_{i}$ appears before the commit operation of $T_{j}$
- example
## Cascading Rollbacks
- a single transaction failure leads to a series of transaction rollbacks
- can lead to the undoing of a significant amount of work
## Cascadeless Schedules
- cascading rollbacks cannot occur; for each pair of transactions $T_{i}$ and $T_{j}$ such that $T_{j}$ reads a data item previously written by $T_{i}$ , the commit operation of $T_{i}$ appears before the read operatino of $T_{j}$
- Every cascadeless schedule is also recoverable
- it's desirable to restrict the schedules to those that are cascadeless
# Implementation of Isolation
- A policy in which only one transaction can execute at a time
	generates serial schedules , but provides a poor degree of
	concurrency.
- Schedules must be conflict or view serializable , and recoverable , for
	the sake of database consistency, and preferably cascadeless
- Concurrency control schemes tradeoff between the amount of
	concurrency they allow and the amount of overhead that they incur.
- Some schemes allow only conflict serializable schedules to be
	generated, while others allow view serializable schedules that are
	not conflict serializable.
# Transaction Definition in SQL
# Testing for Serializability
## Precedence graph
- a schedule is conflict serializable if and only if its precedence graph is acyclic
- if precedence graph is acyclic, the serializability order can be obtained by a topologcical sorting of the graph
-  See references
## Concurrency Control vs Serializability Tests
## Weak Levels of Consistency
## Levels of Consistency in SQL-92


