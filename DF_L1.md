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
- 
