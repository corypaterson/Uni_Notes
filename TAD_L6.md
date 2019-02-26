
# Text-As-Data
### Lecture 6 - Word Embedding
---
# Evaluation of Classification Effectiveness
---
### The Need for a Dataset

We need a **dataset** of example instances for which we know their pre-defined classes. Documents in this set must have **associated class labels**. 

These are then split into training and testing sets:

- For **training**: 
    - the class labels tell the classifier the document's class.
- For **testing**:
    - the class labels allow us to evaluate the classifier's predictions

### Evaluation

1. **Train** a classifier to predict the relevant classes using the set of identified document features
2. **Evaluate** the classification effectiveness by *making predictions* on a set of data from the dataset **for which the actual labels are known**.
3. **Analyse** the classifier's predictions to develop improved features and *re-train*.

We must evaluate with documents that the classifier **has not seen before** but that we know the correct labels for.

You can construct a **contingency table** by counting correct/incorrect predictions, then select an appropriate evaluation measure for the type of classification task.

##### Precision & Recall for evaluation metrics

**Precision**:
- 'exactness', what % of instances that the classifier labeled as positive are actually positive.

**Recall**:
- 'completeness', what % of positive instances did the classifier label as positive.

---

### Classification Metrics

For **single-label multi-class**, Accuracy (a count of correct predictions) is applicable as a metric.

**Multi-label multi-class classification** is performed as multiple binary classifications. Uses **Microaveraging** and **Macroaveraging**.

##### Micro-averaging
Sum the like cells of the contingency tables across classes before calculating. Gives equal weight to each **instance**.

##### Macro-averaging
Calculate for each binary class and then take the average. Gives equal weight to each **class**.

SEE LECTURE SLIDES FOR CLASSIFICATION SUMMARY TABLE

---

# Word Vectors
### Representing words using their contexts

When a word **w** appears in a text, its context is the set of words that apear nearby (within a fixed-size window).

The shorter the windows, the more **syntactic** the representation:

    ± 1-3 very syntacticy

The longer the windows, the more **semantic** the representation:

    ± 4-10 more semanticy
    
Culster Vectors should be used to visualise similarity in co-occurence matrices.

Word co-occurence vectors are:
- **long**
- **sparse** (most elements are 0)
- Storing and making computations using such sparse vetors is problematic

We need to make the vectors **shorter** and **more dense** to be used in machine learning.

---

### Word vectors

We build a dense vector for each word, chosen so that it is similar to vectors of words that appear in similar contexts.

Can use **Singular Value Decomposition** (SVD) and **Neural Language Model** (prediction based models) to get short dense vectors.

### Truncated SVD

1. Perform SVD on Word-Word co-occurrence matrix
2. Each row of W matric is a k-dimensional representation of each word
3. K might range from 50 to 1000
4. Generally we keep the top k dimensions, but some experiments sugest that gettign rid of the top 1 dimension or even the top 50 is helpful.

### Prediction-based models

- Leard embeddings as part of the process of **word prediction** (language modelling).
- Train a neural network to predict neighbouring words.
    - This then learns dense embeddings for words in the training corpus

Adv:
- Fast, easy to train (much faster than SVD)
- Avaliable online
- With sets of pre-trained embeddings

Word embeddings caputre relational meaning:

    vector(‘king’) - vector(‘man’) + vector(‘woman’) ≈ vector(‘queen’)
    
    vector(‘Paris’) - vector(‘France’) + vector(‘Italy’) ≈ vector(‘Rome’)
    
### Problems?

- Words that do not appear in the vocabulary
    - Stop words might have been removed
    - Or vocab may have been truncated to remove rare words
- UNK words are all mapped to one entry in the vector

SEE LECTURE SLIDE (69) FOR INFO TABLE







