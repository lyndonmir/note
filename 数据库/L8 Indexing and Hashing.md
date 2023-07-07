# Basic Concepts
## Goal
- speed up access to desired data
## Structure
- Search Key: attribute or set of attributes used to look up records in a file
- An index file consists of records(called index entries) of the form: {search-key,pointer}
- Index files are typically much smaller than the original file
## Classification
- Ordered indices: search keys(index entries) are stored in sorted order
- Hash indices: search keys(index entries) are distributed uniformly across "buckets" using a "hash function"
## Index Evaluation Metrics
### Access types which are supported efficiently
- "equal" conditon: Where a = 1
- "not equal" condition: where 1 < a <3
### Access time
### Insertion time
### Deletion time
### Space overhead
# Ordered Indices
## Basic Concepts
- in an ordered index, index entries are sorted on the search key value
### Primary index
- Sequentially ordered file: The records in the file(data file) are ordered by a search-key
- Primary index: an index whose search key equals to the search key of the sequentialy ordererd data file, on which the index is made; also called clustering index
- The search key of a primary index is usually but not necessarily the primary key
- Non-sequential files don't have primary index, but the relations can have primary key
- Index-sequential file: sequentially ordered file with a primary index
### Secondary index
- Secondary index: an index whose search key specifiles an order different from the sequential order of the file; also called non-clustering index
## Classification
### Dense Index Files
- Dense index: Index entry appears for every search-key value in the file:
- note: every search key value but not every record
### Sparse Index Files
- Sparse index: contains index entries for only some search-key values
- Applicable only when data file records are sequentially ordered on search-key while dense index files isn't restricted to it
- ways to locate a record with search-key value K
- more time but less space
- Good tradeoff: select the minimum search key in each block to add to index file
### Secondary Indices
- to find all the records satisfy some condition which is not about the search key of primary index
- use the structure "bucket", a secondary index with an index record for each search-key value; index record points to a bucket that contains pointers to all the actual records with that one particular search=key value
- have to be dense
- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 20_45_49.png]]
### Multilevel Index
- reason: sometimes primary index is too big to fit in memory
- To reduce number of disk accesses to index records, treat primary index kept on disk as a sequential file and construct a sparse index
- outer index: a sparse index of primary index
- inner index: the primary index 
- Indices at all levels must be updated on insertion or deletion from the file.
- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 20_49_28.png]]

- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 20_45_49 1.png]]
### Primary and Secondary Indices
## Index Update
### Deletion
- find the record in the data file and delete the record
- update index file
- case1 : Dense![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 20_57_46.png]]
- case 2: Sparse![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 21_00_57.png]]
### Insertion
- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_15 21_02_47.png]]
# B+- Tree Index Files
## Advantages&Disadvantages
- ad over dis
## Properties
- balanced tree-> same path length
- Each node that isn't a root or a leaf has btw $\lceil {n/2} \rceil$  and n children
- a leaf node has btw $\lceil (n-1)/2 \rceil$  and n-1 values
- if root not a leaf, at least 2 children
- if root a leaf, btw 0 to n-1 values
## Structure
- geeksforgeeks->insertion
## Leaf Nodes in $B^{+}$ Trees
- $P_{i}$ points to a file record with search key value $k_{i}$ , or to a bucket of pointers to file records. Only need bucket structure if search-key doesn't form a primary key.
## Non-Leaf Nodes in $B^{+}$ - Trees
- form a multi-level sparse index
## Queries on $B^{+}$ Trees
### Steps
- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_16 0_09_14.png]]
## Compute
- height: $\lceil log_{\lceil n/2 \rceil}(K)\rceil$ 
## Handing Duplicates
- ![[21121350  Database System   Lecture 9_ Storage and File Structure - Adobe Acrobat Pro DC (32-bit) 2023_6_16 13_04_55.png]]
## Insertion
- see reference
- split: left $\lceil (m-1)/2 \rceil +1$ , different from reference, but inter nodes' splict the same-> see the book
## Deletion
- see reference
## Non-Unique Search Keys
# Write-optimized Indices
# Index Definition in SQL
# Index Definition in SQL
