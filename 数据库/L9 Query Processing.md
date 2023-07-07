# Overview
## Basic Steps in Query Processing
### Parsing and translation
- Parser checks syntax, verifies relations
- Translate the query into extended relational algebra(ERA)
### Optimization
- many equivalent relational algebra expressions
- each relational algebra operation have different algorithms
### Evaluation
- The query-evaluation engine takes a query-evaluation plan, executes that plan and returns the answers to the query
- A evaluation plan defines the algorithm
- evaluation in query is execute
# Measures of Query Cost
## Three Points
- CPU can't manipulate the data in disk directly
- Growth rate of transfer speed is much slower than the disk size
- Growth rate of seek speed is much slower than the transfer
## Total elapsed time
- Disk access + CPU + network communication
- Disk access time is the predominant cost
## Disk access
- number of seek operations performed
- number of blocks read \* average-block-read-cost
- number of blocks write\* average-block-write-cost
- write cost more than read, read back after writing to verify
- $t_{T}$: time to transfer one block
- $t_{S}$: time for one seek
# Select Operation
## A1 Linear search
### Cost
- $b_{r}$ denotes number of blocks containing records from relation r
- Cost estimate = $b_{r}$ block transfers + 1 seek
- If selection is on a key attribute no matter candidate key or primary key, since key value is unique, stop right after find it; so the average numbers of transfers is $b_{r}$/2
### Condition
- regardless of selection condition or ordering of records in the file or avaliability of indices
## A2 Binary search
### Cost
- $log_{2}(b_{r})$ \*($t_{S}+t_{T}$) : A1 just settle the head one time to the block; but A2 need to reset head each time we transfer data
- block transfer = \[$log_{2}(b_{r})$] + \[sc(A,r)/$f_{r}$] - 1; sc(A,r) is all satisfied records, $f_{r}$ is number of records in each block; the rate is the number of blocks that have satisfied record; minus 1 represents the first satisfied block which we seek for; when there more than one satisfied records, we should consider this special condtion
### Condition
- applicable if selection is an equality comparison on the attribute on which file is ordered; not used for unequality such as > or <
## A3(primary index, equality on key)
### Cost
- ($h_{i}+1$)\*($t_{s}+t_{T}$): $h_{i}$: the height of B+ tree, so $h_{i}+1$ level
## A4(primary index, equality on nonkey)
- $h_{i}$\*($t_{T}+t_{S}$) + $t_{S} + t_{T}$ \* b : because on nonkey, so multiple records
- The primary index's search key needn't be key
- attribute searched for is also the search key
- b blocks contain retrieved records
## A5(secondary index, equality on nonkey)
- totally n matching records, each may on different block
- ($h_{i}$+1)\* ($t_{T} +t_{S}$) if search-key is a candidate key
- ($h_{i}$+n)\*($t_{T} + t_{S]}$) if search-key is not a candidate key, different form A4 because in secondary index, we need to seek each time not one time
- attribute searched for is also the search key
- block transfer: each time we get a index entry in B+ tree, we need to transfer the block which the entry points to
## A6 (Primary index, comparison)
- for bigger than, use index to search the first tuple in relation
- for less then, just read until the invalild one
## A7(secondary index, comparison)
- use index to search index entry and use pointers
- just use index instead of searching in authentic table compared with A6
## A8(conjunctive selection using one index)
## A9 (conjunctive selection using comopsite index)
## A10(conjunctive selection by intersection of identifiers)
## Bitmap Index Scan
# Sorting
## How
- quicksort: for relations that fit in memory
- external sort-merge: for relations that don't fit in memory
## External sort-merge
- divide into unit which fits the memory
- use quicksort in the memory to sort each unit
- write unit back
- use 2-way merge sort
- use M-1 because the '1' used as output buff, others are input buff
## Transfers
- passes required: $\lceil log_{M-1} (b_{r}/M) \rceil$  
- ![[21121350  Database System   Lecture 11_ Query Processing - Adobe Acrobat Pro DC (32-bit) 2023_6_17 23_14_37.png]]
- each pass need write into and out of memory, so 2$b_{r}$ each pass
- The last merge doesn't need write into, so this pass is 1, and the first initial need 2, so the sum is
- $b_{r}(2\lceil log_{M-1}(b_{r}/M)\rceil+1)$  
## Seeks:
- during initial(run), write and read , 2$\lceil b_{r}/M \rceil$  
- during merge:: buffer size is $b_{b}$ 
- for each pass need2 $b_{r}/b_{b}$  
- sum: $2\lceil b_{r}/M \rceil+\lceil b_{r}/b_{b} \rceil (2\lceil log_{M-1}(b_{r}/M)-1)$  
# Join
## Nested-Loop Join
- see powerpoint
- one outer record read all inner blocks then next outer block
### Transfer
- two outer needs 2
- inner is matched each record in outer, so 6(records of outer)\*3(blocks of inner)
### Seeks
- Steps as follows
1. outer head to first outer block
2. inner head from first outer block to first inner block
3. inner head to second inner block
4. inner head to third inner block
5. outer head to second outer block
6. inner head from second outer block to first inner block
7. inner head to second inner block
8. inner head to third inner block
## Block Nested-Loop Join
- one outer record in one outer block read one inner block each time,
- it follows next record in the same outer block read one inner block
- after the all the records in the certain outer block read the first inner block, they sequentially reacd the second inner block
- after all records in the certain outer block read all inner blocks, it follows the next outer block do the same thing
### Transfer
- Each block in the inner relation is read once for each block in the outer relation(instead of once for each tuple in the outer relation)
- so 2\*3 (2 outer blocks) not 6\*3(6 outer tuples)
- 2\*3 + 2 totally
### Seek
- The same as tranfer 
- 2+2, 2 outer blocks instead of 6 outer tuples
## Indexed Nested-Loop Join
### Worst Case
- buffer has space for only one page of r, and , for each tuple in r, we perform an index lookup on s
### Cost
- $b_{r}(t_{S}+t_{T})+n_{r}*c$  
### Example
- Num of records of customer:n = 10,000, depositor:n = 5000
- Num of blocks of   customer:b = 400 ,    depositor:b = 100
## Merge-Join(sort-merge join)
### Conditions
- only for equi-joins and natural joins
- each block needs to be read only once
- $b_{b}$ : buffer size
### Cost
- $b_{r}+b_{s}$ block transfers
- $\lceil b_{r}/b_{b} \rceil + \lceil b_{s}+b_{b}\rceil$  seeks
## Hash-Join
### Conditions
- equi-jjoins and natural joins
- a hash function h is used to partitiion tuples of both relations
- h maps JoinAttrs values to {0,1,...,n}
### Steps
- r tuples in $r_{i}$ only need to be compared with s tuples in $s_{i}$  ,Need not be compared with s tuples in any other partition
### Algorithm
### Notes
- use a relatively small set to generate a hash set to probe the larger one
### Cost
## Complex Joins


