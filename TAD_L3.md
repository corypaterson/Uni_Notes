# Text-As-Data
### Lecture 3 - Clustering

---

### Clustering

> How can I group a set of items by similarity? (For this course, items will be mostly text-documents).

**Clustering** is discovering the underlying structure of data by grouping similar objects together. Objects (text documents) within the same cluster are assumed to be similar.

CLustering is usually an **unsupervised** learning task. There is no labelling of the data, an algorithm will discover the clusters itself.

##### Process:

1. Derive a document representation
    - Typically a text document vector 
2. **Measure similarity** between documents
3. Apply a **clustering algorithm**
4. Check the **validity/quality** of the clustering
---

### Clustering Algorithms

The **number of clusters** and how they are *defined* vary depending on the clustering algorithm used.

##### Properties:

**Partitioning Criteria**:
 - Multi-level heirarchical partitioning is desirable
 
**Separation of clusters**:
- Exclusive - one object belongs to one cluster
- Overlapping - one object may belong to more than one cluster

**Hard vs Fuzzy**:
- Fuzzy clustering - an object belongs to every cluster with some weight between 0 and 1
- Weights sum to 1
---

### Partition Clustering

Partitions a set of **n** documents into **k** disjoint clusters. Find the partition that optimises a specific criterion. 

##### K-means Clustering Approach

**Basic K-Means Algorithm**: 

0. Choose K random numbers
1. Assign points to closest centroid
2. Recompute centroids
3. Goto 1 (until convergence)
    - Converges when cluster assignments dont change "much"

Good: Tends to converge quickly
Not so good: Sensitve to choice of initial seeds
Complexity: **O(N*K)**(N = #Documents, K=#Clusters)

### What is a Cluster Centroid?

A **cluster centroid** is a prototypical example - typically the average of all objects in a given cluster.

**Centroids** must be descriptive and distinguishing

SEE LECTURE NOTES FOR DIAGRAMS

##### K-means Summary

K means is usually the choice for an all-purpose clustering algorithm.
- Will always converge (given enough time)
- May converge to a local minimum however

Is fast and efficient
- Mini-batch modifications 
- Searched based retrieval using a centroid as a query

How do we impove the quality of a k-means clustering? 
- Pick seeds that are sufficiently far apart
- Run k-means multipole times with different seeds
- Try different values of k, then select best value

K-means produces clusters that are :
- Flat (non-heirarchical)
- Non-overlapping
- Hard assignments

---

### Clustering Conclusions

- Clustering is theorectically solid and intuitively plausible
- Clustering assumes that each document is only about a single topic
- Clustering is unsupervised entirely
- We dont have to cluster documents, we might cluster words or phrases as well.



