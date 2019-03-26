# Algorthimics
### Section 5 - NP Completeness
---

### Polynomial vs Exponential Time
In *general*,
- Exponential-time algorithms - **Bad**
- Polynomial-time algorithms - **Good**

When referencing "efficient algorithms", it means *polynomial* time. 
- often polynomial algorithms require some extra insight whereas,
- exponential algorithms are variations on exhaustive search

A problem is **polynomial-time solvable** if it admits a polynomial-time algorithm.

---

### NP Complete Problems

**No polynomial-time algorithm** is known for a NP-Complete problem. However if one is solvable in polynomial-time, then they all should be.

### Interactable Problems

There are two different causes of intractability (non polynomial algorithm):
1. polynomial time is not sufficient in order to discover a solution
2. solution itself is so large that the exponential time is needed to output it

We will deal with case 1:
- there are **intractability proofs** for case 1
- some decidable problems have been shown to be intractable

---

### Problem and Problem Instances

A **problem** is characterised by (unspecified) parameters. Typically there are infinite instances of a problem. 
A **problem instance** is created by giving these parameter values

An **NP-complete problem**:
- Name: Hamilton Cycle (HC)
- Instance: a graph **G**
- Question: does **G** contain a cycle that visits each vertex exactly once

This is a **decision problem**. Every instance is either a "yes-instance" or a "no-instance"

---

### Optimisation and search problems

**Optimisation problems**: find the *min* or *max* value.
**Search Problems**: find some appropriate optimal structure

NP-completeness deals with **decision problems**:
- corresponding to each instance of an optimisation or search problem
- is a fmaily of instances of a decision problem by setting 'target' values
- an optimisation or search problem can be solved in polynomial time if and only if the corresponding decision problem can

---

### The Class P

**P** is the class of all decision problems that can be solved in polynomial time. Many problems are in **P**. **P** is often extended to include search and optimisation problems.

### The Class NP

The class of all problems that are solvable in **non-deterministic** polynomial time. **P** is contained within **NP**. But the relationship beyween the two is the most nutorious unsolved question in computing science. 

---

### Non-deterministic Algorithm

A **non-deterministic algorithm** has an extra operation called a **non-deterministic choice**. An *NDA* has many possible executions depending on the values returned. 

An *NDA* solves a decision problem Π if:
- for a 'yes'-instance *I* of Π there is **some** execution that returns 'yes'
- for a 'no'-instance *I* of Π there is **no** execution that returns 'yes'

*NDA*'s can be viewd as a **guessing** stage followed by a **checking** stage. 

        START -> non-determinitic alg -> polynomial time alg -> STOP
                  'guessing stage'         'checking stage'
---
### Polynomial Time Reduction

A **polynomial time reduction** *PTR* is a mapping *f* from a decision problem **Π1** to a decision problem **Π2** such that:

For every instance we have
- the instance *f(I1)* of **Π2** can be constructed in polynomial time
- *f(I1)* is a 'yes'-instance of **Π2** if and only if *I1* is a yes instacnce of **Π1**

Write:

        Π1 𝝰 Π2

As an abreviation for 'there is a polynomial time reduction from Π1 to Π2'

#### Properties:
Transitivity:

        Π1 𝝰 Π2 and Π2 𝝰 Π3 implies Π1 𝝰 Π3

This also means that with regards to **class P**:

        Π1 𝝰 Π2 and Π2 ∈ P implies that Π2 ∈ P
        
Roughly speaking, Π1 𝝰 Π2 means that Π1 is no harder to solve than Π2

---

### NP-Completeness
A decision problem Π is **NP-complete** if:
- Π ∈ NP
- for **every** problem Π' in **NP**: Π' is polynomial-time reducable to Π

**Consequences** of the definition:
- If Π is **NP-complete** and Π ∈ P, then P = NP
- every problem in NP can be solved in polynomial time by reduction to Π
- supposing P ≠ NP, if Π is NP-complete then then Π∉P

If A problem Π1 is able to be reduced to Π2 and Π1 is NP-complete, then it can be proved that Π2 is also NP-complete. Approach as is follows:
- for any Π ∈ NP, since Π is NP-Complete we have Π 𝝰 Π1
- since Π 𝝰 Π1, Π1 𝝰 Π2 and 𝝰 is transitive, it follows that Π 𝝰 Π2
- since Π ∈ NP was arbitary, Π 𝝰 Π2 for all Π ∈ NP
- and hence Π2 is NP-complete

---

### Problem Restrictions

A **restriction** of a problem consists of a subset of the instances, of the original problem. Restrictions of a problem Π can still be *NP-complete*. 

For example: 
- a clique restricted to cubic graphs is in **P**
- (cubic graph has every vertex belonging to 3 edges)
- a largest clique has size at most 4, so exhaustive search is O(n^4)

