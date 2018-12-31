# Computational Linear Algebra
---

### Graphs as Matrices

(Like in Algorithmics 1)

We map an edge to a 1 in a v*v matrix where v is the number of nodes in a graph.

Basically an **adjacency matrix**

SEE PAGE 3 OF WEEK_5

---
### Computing Graph Properties

Once we have this binary matrix we can compute:
- The *out-degree* of each vertex (number of edges leaving the vertex)
    - the sum across the **rows**
- The *in-degree* (edges entering vertex)
    - the sum across the **columns**
- If the matrix is **symmetric** (equal to its transpose) the graph is **undirected**.
- A directed graph can be converted to an undirected one by computing A + A^t 

- If there is a non-zero diagonal, then there are vertices with edges to themselves

This adjaceny matrix can be upgraded to include edge weights. Instead of binary 1s, use weight values.

---
### Stochastic matrices

We can think of graphs as defining flows of "mass" through a network of vertices.

- If total flow out of a vertex is > 1, it is a **source** of weight (manufacturing things). 
- If the total weight out of a vertex is < 1 then it is a **sink** (consuming things).
- If the total flow out is exactly 1, then the mass is conserved by the vertex, it only ever *reroutes* things.

If a graph is conserving, then its adjacency matrix will be **stochastic**.

There are three kinds of stochastic matrix:
- **right stochastic**: each row sums to 1
- **left stochastic**: each column sums to 1
- **doubly stochastic**: both rows and columns all sum to 1

A stochastic matrix represents a graph where as much stuff that goes into the graph, comes back out of the graph and no node produces or consumes resources. **Doubly stochastic** means if the flow were reversed, it would still be a conserving graph.

### Some new matrix operations

- Exponentiated C = A^n, repeats the effect of the matrix
- Inverted C=A^-1, undoes the effect of the matrix
- We can measure properties of 'A' numerically including, the **determinant**, **trace** and **condition number**.


### Matrix Powers

        A^2 = AA
        A^3 = AAA
        A^n = AA...n

This is the **repeated application** of a matrix (can only be defined for square matrices).

Therefore we can ask, *What about in a week's time?* We simply find this by applying the matrix 7 times, or raising it to the power of 7.

> If **x** represents a vector of package numbers and **A** is the flow of packages around depots in a company to find out how many packages will be flowing in a week's time: **x(A^7)**. To find out how many in an hour: **x(A^1/24)** and so on.

### Decompositions

Whole numbers can be factored into their prime factors:
> 30 = 2 * 3 * 5

The is a **decomposition** of a mathematical object. The same can be done to matrices. Matrix decompositions usually involve splitting up matrices into simpler objects like *vectors* or *special form* matrices.

Can be used to:
 - analyse datasets represented as matrices
 - analyse the effect of linear maps
 - perform matrix computations efficiently
 - Compute interesting matrix functions like the square root, log or inverse of a matrix.
 
All of Google was built on this concept and Netflix uses is this for reccomendation algorithms!

### Fixed Points

A **fixed point** is any point of a function f(x), where f(x) = x. Like x^2 has fixed points at x=0,1.

One way to find fixed points is to choose some random *x*, then apply the rule **x=f(x-1)** repeatedly, not garunteed to find all fixed points but will often find stable fixed points.

---
### Eigen Problems

Matrices represent a **linear map**, using this on a vector space is called a **linear transformation**. Linear Transforms sometimes have a close analogue of fixed points. These are called **eigen values** and **eigen vectors**.

> Its easier to think of eigen as the "fundemental characteristics of matrices" - fundemental vectors and fundemental values.

### The Power Iteration Method

Power iteration is the approach of repeatedly taking the result of a transform **Ax**, and applying that to **A**. 

In order for this not to expload in value or collapse to zero, it must be normalised with the L∞ Norm at each step [SEE WEEK 5 PG 23 FOR FORMULA].

Regardless of the vector started with, it will reach the **leading eigen vector**, which satisfies Ax so that **A** maps the vector **x** onto a pure scaling operation (no rotation or skewing). The scaling value of this operation is called the **leading eigenvalue**.

        Ax = nx
        where A is a matrix transform
        and n is a scaling factor

### Eigen Spectrum

The **eigenspectrum** is just the sequence of absolute eigenvalues, ordered by absolute value. This *ranks* the eigenvalues (and their matching eigenvectors) in order of "importance".

### Eigenvectors of the covariance matrix

The covariance matrix is the somehow represented by an ellipse which covers the data (loosely speakling). The **eigenvectors** of a covariance matrix are called the **principal components**. They show in which ways the data varies most. The principal components disentangle linear correlation in the data. 

The direction of the principal component is given by the eigenvector x, and the length is given by 1/√n where n is the scaling factor.

### Summary of Eigen Problems

- Eigenvectors only exist for square matrices
- For these few specific vectors, **the operation of A only scales the vector** (doesnt rotate or scale it).
- The **eigenvalues** of A are factors n, that match each vector
- These can be computed algorithmically by using the **power iteration algorithm** (finds the leading vectors and values).
- If we have a set of eigenvectors and values, we can reconstruct the matrix.

