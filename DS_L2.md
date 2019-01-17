# Database Systems
### Lecture 2 - Functional Dependency & Normalisation Theory
---

### Guidelines for a GOOD Design

##### Guideline 1:

The **attributes** within a relation should make sense. 

- Attributes of *different* entities (students, employees, courses) should **not be in the same** relation. 
- Any relationship between entities should be represented **only** through **foreign keys**. 


##### Guideline 2:

Avoid *redundant* tuples (repetition of the *same* information)

The impact of not achieving this is:
- **Storage cost**
- **Consistency cost & operation anomalies**
    - replicas must be kept consistent during *insertions*, *deletion* and *updating* of tuples

##### Guideline 3:

Relations should be desinged such that tuples have as **few** *NULL* values as possible.

Attributes that are frequently NULL should be placed in separate relations to avoid **waste of storage & reduce uncertainty**.

Reasons for NULL:
- A value is *not applicable*
    - a supervisor cant be supervised by any other supervisor
- A value is *unknown*
- A value is *known* to exist but *unavailable*

##### Guideline 4:

Desing relations to avoid *fictitious* tuples after *join*. 

FINISH THESE NOTES DURING LECTURE

---

### Theory of Functional Dependency

**Functional Dependancy** measures the *degree of goodness* of relational schema:

- A FD is a *constraint* that derives from the inter-relationships between attributes of a tuple.

Given a relation **R**, an attribute X *functionally determines* an attribute Y, if a value of X determines a *unique* value for Y. 

**FD: X -> Y** (X *uniquely determines* Y) holds if whenever two tuples have the same value for **X** they must have the same value for **Y**.

##### Principles:
1:
If **K** is a **candidate key** of relation **R**, then **K** *functionally determines all* attributes in **R**. 

2:

ADD IN LECTURE

---

### Functional Dependeny & Normalization

> Idea: exploit the FDs to specify which attributes can become keys.

Algorithm:
1. Assert which are the FDs anmong attributes
2. Take a pool and put into all the asserted FDs
3. Create a universal **big** relation with all attributes
4. *Recursively decompose* the big relation based on FDs into many **smaller** ones, such that, when we re-join them together, it guaruntees that no information is lost and the big relation can be reconstructed *without* fictitious tuples.

This is the **normalization** process.


### Theory of Normalization


**Progressive decomposition** of unsatisfactory (bad) relations by breaking up their attributes into *smaller good* relations. 

The *degree of decomposition* is refererred to as **Normal Form** (NF): 
- First Normal Form (1NF)
- Second Normal Form (2NF)
- Third Normal Form (3NF)
- Boyce-Codd Normal Form (BCNF)
- Fourth Normal Form (4NF)

**Objective**: The *higher* the NF, the higher the *quality* of the schema
**Target**: *normalize* to the highest possible NF, usually up to 3NF or BCNF

Why only up to 3 or BCNF?

- Answer: because if we decompose the original relation into *many* good relations, we need to pay a lot for *reconstructing* the split information.

---

### Quick Definitions

A **prime attribute** is an attribute that belongs to some candidate key of the relation.

A **non-prime attribute** is not a prime attribute, its not a member of *any* candidate key.

---

FINISH NORMALIZATION NOTES IN LECTURE


