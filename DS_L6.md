# Database Systems
### Lecture 6 - Indexing Methodology (1)
---

##### Physical Design
Given a *specific* file type, provide a **primary access** path based on a *specific searching* field (e.g. search only SSN)

##### Index Design
Given *any* file type, provide a **secondary access** path using *more* than one searching field (e.g. SSN, Salary, Name etc).

**COST**: Additional meta-data file on the disk & maintanance
**BENEFIT**: Expedite significatly the search process avoiding Linear Scans

---

### Principles

##### Principle 1:
Create *one* index over *one* field

##### Principle 2:
An index is in another *separate* file

##### Principle 3:
All index entries are *unique & sorted* 

##### Principle 4:
*First* search within the index to *find* the block pointer, *then* access the block from the data-file

#### Hypothesis 1: Index file occupies less blocks than the data-file

**Fact**: index entries are smaller records. We fit more index entries in a block than data-records.

**Dense index**: an index entry for every record in the file
**Sparse Index**: index entries for only some of the records (e.g. every second record)

#### Hypothesis 2: Searching over index is faster than over file

**Fact**: By definition, index is an ordered file, thus we adpot **binary-based** and/or **tree-based** methods to find the pointer to the actual data block

# Proof
### Indexes: 1-D Space

**Primary index**: index field is an **ordering-key** field of a sequential file

**Clustering index**: index field is an **ordering non-key** field of a sequential file

**Secondary index**: index field is - 

- A **non-ordering** key field e.g. unique passport number, over an ordered or non-orderd file
- A **non-ordering non-key** field e.g. salary, over an ordered or non-ordered file

---

### Primary Index

An ordered file over an **ordering key** of a sequential data-file:
- fixed-length index entries = pair **(k**i **,p**i **)**
- **k**i is the unique value of the index field
- **p**i is the pointer to the i-th block containing the record with key **k**i

**Sparseness**: one index-entry per data block.
- i-th index entry **(k**i **,p**i **)** refers to the i-th data block
- **k**i is the field value of the first record in block i
- The first data-record in block i with value **k**i is the anchor block i

Overhead vs Speed: 0.37% storage, 53% speed-up

##### Decision Making 1

When deciding to create a Primary Index.

**Indicator**: observe the frequency of anchor-records updates/deletions

**Theorem 1**: Primary Index is created if the block can accomodate at least two index entries independantly of the number of data-records.

---

### Clustering Index

**Challenge 1**: Index a sequential file on an **ordering, non-key** field e.g. create an index on EMPLOYEE ordered by DNO.

**Idea**: The file is a set of clusters of blocks, a cluster per distinct value:

    index-entry = (distinct-value, block pointer)

- One index entry per distinct clustering value
- Block pointer points at the first block of the cluster

##### Decision Making 2

When we decide to create a clustering index.

**Theorm 2**: A clustering index of *m* blocks is always created over a *ordering non-key* field.

**Proof**: cost over the index < cost over linear search since index blocks *m* < file blocks *b* and:

    log2(m) < b(n+1)/2n - (b/n) = b(n-1)/2n < b/2 < log2(b)
    
Overhead vs Speed: 0.01% storage, 81.8% speed-up

---

### Secondary Index

**Challenge 2**: Index a file on a *non-ordering* field. The file might be unordered, hashed, or ordered **but not ordered according to index field**. 

Cases:
- **[S1]** Secondary index on a non-ordering, key field e.g. SSN
- **[S2]** Secondary index on a non-ordering, non-key field e.g. DNO

### [S1]
One index entry per data record i.e.**dense** index. This is because, the file is not ordered according to the indexing field, therefore **anchor records cant be used**:
        
        index-entry = (index-value, block-pointer)
        
Overhead vs Speed: 14% storage, 99.68% speed-up

### [S2]

**Idea 1**: group the block addresses of those records having the same index value
**Idea 2**: assign an index entry per group (cluster) of block addresses

A **cluster-pointer** points to (2 levels of indirection):
- (Level 1) a block of {block pointers} of a cluster
- (Level 2) a block pointer points to the data-block that has records with this distict index value

### Multi-level index

**Observation**: in all index files it holds true that:
- they are ordered on the indexing field
- the indexing field has unique values
- each index entry is of fixed length

**Conclusion**: we can build a primary index over any index file, since it is an orderd file with reference to a key field.

**Challenge 3**: Find the best level *t* of a multi-level index to expedite the search process trading off speed-up with overhead. 

**Idea**: A logarithm with base m > 2 splits the search space into *m* subspaces until finding the unique block. 

**Theorm 3**: Given a Level-1 Index with *m* being the blocking factor of the Level-1 Index file, then the multi-level index is of *maximum* level **t=logm(b)**.

This has a **scalable design** independant of data-size, which is the start of Big Database Systems.

Overhead vs Speed: 14.7% storage, 99.9% speed-up & 66.7% faster than L1

See lecture notes for proof