# Database Systems
### Lecture 8 - Query Processing
---

### Fundamental Tool: Sorting

Almost all SQL queries involve **sorting** tuples. We cannot store the entire relation into memory for sorting the records. Therefore we must implement:
- **External Sorting** - sorting algorithm for large relations stored on disk that do not fit entirely in main memory. 
---
### External Sorting

Works in a **Divide & Sort (Conquer)** system.

##### Divide: 
A file into many smaller **sub-files** and write them to the disk. 

##### Sort:
Load each small sub file to memory, sort using **quick-sort** or **bubble-sort** and write it back to the disk. 

##### Merge:
Merge two (or more) sorted sub-files **loaded from disk** in memory. This creates bigger sorted sub-files, that are then merged in turn. 
LOOP ↫

### Overview

**Lemma 1**:

        Expected cost = 2b(1 + logm(L))

- *b*, number of blocks
- *M*: **degree of merging** (number of sorted blocks merged in each loop)
- *L*: number of the initial sorted sub-files (before entering merge phase)
- **Keep** *M > 2* **for best performance**.

---

### Strategies for SELECT

        SELECT * FROM relation WHERE selection-conditions
        
#### S1: Linear Search
Retrieve *every* record and test whether it satisfies condition.
**Pre-condition**: none
**Expected Cost**: b/2

#### S2: Binary Search
Involves the use of an **ordering key** (file is sorted before).
**Pre-condition**: file is sorted
**Expected Cost** (sorted): log2(b)
**Expected Cost** (unsorted): log2(b) + 2b(1 + logm(L))

#### S3: Use of Primary Index or Hashing over a key
Involves equality on *key* with a primary index or hash function *h(key)*.
**Pre-condition**: Primary Index of level *t*, over the *key* (file sorted by key)
**Pre-condition**: File hashed with the *key*
**Expected Cost** (sorted): *t + 1*
**Expected Cost** (hashed-file): 1 (*no-overflow* buckets)

#### S4: Use of a Primary Index in a Range Query
Involves a *range* (>,<,<=,>=) on a key with a Primary index. Use *Index* to find the record **satisfying the equality** and then **retrieve all subsequent blocks** from the ordered file. 
**Pre-condition**: Primary Index level of *t* over the key (file sorted by key)
**Expected Cost**: (t+1) + O(b)
> Note: Hashing should not be used for range queries

#### S5: Use of Clustering Index to retrieve multiple records
Involves equality on a *non-key*. Retireve all the contiguous blocks of the cluster of the non-key value. 
**Pre-condition**: Clustering Index level of *t* on non-key (file sorted by non-key)
**Expected Cost**: (t+1) + O(b/n)
> Note: n = number of distinct values of the non-key attribute

#### S6.1: Use of Secondary Index (B+Tree) over equality involving a non-ordering key
Retrieve a single record
**Pre-condition**: File is **not** ordered by key
**Expected Cost**: t+1
> Note: B+ Leaf Node points at unique block

#### S6.2: Use of Secondary Index (B+Tree) over equality involving a non-ordering non-key
Retrieve multiple records from different blocks
**Pre-condition**: File is **not** ordered by key
**Expected Cost**: t+1 + O(b)
> Note: B+ Leaf Node points to a **block of pointers** to data blocks that satisfy WHERE clause

---

### Strategies for Disjunctive SELECT
    
    SELECT * FROM EMPLOYEE
    WHERE   SALARY > 10000 OR NAME LIKE '%CHRIS%'
    
**Disjunctive Selections**: conditions involving *OR*
*Final result*: contains tuples satisfying the **union** of *all* **selection conditions**

##### Method:

**IF** an access path exists (B+/Hash/PI) for **all** the attributes:
- Use each to retrieve the set of records satisfying each condition
- **Union** all sets to get final result

**ELSE** if none or some of the attributes have an access path:
- **linear search** is unavoidable.

---

### Strategies for Conjunctive SELECT
    SELECT *    FROM EMPLOYEE
    WHERE       SALARY  > 40000 AND NAME LIKE '&CHRIS%'
**Conjunctive Selections**: conditions involving *AND* 

##### Method:

**IF** an access path exists for an attribute, use it to revtrieve tupples satisfying that condition [INTERMIDIATE RESULT].

**GO** through this intermediate result to check which record satisfies also the other condition **in memory**. 

---

