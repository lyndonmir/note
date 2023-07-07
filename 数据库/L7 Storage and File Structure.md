# Overview of Physical Storage Media
## Classification
### reliability
- volatile
- non-volatile
### Speed
- cache
- main memory
- flash memory
- magnetic disk
- optical storage
- tape storage
## Storage Hierachy
- ![[No Slide Title - Adobe Acrobat Pro DC (32-bit) 2023_6_15 17_24_20.png]]
# Magnetic Disks
## Structure
### arm assembly
### arm
### read-write head
### spindle
### cylinder
### platter
- 50k-100k tracks per platter 
### track
- 500-1000 sectors (on inner tracks) to 1000 to 2000 (on outer tracks)
### sector
- smallest unit of data that can be read or written
- typically 512 bytes
## Seek
- disk arm swings to position head on right track
- platter spins continually; data is read/written as sector passed under head
## Interact
- use disk controller btw system and disks
- scsi: parallel
- sas: serialization

## Performance Measures of Disks
### Access time
- seek time: track
- rotational latency: sector
### Data-transfer rate
- 25-100MB per second max rate
### Mean time to failure(MTTF)
## Optimization of Disk-Block Access
### Block
- A contiguous sequence of sectors from a single track
### Disk-arm-scheduling algorithms
- elevator algorithm
### File organization
- store related informatino on the same or nearby cylinders
- defragment 
### Non-volatile write buffers
- non-volatile ram: battery backed up ram or flash memory
- write back: to buffer; write through: to memory
### Log disk
- a disk devoted to writing a sequential log of block updates
# Storage Acess
## Buffer
### physical 
- portion of main memory available to store copies of disk blocks
### structure
- page: unit of data
- block: unit of disk space
- frame: unit of buffer pool
### prodedure
- ![[No Slide Title - Adobe Acrobat Pro DC (32-bit) 2023_6_15 18_20_02.png]]
### Constraints
- pin
- pin count
- toss-immediate stratey
- forced output of blocks
- dirty
### BUffer-replacement policies
- LRU strategy
- MRU strategy
# File Organization
## Structure
- file
- record
- field
## Fixed-length records
- simple approach
- deletion
## Free Lists
- store the address of  the first deleted record in the file header
- use the first record to store the address of the second deleted record
- like pointers, save space since use the original table, instead of establish new one
## Variable-Length Records
- first fixed length attributes then virable
- null values by null-value bitmap
## Slotted Page Structure
### content
- Number of record entries
- End of free space in the block
- Location and size of each record
### pointers
- Pointers (Index) should not point directly to record instead they should point to the entry for the record in header indirect pointer
### notes
- Records can be moved around within a page to keep them contiguous with no empty space between them; entry in the header must be updated.
## Fixed-length represention
### reserved space can use fixed length records of a known
- maximum length ; unused space in shorter records filled with a null or end of record symbol.
### pointer method
# Column-Oriented Storage
## Definition
- also columnar representation
- store each attribute of a relation separately
## Benifits&Drawbacks
