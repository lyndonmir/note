# Lock-Based Protocols
## Concepts
### Basis
- Serializable schedule is the basis of the concurrent control
### Two modes
- Exclusive(X) mode. Both read and written. X-lock use lock-X instruction
- Shared(S) mode. Can only read. lock-S instruction
- Lock requests are made to concurrency-control manager, transaction can proceed only after request is granted
### How lock works
- A transaction may be granted a lock on an item if the requested lock is compatible with locks already held on the item by other transactions
- Any number of transactions can hold shared locks on an item, but if any transaction holds an exclusive on the item no other transaction may hold any lock on the item
- If a lock cannot be granted, the requesting transcation is made wait till all incompatible locks held by other transactions have been released. The lock is then granted
## Schedule With Lock Grants
- A locking protocol is a set of rules followed by all transactions while requesting and releasing lock
- Locking protocols enforce serializability by restricting the set of possible schedules
## Pitfalls of Lock-Based Protocols
- deadlock: deadlock happens when two or more transactions are waiting for each other to release a lock on a data item, and none of them can proceed
- starvation: Starvation happens when a transaction is repeatedly denied access to a data item because of other transactionis holding locks on it
## The Two-Phase Locking Protocol
### Goal
- Ensure conflict-serializable schedules
### Phase 1: Growing Phase
- Transactoin may obtain locks
- Transacton may not release locks
### Phase 2: Shrinking Phase
- Transaction may release locks
- Transaction may not obrain locks
### Assure serializability
- It can be proved that the transactions can be serialized in order of their lock points(the point where a transaction acquired its final lock), note the lock that used for deciding the order must be on the same attribute
### Drawback
- not ensure freedom from deadlocks
### Strict two-phase locking
- to make cascading roll-back impossible. Here a transaction must hold all its exclusive locks till it commits/aborts
### Rigorous two-phase locking
- Here all locks are held  till commit/abort. In this protocol transactions can be serizlized in the order in which they commit
### When to use
## Lock Conversions
### 2PL with lock conversions
- First Phase: acquire S/aquire X/convert S to X
- Scond Phase: release S/release X/ convert X to S
## Automatic Acquisition of locks
- Operation read(D)
- Operation write(D)
- All locks are released after commit or abort
## Implementation of Locking
- lock manager+
- lock table
## Graph-Based Protocols
### Definition
### Tree protocol
### Advantages
- ensures conflict serializability as well as freedom from deadlock
- Unlocking may occur earlier in the tree-locking protocol than  in 2pl":
1. shorter waiting times, and increase in concurrency
2. protocol is deadlock-free, no rollbacks are required
### Drawbacks
- not guarantee recoverability or cascade freedom: need to introduce commit dependencies to ensure recoverability
- Transactions may have to lock data items that they don't access
### Schedules not possible under two-phase locking are possible uncdr tree protocol, and vice versa
# Multiple Granularity
## Concepts
- For the convenience, allow data items to be locked in various sizes according to to the requirements multiple granularity .
- Define a hierarchy of data granularities, where the small granularities are nested within larger ones, and can be represented graphically as a tree (but don't confuse with tree locking protocol) (see next page)
- When a transaction locks a node in the tree explicitly, it implicitly locks all the node's descendents in the same mode .
- Granularity of locking (level in tree where locking is done): Fine granularity and Coarse granularity
## Intention Lock
### Procedure
- Intention locks are put on all the ancestors of a node before that node is locked explicitly
### Advantage
- allow a higher level node to be locked in S or X mode without having to check all descendent nodes
### Intention Lock Modes
- Intention-shared(IS)
- Intentioin-exclusive(IX)
- Shared and intention-exclusive(SIX): root->shared mode; others->exclusive-mode
### Compatibility Matrix
## Multiple Granularity Locking Schema
1
2
3
4
5
6
- Locks are acquired in root-to-leaf order, whereas they are released in leaf-to-root order
# Deadlock Handling
## How to handle
- Deadlock prevention
- Deadlock detection and deadlock recovery
## Deadlock prevention
### Strategy1
- Require that each transaction locks all its data items before it begins execution(predeclaration)- conservative 2PL(Either all or none are locks)
- Disadvantages: bad concurrency, hard to predict
### Strategy2
- Impose partial ordering of all data items and require that a transaction can lock data items only in the order(graph-based protocol)-- therefore never form a cycle
### Timeout-Based Schemes
- A transaction waits for a lock only for a specified amount of time. After that, the wait times out and the transaction is rolled back.
- Thus deadlocks are not possible
- Simple to implement; but starvation is possible. Also difficult to determine good value of the timeout interval.
### Wait-die scheme-- non-preemptive
- Older transaction may wait for younger one to release data item. Younger transactions never wait for older ones; they are rolled back instead.
- A transaction may die several times before acquiring needed data item
### Wound-wait scheme-- preemptive
- Older transaction wounds (forces rollback) of younger transaction instead of waiting for it. Younger transactions may wait for older ones.
- May be fewer rollbacks than wait die scheme
### For Wait-die and Wound-wait
- Both in wait die and in wound wait schemes, a rolled back transactions is restarted with its original timestamp. Older transactions thus have precedence over newer ones, and starvation is hence avoided.
## Deadlock Detection
### Wait-for graph
- definiton
- how a cycle defined here
## Deadlock Recovery
When deadlock is detected
- Some transaction will have to roll back(made a victim) to break deadlock. Select that transaction as victim that will incur minimum cost
- Rollback-- determine how far to roll back transaction
1. Total rollback: Abort the transaction and then restart it
2. Partial rollback: Roll back transaction only as far as necessary to break deadlock
- Starvation happens if same transaction is always chosen as victim. Include the number of rollbacks in the cost factor to avoid starvation