# Matrices and Vector Spaces
---

### Vector Spaces

ANy vector of given dimension n lies in a **vector space**, called R^n, which is the set of possible vectors of length n that have real elements. The operations of scalar multiplications, vector addition, **norm** (allows length of a vector to be measured) and **inner product** (allows angles of two vectors to be compared) exist.

Relation to arrays:
These vectors of real numbers are represented by 1D floating point arrays.

### Uses of vectors

Vectors can be:

- **composed** (via addition)
- **compared** (via norms/inner products)
- and **weighted** (by scaling)

The can represent the kind of transformations to be done to data sets. They map onto the ndarray structure so can be operated on efficiently.

### Vector Data

Datasets are commonly stored as 2D Tables. These can be seen as a **list of vectors**, each row is an observation representing a vector. I.e. lots of vectors stacked up into a 2D matrix. Because all vectors are plotted in the same vector space, we can draw **geometric conclusions** about the tabular data.

We can take this data in space and perform **geometric operations** on it, such as:
- scaling
- rotation
- flipping (mirroring)
- translation (shifting)

---

### Basic Vector Operations
Addition and Multiplication:

Elementwise additon and scalar multiplication only apply to vectors of the same dimension. (Previously defined in notes, see diagrams online or on slides).

Linear Interpolate:

        lerp(x,y,a) = ax + (1-a)y

This lets us move along the line between two vectors as a goes from 1 to 0, the result goes in a smooth line from x to y. (See notes for visual representation - fan shape).

Linear Norm:

The Euchlidean length of a vector x can be computed by using np.linalg.norm(), it corresponds to the radius of a sphere that would just touch the position specified by the vector. The **norm** is the **norm of the difference of two vectors**

Inner Product of vectors:

An inner product is the *angle* between two vectors. (related to the cosine difference) 
        
        cosø = x.y / |x||y|

For unit vectors, the bottom of the equation will be 1. So for vectors inner product is basically cos^-1(x.y)

---
### Basic Vector Statistics

These statistics can generalise the sets of ordinary real numbers.

The **mean vector** of a collection of N vectors is the sum multiplied by 1/N.

It is a **geometric centroid** of a set of vectors and can be thought of as capturing "center of mass" of those vectors

---
### Matrices and linear operations

Uses of Matrices:

Matrices represent **linear maps** as 2D arrays of real numbers. **Vectors** represent *points in space*, **Matrices** represent *operations* that do things to those points in space.

Matrix operations:
- Added and subtracted C = A + B
- Scaled C = sA
- Transposed B = A^t (exhanges rows and columns)
- Applied to vectors y = Ax
- Multiplies together C = AB 

A matrix with dimension **n \* m** has *n* rows and *m* columns (in that order!)

Matrices are **functions applied to vectors**. Like applying the function f to x: Ax = f(x) in mathematics. Specifically a *n\*m* matrix represents a function f(x) taking *n* dimensional vectors to *m* dimensional vectors. Such that all straight lines remain straigh and all parrallel lines remain parallel and the origin doesnt move.

Linearity:

        f(x+y) = f(x)+f(y) = A(x+y)= Ax+Ay
        f(cx) = cf(x) = A(cx) = cA(x)

Therefore transform of the sum of two vectors, is the same as the transform of two vectors, summed (same for a scaled vector).

SEE PAGE 43 WEEK_4 NOTES FOR MATRIX TRANSFORM EXAMPLES

**Matrix Algebra** is **linear algebra**. The addition of matrices and scaler multiplication of matrices are both **elementwise**.

### Matrix Multiplication

Multiplying two matrices is equivalent to comnposing the linear functions they represent, and it results in a matrix which has that affect.

        C=AB
        #See formulat on lecture notes
        Cij = SIG(k)[Aik*Bkj]

Time complexity of multiplication for multiplying two sqaure matrices is O(n^3). Many special forms of matrix allow for faster. Some algorithms work faster all > O(n^2) but < O(n^3).

### Composed Maps

If A represents f(x) and B represents g(x), then the product BA represents g(f(x)). **Multiplication is composition**. Means do **A to x** then do **B** to the result.

### Commutativity

The order of multiplication is important! **Matrices are not commutative**

        AB ≠ BA
        
However you can use **transpose order switching** to make this computation feasible:

        (AB)^t = (B^t)(A^t)
        also true that:
        (A + B)^t = (A^t) + (B^t)
        
BEcausew of the lack of commutativity there are actually two different multiplication operations **Left** and **Right** multiply:

        A[Bx + y] = ABx + Ay
        [Bx + y]A = BxA + yA 


### Covarience

In single dimensions the spread of data is measured by the standard deviation.

However, in multdimentional cases, we need to compute the **covarience** of every dimension with every other dimension. This is the **average squared difference** of each colum of data from the average of every colum (forms a 2D array).

It can be seen as capturing an **ellipse** that represents the dataset. The **mean vector** represents the centre of the ellipse, and the **covarience matrix** represents the shape of the elipse. 

- Mean vector -> center
- Covarience matrix -> spread
- Of a collection of points in a vector space
- Very useful summary of high dimensional data