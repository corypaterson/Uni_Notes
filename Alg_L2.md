# Sorting Algorithms
---
### Recap
Naive sorting algorithms: O(n^2) worst case.
- Selectionsort, Insertionsort, Bubblesort

Clever sorting algorithms: O(n log n) in worst case. 

- Mergesort, Heapsort (previous lecture)

The **fastest** sorting algorithm in practise is **Quicksort**. O(n log n) on average, but no better than O(n^2) in worst case (unless a clever variant is used).

---
### Comparison based sorting
No sorting algorithm that uses pairwise comparison of values can be better than O(n log n). Which is seen by using a decision tree justification.

---
### Radix Sorting

**Radixsort** uses a different approach to achieve an O(n) complexity. The algorithm has to be exploit the structure of the data, so it may be less versatile.

For the set of integers, we can treat them as a set of bit-sequences of length **m** we create **2^b buckets** where *b* is a chosen factor of **m**. The algorithm then uses **m/b iterations**. 

In each iteration: 
- Items are distributed into **2^b buckets**, where a bucket is a list
- The buckets are labeled 0,1,...,(2^b)-1
- during iteration **i** an item is placed in the bucket corresponding to the integer **b\*i-1,...,b\*(i-1)**
- At the end of each iteration the buckets are **concatenated** to give a new sequence which will be used as the starting point for the next iteration.

SEE LECTURE SLIDES FOR CODE AND EXAMPLE

### Radix Sort: Complexity
Number of iterations is **m/b** and number of buckets is buckets is **2^b**.

During each of the **m/b** iterations:
- The sequence is scanned and items are allocated buckets: O(n).
- Buckets are concatenated: O(2^b).

Therefore overall complexity is **O(m/b\*(n+2^b))**, which is **O(n)** since *m* and *b* are constants.

The Time-Space trade-off:
- Since the larger the value of *b*, the smaller the number of iterations will become, since **m/b** will be smaller. Therefore the algorithm will become faster.
- But an array of size **2^b** is required for the buckets, therefore increasing *b* will increase the space requirements.

