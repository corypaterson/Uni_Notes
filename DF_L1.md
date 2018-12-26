# Arrays
---
The fundemental data type for the DF course is the **multidimensional numerical array**. Also called *ndarrays* or sometimes called *tensors*.

### Why use arrays?

- An *image* is a 2D array of brightness values
- A *sound* is a 1D array of sound pressure levels
- A *video* is a 3D array of brightness values (x,y and time)

If we want to edit this data, it is very easy through simple array operations to do so (brightening a video, mixing together two sounds, cropping an image etc.)

**3D Graphics** usually involves manipulating geometry, which as made up of points -- **vertices** -- typically with an [x,y,z] location. These can be **scaled**, **moved**, and **rotated** by array operations on their vertices arrays.

### Numerical Arrays

These array are both **compact** (stored in memory efficient way) and **computationally efficient** as it is possible to write code that manipulates arrays extrememly quickly 

The practise of writing code which acts on arrays of avlues simulatenously is called **vector computation** (special casse of *parallel computing*).

### Vector, Matrix Tensor 

**ndarrays** can have different *dimensions* 
- 1D array is called a **vector**
- 2D array is called a **matrix**
- (3+)D array is called a **tensor**

The **number of dimensions** in an array is sometimes called it **rank**

- A scaler is rank 0
- A vector is rank 1
- A matrix is rank 2
- And so on...

>Typically tensors do not go above **6 Dimensions** as they dont have many real world applications, and are not memory compact.

### Array Operations

**Array Transformations**
- **Arithmetic**, can be used in arithmetic expressions (multiplying every element by 2)
- **Indexing and Slicing** specific parts of arrays (selecting the top half of a matrix)
- **Generation**: zero arrays, identity arrays, meshgrids, random arrays (generating a vector of 200 evenly spaced numbers from 0 to 1)
- **Rearranging**: reshaping, unravelling, stuck together, repeated, rotated and flipped (joining together two (same length) vectors into one matrix)
- **Order Expressions**: can be sorted, shuffled and reindexed
- **aggregate functions**: operations to work on groups of numbers (like min, max, mean)

**Mathematical Operations**
- **Vector operations**: apply geometric effects to vectors (dot product, cross product, norm)
- **Matrix Operations**: linear algebra operations (multiplication, transpoose, inverse, matrix exponentials, decompositions)
- **Signal Processing**: convolution, Fourier transform, numerical gradients, cumulative sumattion

### Statically typed 1D arrays

**ndarrays** represent sequences. However arrays are not like lists as they have:

- fixed, predefined size
- fixed, predefined type
- they can only hold numbers
- they are inherently multidimensional
- they are required to be "rectangular" (same number of columns in each row)
---

### NUMPY

Every array is characterised by the **dtype** and its **shape** (dimensions). The shape is always described in order *rows* then *columns*.

**Indexed form zero**, so element [0,1] of an array means *first row, second column*

### Creating Arrays

Converting and Copying: np.array()

        np.array() 
        //takes a sequence of data and converts it into an array

This can take any sequence, including another ndarry so np.array() can be used for copying.

When creating, arrays should never be *ragged* always **rectangular**!

Other methods for creating arrays are:
- np.zeros(shape)
- np.ones(shape)
- np.full(shape, value)
- np.random.randint(a,b,shape) - random ints between a and b
- np.random.uniform(a,b,shape) - random floating points between a and b

### Ranges

**Arange:**
**np.arange()** creates a vector with increasing values along a range.
- np.arange(end)
- np.arange(start, end)
- np.arange(start, end, step) - step can be negative and/or fractional

**Linspace:**
**np.linspace(start, stop, steps)** is a better alternative as it is parameterised better.

**Loading and saving**

Huge number of ways to store and recall arrays:
- CSV in text files (Comma Separated Values)
- Binary formats 
- Specialised scientific data formats (HDF5)
- domain specific formats (png, jpeg, mp3, mp4)

        np.loadtxt(fname)
        np.savetxt(arr, fname)
        
### Slicing and Indexing

**Indexing begins at zero**

To slice an array it is done in the format:
        arr[start : stop : step]
        //any part can be omitted
        
- no colon, specifies an index
- one colon specifies a range
- two colons specifies a range with a step
- if *start* is missing, defaults to 0
- if *end* is missing, defaults to last element 

**Negative indices** mean **counting from the end**, so x[-1] is the last element.

**Slicing** does not change the rank of an array, it selects a rectangular subset with the same number of dimensions.
**Indexing** reduces the rank of an array. It sepects a retangular subset where one dimension is a singleton and removes that dimension.

**Boolean Tests:**

We can do tests like greater than, less than on arrays and the result is a boolean array with the same shape as the original array

### Transposition

A transpose exchanges rows and columns (not the same as 90º rotation!). Transpose of x is **x.T**.

Has no effect on 1D array, and it reverses the order of all dimensions in >2D arrays.

As well as transposition we can *rotate* and *flip* arrays with single operations.

### Tiling


When we need to repeat arrays, we **tile** them:

        np.tile(a, tiles)
        //repeats a in the shape given by tiles
 They are tiled on a **specific axis**.
 
### Boolean Indexing

We can use a boolean array to index and select elements from a numerical array EG:

        x = [1,2,3]
        y = [true, false, true]
        x[y] = [1,3]

---
### Arithmetic on Arrays

Basic arithmetic is computed *elementwise*. This means a function is applied to each array element. For example:

        x + y + 2
        x=[1,2,3,4]
        y=[0,1,2,3]
        x+y=[1,3,5,7]
        x+y+2=[3,5,7,9]
        
These operations can be used to alter sounds and images when applied to arrays representing these, to up the pitch of a sound, simply add an integer value to each value in the sound array etc.

### Broadcasting

So far, **elementwise arithmetic** must be done on **arrays with same shape**.

But *Broadcasting* is the way in which arithmetic is done when arrays are of different shape.

- If one operand is an array with fewer dimensions than the other, then if the *last dimensions* of the first array match the shape as the second array, operations are well-defined (valid)

### Reduction

**Reduction** is the process of applying an operator or function with two arguments repeatedly to some sequence.

We can reduce on coloumns, rows or rows and columns. If we reduce [1,2,3,4] with the + operator, the result is 10.

Reduce on columns [[1,2,3,4],[1,2,3,4]] = [2,4,6,8]

Reduction is an **aggregate** function.

An *aggregate* function is one that processes an entire array and returns a single value which summarises the array in some way.
- np.any is reduction with logical OR
- np.all is the reduction with logical AND
- np.min is the recduction with min(a,b)
- np.max
- np.sum is reductio with +
- np.prod is reduction with *
- np.mean
- np.std

### Accumulation

The sum of an array is a single scalar value. The **cumulative sum** or **running sum** is an array of the same size which stores the result of summing up every element untik that point.

Accumulation of [1,2,3,4] with + is [1,3,6,10]

- np.cumsum is accumulation of +
- np.prod is accumulation of *
- np.diff is accumulation of - (one less output than input)

This needs to have an axis specififed!

### Finding

These are functions **which find indicies** that satisfy criteria.

- np.argmax() finds the index of the largest elemet
- np.argmin()
- np.argsort() finds indicies that would sort the array back into order
- np.nonzero() finds indicies that are non-zero (or True, for boolean arrays)

Findind indicies is good for cross referencing across multiple arrays.
