# Failure Classifcation
## Classification
### Transaction failure
- logical errors
- system errors
### System crash
- Fail-stop assumption
### Disk failure
## Recovery Algorithms
- Actions taken during normal transaction processing to ensure enough information exists to reover from failures
- Actions taken after a failure to recover the database contents to a state that ensures atomicity, consistency and durability
# Log-Based Recovery
## Concepts
- A log is kept on stable storage, is a sequence of log records, and maintains a record of updataed activities on the database
## Steps
- When transaction starts:
- Before write
- When finish
## Deferred Database Modification
### Concepts:
- Deferred Update: It is a technique for the maintenance of the transaction log files of the DBMS. It is also called NO-UNDO/REDO technique. It is used for the recovery of transaction failures that occur due to power, memory, or OS failures. Whenever any transaction is executed, the updates are not made immediately to the database. They are first recorded on the log file and then those changes are applied once the commit is done. This is called the “Re-doing” process. Once the rollback is done none of the changes are applied to the database and the changes in the log file are also discarded. If the commit is done before crashing the system, then after restarting the system the changes that have been recorded in the log file are thus applied to the database.
### Steps
### At time of crash
## Immediate Database Modification
### Concepts
-  **Immediate Update:** It is a technique for the maintenance of the transaction log files of the DBMS. It is also called UNDO/REDO technique. It is used for the recovery of transaction failures that occur due to power, memory, or OS failures. Whenever any transaction is executed, the updates are made directly to the database and the log file is also maintained which contains both old and new values. Once the commit is done, all the changes get stored permanently in the database, and records in the log file are thus discarded. Once rollback is done the old values get restored in the database and all the changes made to the database are also discarded. This is called the “Un-doing” process. If the commit is done before crashing the system, then after restarting the system the changes are stored permanently in the database. 
### Notes
### Example
## How to recovery(Immediate Database Modification)
### Two Operations
- undo
- redo
### Requests
- Both operations must be idempotent
### Steps
- undo operations are performed first, then rdo operations
### Example
## Checkpoints
### Problem
- Redoing/undoinig all transactioins recorded in the log can be slow
### Streamline recovery procedure by periodically performing checkpointing
- output all log records currently residing in main memory onto stable storage
- output all modified buffer blocks to the disk
- write a log record \<checkpoint L> onto stable storage where L is a list of all transactons active at the time of checkpoint
- All updates are stopped while doing checkpointing
### Following
- During recovery we nned to consider only the most recent transaction $T_{i}$ that starrted before the checkpoint, and transactions that started after $T_{i}$ 
- scan backwards from end of log to find the moset recent\<checkpoint L> record 
- only transactoins that are in L or started after the checkpoint nneed to be redone or undone
- Transactions that committed or aborted before the checkpoint already have all theri updates output to stable storage
### Some earlier part of log may be needed for undo operationis
- continue scanning backwards till a record \<$T_{i}$ start> is found for every transaction $T_{i}$ in L
- Parts of log prior to  earliest \<$T_{i}$ start> record above are not needed for recovery, and can be erased whenever desired
- ![[Chapter 17_ Recovery System - Adobe Acrobat Pro DC (32-bit) 2023_6_19 18_18_59.png]]
## Recovery Algorithms
### Logging(during normal operation)
- \<Ti start> at transaction start
- \<Ti,Xj,V1,V2> for each update and
- \<Ti commit>  aat transaction end
### Transaction rollback(during normal operation)
- to roll back Ti
- scan log backwards from the end, and for each log record of Ti of the form \<Ti,Xj,V1,V2>
- 1. perform the undo by writing V1 to Xj
- 2.Write a log record \<Ti,Xj,V1>
- 2.1 such log rcords are called compensate log records
- once the record \<Ti start> is found stop the san and write the log record \<Ti,abort>
### Recovery from failure: Two phases
- redo phase: replay updates of all transactions, whether they committed, aborted, or are incomplete
- undo phase: undo all incomplete transactions
### Redo phase
- Find last \<checkpoint L> record, and set undo-list to L
- Scan forward from above \<checkpoint L> record
- 2.1 whenever a record \<TI,Xj,V1,V2> or \<Ti,Xj,V2> is found, redo it by writing V2 to Xj
- 2.2 whenever a log record \<Ti start> is found, add Ti to undo-list
- 2.3 whenever a log record \<Ti commit> or \<Ti abort> is found, remove Ti from undo-list
### Undo phase
- Scan log backwards from end
- 1 whenever a log record \<Ti,Xj,V1,V2> is found where Ti is in undo-list perform same actions as for transaction rollback
- 1.1 perform undo by writing V1 to Xj
- 1.2 write a log record \<Ti,Xj,V1>
- 2 Whenever a log record \<Ti start> is found where Ti is in undo-list,
- 2.1 Write a log record \<Ti abort>
- remove Ti from undo-list
- 3 Stop when undo-list is empty
### After undo phase completes,  normal transaction processing can commence
### Example
# Recovery With Concurrent Transactions
## Overview
### We modify the log-based recovery schemes to allow mutiple transactions to execute concurrently
- all transactions share a single disk buffer and a single log file
- a buffer block can have data items updated by one or more transactions
### We assume concurrency control using strict-two-phasing locking(--2PL with X-locks held until the end of the transaction)
### Logging is done as described earlier
### The checkpointing technique and actions taken on recovery have to be changed
- since serveral transactions may be active when a checkpoint is performed
### Checkpoints are performed as vefore, except that the checkpoint log record is now of the form
- \<checkpoint L>
- where L is the list of transactions active at the time of the checkpoint, like {T2,T4}
- we assume no updates are in progress while the checkpoint is carried out
### Steps: When the system recovers from a cash
- First:
1. Initialize undo-list and redo-list to empty
2. Scan the log backwards from the end, stopping scan when the first\<checkpoint L> record is found. Meanwhile, for each record found in log during the backward scan
2. 1 if the record is \<Ti commit>, add Ti to redo-list
2. 2 if the record is \<Ti start>, then if Ti is ont in redo-list, add Ti to undo-list
2. 3 if the record is \<Ti abort>, add Ti to undo-list
3. For every Ti in L, if Ti is not in redo-list, add Ti to undo-list
3. 1 at this point, undo-list consists of incomplete transactions which must be undone, and redo-list consists of finished transactions that must be redone
 - Recovery now continues as follows
 1. Scan log backwards from the end of log file, stopping when \<Ti start> records ave been encountered for every Ti in undo-list.During the scan, perform undo for each log record that belongs to a transaction in undo-list
 2. locate the most recent \<Ccheckpoint L> record
 3. Scan log forwards from the \<checkpoint L> record till the end of the log
 3. 1 During the scan, perform redo for each log record that belongs to a transaction on redo-list
