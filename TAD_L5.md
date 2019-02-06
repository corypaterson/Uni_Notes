# Text-As-Data
### Classification 1
---

> **Classification**: the task of predicting which or a *predefined* set of classes an object belongs to.

### Types of classification

- **Binary**: each item belongs to exactly 1 out of 2 classes.
- **Single-Label Multi-Class**: Each item belongs to exactly 1 out of >2 classes.
- **Multi-Label Multi-Class**: Each item can belong to 0,1 or Many classes


---

### Document Classification

We need a **training set** of example documents for which we know their pre-defined classes. Documents in this set must have **associated class labels** to tell the classifier which class the document is in.

Usually this **training set** is labelled by human 'assessors', which is very resouce heavy - consistency is important so there miust be **clear classification guidelines**. 

##### Classification Process:

- Annotate data to create a **training set**
    - Labels must be assigned accurately and consistently
    - Larger set the better
- Identify the set of important features, and extract those from the documents
- The classifier will then **learns** a classification model from the training set
- And applies it to **unseen** documents.

##### Formal Spec:

**Input**:
- A document **D** 
- A fixed set of classes **C = {c1, c2,...,cn}**

**Output**: 
- A predicted class **c -> C**

**Goal**:
- Learn a function **f(d)->C** where **f** is a *categorization function* that takes a **feature vector** and whose range is **C**.


### Types of Features
- Binary: TRUE or FALSE (1/0)
- Nomial: UGT, PGT
- Ordinal: Categories with ordering e.g. small, medium, large
- Continuous: i.e. numerical

TEXT MUST BE VECTORIZED BEFORE USED IN A CLASSIFIER.

---

# Important Classifier Types
### Categories

**Geometric**: 
- k-nearest neighbour
- Support Vector Machines

**Probabilistic**: 
- Naive Bayes
- Logistic Regression
- Neural Networks

Descision trees can also be used.

---
### Nearest Neighbour

Basic idea: If it walks like a duck, quacks like a duck, then its probably a duck

It computes the vector distance and decides which training record the test case is "nearest" to.

**Requirements**: 
- The set of stores instances.
- A distance metric to compute the distance between instances.
- The value of **k**, the number of nearest neighbours to retrieve.

**How it works**:
- Compute a distance to other training instances,
- Identify **k** nearest neighbours,
- Use class labels of nearest neighbours to determine the class label of unknown instance.

##### Discussion:

- K-NN classifier is a 'lazy learner'
    - doesnt build models
- It doesnt learn the importance of the features in performing the classification
- Scaling issues
    - Attributes may have to be scaled to prevent distance measures from being dominated by a single feature

Feature scaling is used by many classifiers. Allows them to be more easily comparable across instances, provides separation between 'close' feature values.

---

### Naive Bayes

Is a **probabilistic** classifier based on *Bayes rule*. 

It assigns a probability to each document **d**, for each class **c->C** based on the probability of the class **generating** that document. 

1. Assumes a **distribution of features**
2. 'Naively' assumes that the features are **conditionally independant**

We have to estimate: 
- The probabiltiy of observing class **c** in the collection **P(c)**
- The probability that document **d** is observed given the class is known to be **c**. 

Issues with Naive Bayes:

- We often use **one hot encoding** representation for documents
- **Word n-grams** are often used as features
    - Therefore *negation* can be hard to handle
- Use other features besides word counts
    - Use a manual dictionary of 'bad' and 'good' words
    - Add is_bad or is_good as features in a vocab
    - Allows us to incorporate external/manual knowledge

##### Summary: 
**Adv**: 
- Fast and efficient
- Probabilistic
- Interpretable
- Simple
- Often fairly effective
- Few (if any) parameters: **robust**

**Disadv**: 
- Sensitive to errors on rare words
- Assumption of one class per document
- Weak on rare categories
- Weak on very large and noisy feature sets
- Biased due to independance assumptions

---

### Logistic Regression

Generalization of **Naive Bayes** that learns the conditional probability: **P(Y | X)**

Logistic regression is designed as a *discriminative* **binary classifier** that outputs the probability that the input instance is in the "1" class.

        P(x) = 1 / (1 + exp(-xB)
        
Where **x=(x1,...,xm)** is the vector of features for an instance and **B** is the vector of **feature weights**.

>The feature weights are learned iteratively using an optimization method such as a stochastic gradient descent.

Summary:

**Adv**:
- The most widely used general purpose classifier
- Does better than NB cause it can deal with dependancies between features
- Should always perform **as least as well** as Naive Bayes
- Easy to incorporate arbitrary features
- Can be scaled to very large datasets

**Disadv**:
- May need more data than NB to learn effective model weights
- **It can overfit** on very sparse data so is often used with *regularization*
    - Regularization penalizes models with many high weight features
    - Simpler models are better than more complex models
    - Common types of reularization are "L1" and "L2"

---

### Support Vector Machines

Is a *discriminative* **geometric** classifier. Tries to find a **hyperplane** that separates the classes by **maximal margin**

Summary:
**Adv**: 
- Nice theoretical guaruntees
- SVM typically outperforms logistic regression
- Fast on small/medium datasets
- No assumption of distributions
- Few parameters to tune

**Disadv**:
- Need to select a kernel
- Need to tune kernal hyperparameters
- May be slow, depending on kernel
- Need regularization
- Some kernels dont scale to large datasets
- Not all kernels are probabilistic
- No easy solution to multiclass problem

---
### Decision Tree Models

A flow chart-like tree structure:
- Internal node denotes a test on a feature
- Branch represents an outcome of the test
- Leaf nodes represent class labels or class distribution

Descision tree generation:
- Phase 1: **Tree Construction**
    - At start, all the training examples are at the root
    - Partition examples recursively based on selected attributes
- Phase 2: **Tree Pruning**
    - Identify and remove branches that reflect noise or outliers

Summary:
**Adv**:
- Cheap to create
- Fast classification
- Interpretable for small trees
- Comparable accuracy
- Handles diverse features

**Disadv**: 
- Unstable: small change in data leads to very different tree
- Less accurate than other methods
- Can be complex for large trees
- Spliting criteria not perfect for all types of data