### Eigenvectors/values tell us?

- If a matrix has any **zero eigenvalues**, the the correspoding vectors get "sqaushed flat" in the transform. Tells us that **A is singluar**.
- Eigenvectors corresponding to **larger eigenvalues**, are more "important", represent the ways that **data will be stretched most**.
- We can summarise a large matrix A with a few leading eigenvectors, this is a **truncated** approximation to the original matrix.
- If a matrix A is applied repeatedly to some vector **x** it will be stretched along the largest eigenvectors. The **eigenspectrum** being the order of eigenvalue (largest first).
- If the eigenspectrum is **relatively flat**, **A** represents a transform that stretches nearly **equally in all dimensions**.

---

### Trace and Determinant

Trace:

The **trace** of a square matrix can be computed from the sum of its **diagonal values**: 

        Tr(A) = a(1,1) + a(2,2) + ... + a(n,n)
        
It is also equal to the sum of its **eigen values**. 

- Thought of as measuring the **perimeter** of the paralleltope of a unit cube, transformed by the matrix.

Determinant:

The **determinant** is thought of as the **volume** of the parallelotope if a unit cube transformed by the matrix.

- Meauses how much space expands of contracts after the linear transform.

It is equal to the **product of the eigenvalues** of the matrix.

If any eigen value is *zero* then the determinant will also be *zero*. This means the transform collapses to 2D and **cannot be reversed** therefore information is lost.

### Definite or Semi-definite?

- **positive definite** if all eigenvalues are > 0
- **negative definite** if all eigenvalues are < 0
- Add **semi-** if these are >or< = 0

---
### Inversion

Quick Recap:
- scalar multiplication cA
- matrix addition A + B
- matrix multiplication BA
- matrix transposition A^t

**Inversion**:

- (A^-1)(Ax) = x
- (A^-1)A = I
- (A^-1)^-1 = A
- (AB)^-1 = (B^-1)(A^-1)

Inversion is only defined for certain kinds of matrices. The equivalent of **matrix division**, is *left-multiplication by the inverse*.

Is only for **Square Matrices**. If it is taken from a non-quare matrix, then the transform is irreversible because dimensions n will map to m (if square, will map to n).

Singular and Non-Singular:

- Matrix with det(A) = 0, is called **singular**
    - has no inverse.
- If you can take the inverse, it is called **non-singular**.

The inverse can be used to *undo* effects of a matrix transformation.

### Time Complexity

Matrix inversion, for general matrices, takes **O(n^3)** time. It can be *proved* that no general matrix inversion algorithm can ever be faster than **O(n)**.

For faster inversion, matrices like this can be used:
- Orthoganal matrices: O(1) = A^t
- Diagonal matrices: O(n) = 1/A
- Positive-definite: O(n^2)
- Triangular matrices: O(n^2), invertible by elimination algorithms

### Singular value decomposition

**Eigendecompositions** apply only to diagonalizable matrices (subset of square matrices). 

The **singular value decomposition** is a general approach to decompose any matrix A. It splits **any** matrix up into **three** matrices:

        A = UWV

where :
- A is any m * n matrix
- U is a **square orthonormal** m\*m matrix (called **left singular values**)
- V is a **square orthonormal** n\*n matrix (called **right singular values**)
- W is a diagonal m\*n matrix, whose diagonal is the **singular values**

The **SVD** is the same as:
- taking the eigenvectors of (A^t)A to get U
- taking the square root of the *absolute* value of the eigenvalues of (A^t)A to get W
- taking the eigenvectors of A(A^t) to get V

Once the matrix is factorised into these three matrices, many operations are trivial:

Inverse:
 
Once we have the **SVD**, the inverse of a matrix can be done:
        
        (A^1) = (V^t)(diag(1/W)^t)(U^t)

Which can be done in O(n) time.

### Singular values

The singular values in the diagonal **W** matrix show essential aspects of a linear transform:

- The **rank** of the matrix is the number of non-zero singular values.
- If the number of **non-zero values** is **equal to the size of the matrix**, then the matrix is **full rank**.
    - This matrix will have non-zero determinant and will be invertible
    - The rank tells how many dimensions the parallelotope will be after the transform.
- If a matrix is *not* full-rank, then it has **deficient rank**.

The **condition number** of a matrix is the ratio of the largest singular value, to the smallest singular value (only for full rank matrices).
- Small condition number means **well conditioned**.
- Large condition number means **ill-conditioned**
- The more ill-conditioned the condition number, the more likely to cause numerical issues (floating point round off).

We can think of condition number as a measure of how-close a non-singular matrix is to being singular.

### Whitening

**Whitening** removes all linear correlations within a dataset. It is a *normalizing* step used to preprocess data before analysis to standardise data.

Given dataset matrix X:

        white(X) = (X-u)C^1/2

Where *u* is the **mean vector** and *C* is the **covariance matrix**.

This:
- centers the data around its mean, so it is **zero mean**
- "Squashes" the data so that it is spherical and has **unit covariance**

Taking the inverse square root would be incredibly complicated if we did not have the SVD.

### Low Rank Approximations

See movie reccomendation example in lecture notes.