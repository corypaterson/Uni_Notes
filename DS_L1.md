# Database Systems
### Lecture 1 - Relational Model
---
### The Database System:

The fundemental functionality is to provide software to:

- **Model Data**: relational modelling (for this course)
- **Access Data**: *Query* for data, *insert*, *delete* and *update*;
- **Analyze Data**: complext aggregation queries, function approximation, histograms, ...
- **Physically store data**: from memory to hard disks;
- **Secure data**: control access to sensitive data, ciphers and encoding


We must **maintain data consistency** in the face of machine failures, power cuts etc. **Optimise data access** to efficiently retrieve data (indexing and hashing structures, optimization algorithms etc).

---
### Relational Model

An **entity** and a **relationship** are modelled as a *relation*, which maps to a 2-D table:

- An ordered set of **attributes** (columns), where each column gives an indication of the meaning belonging to that relation
    - Must assume values within a domain:
        - varchar(50)
        - natural numbers
        - real numbers
        - boolean/status
- A set of **tuples** (rows), which represent instances of the relation
- There exists a **specific** attribute that **uniquely** identifies a tuple in the relation. 

SEE LECTURE NOTES FOR CONTEXT EXAMPLE OF RELATIONAL MODELLING - COMPANY

---
### Relational Constraints

Constraints are conditions that must hold on all valid relational instances for each relation.

There are *three* fundemental constraints:

##### Key Constraint:

If a column is a candidate/primary key, then it has the constraint that each tuple must have a **unique value** in that column.

**Super Key**:

 A superkey **SK** of relation **R** is a subset of attributes containing *at least* one attribute that uniquely identifies a tuple.

E.g. EMPLOYEE: **{SSN, Ename, Bdate}** , **{SSN}**, **{SSN, ENAME}**, {Ename, Salary}, {Dno, Lname}
**\*** all valid superkeys.

A **candidate key** is the minimal superkey. It is minimal, if the *removal* of **any** attribute from the candidsate key, results in K no longer being a super key. 

>From the above example **{SSN}** would be the minimal superkey and therefore the candidate.

If there are several candidate keys, then one is chosen randomly to be the **primary key**.

##### Entity Integrity Constraint:** 

The **primary key** PK cannot be NULL in any tuple of a relationship instance. If the PK has multiple attribtues (composite primary key), then NULL is not allowed in any of these attributes.

##### Referential Integrity Constraint:

Referencing relation R1, and referenced relation R2:

        R1 -----> R2
        
There exists an attribute FK (**Foreign Key**) in R2 having the *exact same* value with the  **Primary Key** PK in R1 or is *NULL*.

---

### Quick Summary

- **super key** is used to uniquely identify a tuple in a relation
- If K is a **superkey**, then *any superset* of K is a superkey

- **Candidate Key** is the *minimal* superkey, K is a candidate key if there is no subset of K that is also a superkey

- A relation can have several different candidate keys, one of them is chosen to be the **primary key**.
    - Key attributes are *underlined* in the relational schema.

- A **foreign key** in a referencing relation must have either a *NULL* value (if it is not part of the primary key) or a value of the primary key of the referenced relation.
---

### Fundemental Operations:

        INSERT a tuple
        DELETE a tuple
        UPDATE a tuple

**Principle 1:** Integrity constraints *should not be violated* by the operations.

**Principle 2:** Operations may *propogate* to **trigger** other operations *automatically*. Integrity constraints must be maintained, thus the database transits between consistent states.

If an **integrity contraint is violated**:
- *Cancel* the operation that causes the violation
- *Perform* the operation but inform the user of the violation
- *Trigger* additional operations to correct the violation
    -  CASCADE option
    -  SET NULL option
-  *Execute* a user-specified error-correction procedure

---

### Violations

##### INSERT Violations:

- **Domain:** one of the attribute values for the *new* tuple is not in the attribute domain.
- **Key:** the value of a *key* attribute in the new tuple already exists.
- **Referential Integrity:** a *foreign key* value in the new tuple references a PK value that does not exist in a referenced relation.
- **Entity Integrity:** the primary key value is *NULL* in the new tuple.

##### DELETE Violations:

- **Referential Integrity:** Deleting a primary key value that is referenced by other tuples in other relations

##### UPDATE Violations:

- May have **duplicate PK values**
- **Referential Integrity:** Updating a foreign key to one that is not referencing a PK from another relation 



