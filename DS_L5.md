# Database Systems
### Lecture 5 -  Physcial Database Design

---

### Pysical Storage

There is a **3 Level** storage hierarchy:
- Primary Storage, e.g. main memory (RAM), cache
- Secondary Storage, e.g. hard-drive disks, SSD
- Tertiary Storage e.g. optical drives

As we go down the heirarchy:
- Storage capcity: **increases**
- Access Speed: **decreases**
- Money-cost: **decreases**

### For Databases:

A Database is **too large** to fit in the main memory. Therefore, data access involves **secondary storage** due to the lower costs.

##### Consequences:
Since HDD is not CPU-accessible, then
- Data must be loaded into the main memory from disk
- Data is then processed in the main memory

The speed of data acccess becomes low
- Data access from HDD takes 30ms, while only 30ns in RAM, therefore HDD is the main **bottleneck**

The challenge then is:
**How to oragnise data on HDD to minimise this latency**.

---
### Disk Anatomy

How Data is stored on the disk:
1. Take a (magnetic) disk
2. Dig concentric tracks
3. Split tracks into circular sectors
4. Take the DB data
5. Data is organised in **files of records**
6. Each file consists of *blocks* to store these records: ~512bytes
7. Store each block in a set of sectors
8. Done!

Read/Write Access:
1. Get a physical address
2. **Position**: move arms over the tracks
3. **Spin**: right sector under the head
4. **Transfer**: data from track to memory via bus

The **Spatial Optimization Problem**: How to spacialy organize the file blocks to minimize the expected seek/rotation time. 

---

### Organization Based Optimization

How to organize tupes on the disk to minimize I/O access.

Representation in Storage Context:

- Tuple is represented as a **Record**
- **Records** are grouped together forming a **Block**
- **File** is a group of blocks

Records can be **variable** or **fixed** length. 

### Blocking Factor

Blocks are of fixed-length, normally between 512 and 4096 bytes.

Consider a record of **R** Bytes and a block of **B** Bytes. 

The **blocking factor** is defined as the number of records stored in a block:

    bfr = floor(B/R)
    
### Blocks to Files on Disk

A **File** is a set of **blocks**, each block has a set of **records**. 

How do we allocate these blocks on on the disk?

##### Continuous (neighbouring) Allocation

A file will contain spatially consecutive blocks. 

##### Linked Allocation
Each block *i* has a **pointer** to the logically next block *i+1* **anywhere** on the disk. This navigation information is stored on each block.


##### Indexed Allocation
There exists a specific block, which maintains a list of pointers to the physical address of each block, **anywhere** on the disk. This navigation information is stored in a separate block.

---

### File Structures for Database Data

How to distribute records within file blocks to *minimise* I/O Cost?

**Heap File**:
- A new record is added at the end of the file i.e. at the end of the last blcok

**Ordered File**:
- Records are kept sorte with an **ordering field**

**Hash File**:
- A hashing function is applied to each record field
- The output is the physical block address
- This is **mapping a record to a block**.

Whem measuring I/O costs, we look at: 
- Retrieving the whole block containing the record x according to a searching field from the disk to memory
- Inserting/Deleting/Updating a record by transferring the whole block from memory to the disk.

---
### Heap File Complexity 

**Inserting** a new record is efficient.

- Load the **last** block from the disk to the memory
- Insert rhe new record at the **end** of the blcok and **write** the block back to disk


    2 Block accesses
    O(1) block access

**Retrieving** a record is *inefficient*.

- Linear Search through all the file blocks
- Retrieve each block from disk to memory
- Search in-memory for the record
- Repeat until EOF


    On average, we access ~b/2 blocks
    O(b) block access

**Deleting** a record is *inefficient*.

- **Find** and **load** the block containing the record, call the retrieval process
- **Remove** the record from the block and **write** the block back to disk
    - (This leaves *unused* spaces within blocks)


    O(b) + O(1) block accesses
**Deletion markers** (set a bit from 0 to 1) are used to indicate whether a record has been deleted. Then just periodically re-orgainze the file by gathering the non-deleted records and freeing up the space of deleted records

### Heap File - Overall Performace

- **O(1)** for INSERT
- **O(b)** for SELECT
- **O(b) + O(1)** for DELETE, UPDATE

A heap files does the job when only appending information (log files etc).

---
### Sequential File 

All records are stortes by an **ordering field** and are kept sorted at all times.

**Retrieve** a record (with the **ordering field**) is *efficient*.
- The right block is found by binary search on the ordering field.
    

    Compexity is O(log2b)
    
**Retrieve** a record (using a **non-ordering field**) is *inefficient*.


    Complexity is O(b) - linear search
        
**Insertion** is *expensive*.
- First, locate the block where the record should be inserted: binary search
- On avergae half of the records must be moved to make room for the new one

Can use chain pointers to improve this though.

**Deletion** is expensive.

- First locate the block where the record is to be deleted: binary search
- To avoid immediate records movement due to the gap, adopt deletion markers and update the pointer not to point to the deleted record
- Periodically reorganize the file to restore the sequential order 

**Update** on the ordering field is *costly*.
- The new record is deletd from its old position and inserted into a new position

**Update** on the non-ordering field is *efficient*!
- Complexity is O(log2b) + O(1) block 

---

### Hash File

Idea of hashing:
- Partition the records into M buckets.
- Each bucket can have more than one blcok
- Choose a hash function y = h(k) with output = to the bucket values for a value of k

### External Hashing

Mapping a record *x* to a bucket *y=h(x.k)* is called **external hashing**.

**Retrieve** a possible record by hash key SSN:
1. Hash **k** and get the corresponding bucket e.g h(SSN) = M-2
2. Use the file header to translate it to the block address in disk.
3. Fetch the block from the disk to memory
4. Linear search in memory to find the record **x** such that h(SSN) = M-2

##### Algorithm

**Hash Search** (k: hash key)

Pre-Initialization: **Load** the meta-data (hash) block with the file header from disk to memoruy, which contains the hash-map *(bucket, block-address)* 

**Compute** the bucket id y=h(k).
**Access** the in-memory hash-map to get the block address related to bucket y=h(k).

**Load** the block from the disk to memory
**Search** in-memory the record x with hash(x.k)

**If** found **then return** record x
**Else return** not found

    Complexity: O(1) block access
    
### External Hashing Overflow