# Buffer Management
## Overview
### Situations when log records are output to stable storage
- block of log records are full
- or a log force operation is executed(checkpoint)
### Lock force
- to commit a transaction by forcing all its log records to stable storage(including the commit record \<Ti commit)>
## Rules
- Log records are output to stable storage in the order in which they are created.
- Transaction Ti enters the commit state only when the log record Ti commit> has been output to stable storage.
- Before the < Ti commit> can be output to stable storage, all log records pertaining to Ti must have been output to stable storage.
- Before a block of data in main memory is output to the database , all log records pertaining to the data in that block must have been output to stable storage(write-achead logging rule)
## Database Buffering
### Database maintains an in memory buffer of data blocks
### The recovery algorithm supports the no force policy
- , i.e., updated blocks need not be written to disk when transaction commits
- Force policy : requires updated blocks to be written at commit
### The recovery algorithm supports the steal policy
- , i.e., blocks containing updates of uncommitted transactions can be written to disk, even before the transaction commits
- If a block with uncommitted updates is output to disk, log records with undo information for the updates are output to the log on stable storage first
### No updates should be in progress on a block when it is output to disk. 
- Before writing a data item, transaction acquires exclusive lock on block containing the data item
- Lock can be released once the write is completed.
### To output a block to disk
- First acquire an exclusive latch on the block
- Then perform a log flush
- Then output the block to disk
- Finally release the latch on the block
## Buffer Management
### In main-memory
### In virtue memory
# Failure with Loss of Nonvolatile Storage
# Recovery with Early Lock Release

# ARIES Recovery Algorithm