### Strategies for JOIN

    SELECT * 
    FROM EMPLOYEE E, DEPARTMENT D
    WHERE E.DNO = D.DNUMBER
**Obeservation**: the most resource-consuming operator.
**Focus**: two-way equijoin (join two relations with '=')

**Five** fundemental strategies for join processing
1. Naive join
2. Nested-loop join
3. Index-based nested-loop join
4. Merge-join
5. Hash-join
---
#### Naive Join
**Idea**: A naive natural strategy, which doesnt require access path
**Join query**: R.A = S.B
- Step 1: Compute the cartesian product of **R** and **S**, i.e. all tuples from **R** are combined with the ones from **S**.
- Step 2: Store the result in a file **T** and for concatenated tuples t = (*r*,*s*)with *r* ∈ **R** and *s* ∈ **S** check if *r*.A = *s*.B

##### Algorithm:
- T = Cartesian R x S
- **Scan** T, a tuple t ∈ T t a time: t = (r, s)
 - **IF** r.A = s.B 
 - **THEN** add (r,s) to the result file
 - **ELSE go to** next tuple t ∈ T

**Outcome**: *inefficient*, typically the result is a small subset of the cartesian
Tuples may not match, therefore **try to predict matches in advance**!
----

### Nested-Loop Join

**Idea**: A non-naive natural strategy, which does not require any access path

##### Algorithm:

- **FOR** each tuple r ∈ **R**
    - **FOR** each tuple s ∈ **S**
        - **IF** r.A = s.B **THEN**
        - add (r,s) to the result file

**Step 1**: 
- LOAD a set of blocks from the outer relation R
- LOAD one block from inner realtion S
- Maintain an output buffer for the matching tuples

**Step 2**:
- JOIN the S block with each **R** block from the chunk
- FOR each matching tuple r ∈ **R**-block and s∈**S**-block ADD (r,s) to ouput buffer
- IF Output Buffer is full, PAUSE; WRITE current join result to disk; CONTINUE

**Step 3**: LOAD next S-Block and GOTO **Step 2**
**Step 4**: GOTO **Step 1**
> Note: the outer & inner loops are over blocks and not over tuples
Note: Re-form the pseudocode in a block-centric programming mode

---

### Index-Based Nested-Loop Join 
**Idea**: Use of an index on either A or B joining attributes: **R**.A = **S**.B
**Focus**: Assume an index f on joining attribute B of relation S


##### Algorithm:
- **FOR** each tuple r ∈ R
    - **Use** index of B from S by f(r.A), to retrieve all tuples s ∈ **S** having s.B=r.A
    - **FOR** each such tuple s ∈ **S**, add matching tuple (r,s) to the result file

**Outcome**: Much faster compared to nested-loop join. We get immediate access on s ∈ **S** with s.B = r.A by searching for r.A using the index f on B, avoiding linear search on **S**.

---

### Sort-Merge Join
**Idea**: Use of the merge sort algorithm over two sorted relations w.r.t their joining attributes
**Precondition**: Relations **R** and **S** are *physically ordered* on their joining A and B

##### Method:
**Step 1**: 
- Load a pair {R.Block, S.Block} of *sorted* blocks into the memory

**Step 2**: 
- Both blocks are *linearly * scanned *concurrently* over the joinign attributes (list-merge mode)

**Step 3**: 
- If matching tuples found then store them in a buffer

**Gain**: The blocks of each file are scanned only once
**But**: If **R** and **S** are not a-priori *physically* ordered on A and B then *sort* them first!
---

### Hash-Join 
**Precondition**: 
- File **R** is partitioned into M buckets w.r.t *hash function* over joining attribute A
- File **S** is also partitioned into M buckets w.r.t the same hash function h over attribute B

**Assumption**: R is the *smallest file* and fits into main memory: M buckets of **R** are in memory. 

##### Algorithm Hash-Join
Partitioning Phase:
- **FOR** each tuple r ∈ **R**
    - **Compute** y=h(r.A) - *address of bucket*
    - **Place** tuple r into bucket y=h(r.A)

Probing Phase:
- **FOR** eacg tuple s ∈ **S**
    - **Compute** y=h(s.B) - *use same hash function*
    - **Find** the bucket y = h(s.B) in memory (of the **R** partition)
    - **For** *each* tuple r ∈ **R** in the bucket y=h(s.B)
        - **If** s.B = r.A **add** (r,s) to the result file

---

FOR COSTING PREDICTIONS SEE LECTURE SLIDES