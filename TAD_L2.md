# Text-as-Data
### Lecture 2 - Geometric Similarity & Text Distributions
---

### Bag of Words

**One-hot encoding** treats each document as a set of terms. If we count frwquencies of the words, we treat each document as a **bag**. Hence this representation is called a **Bag-of-Words**.

##### Model:

Assumption: 
>If a word occurs *lots* in a document it should imply something about what the document is about.

We can use a dictionary to keep count of term occurences:
- [0,5,0,0,9,1,1,4,0,0,0] - **dense representation**
- [2:5 5:9 10:1 11:1 12:4] - **sparse representation** (uses less memory)

We should consider documents as a **bag-of-words** rather than binary (sets). This gives us a **term frequency**. 

##### Smililarity Analysis:

The entire corpus of documents can be represented as a **document term matrix** where each row is a document vector. 

**Term Document Matrix**:

- Documents are the columns
- Terms are the rows

                D1      D2      D3
        number  1       2       1
        equals  1       0       1
        set     0       0       2
        it      0       1       0
        how     1       0       0
        
Here we can see how similar documents are by how similar the numbers are across each instance of a term in each document (across a row).

---

### Gometric Similarity

We can then plot the vectors for each document from the **term document matrix**

We use the **angle between vectors** to measure the *similarity* of two vectors. Using the angle, then means that the magnitude of vectors is not taken into account.

**Similarity** is the distance between points representing units of text. We can measure the **Cosine Similarity** by using the cosine rule:

        Cosine(D1, D2) =
        D1.D2 / (√(|D1|^2 . |D2|^2))
        
---
### Applications

All search engines use **bag-of-words** to allow searching documents (with more statistical/distance similarity measureas).

**Clustering documents** uses similarity metrics.

---

### Problems with Term Frequency

- Many most frequent words arent very useful (they dont discriminate one doc from another)

1. Many use-cases define a list of **stopwords** that should be deleted (pronouns/articles).
2. Some words might still be frequent in general within a corpus and still not discriminative
3. Some words are related: "sell" & "sells"
4. We only know which terms are present, not how they might be related: "charles" & "mackintosh"

##### Problem 1: Raw Term Frequency

The term frequency **tf(t,d)** of term *t* in doc *d* is defined as the number of times that **t occurs in d**.

We use this in cosine similarity, but it has an issue:

- A document with 10 occurences of the term is more related than a document with 1 occurence of the term.
- But it is not 10 times more relevant.

**Solution:**

The **log** frequency (**W**) of term t in d is:
        
        W = 1 + log(tf(t,d)) if tf > 0.
        otherwise W = 0

##### Problem 2: How "good" is each term?

**Problem**: All terms are considered equally important when measuring aboutness.

We need to be able to look at an entire collection of documents to see how useful a term is.

We acheive this by measuring the **document frequency** - How many documents in a given collection contain a given term.

---

### Document Frequency

**Rare terms** are more informative that frequent terms. We need to **weight items highly** if they are *rare* and *informative*.

df(t) is the **document frequency** of the term *t*: The number of documents that contain *t*.

We define the idf(inverse document frequency) of t by:
        idf(t) = log10(N/df(t))
        
---

### TF-IDF Weighting

The **tf-idf weight** of a term is the product of its **tf weight** and its **idf** weight.

        W = log(1 + td(t,d)) * log(N/df(t))
        
This is the **best known** weighting shceme in information retrieval. It *increases* with the number of **occurences** in a document and *increases* with the **rarity** of the term in the collection.

---
### Summary:

- How representative a term is of a document is not necessarily linearly related with its frequency.
- We can examine the collection as a whole for information about hwo *informative* or *discriminative* each term is.
- The key outcome is IDF (inverse document frequency). This can be combined with term frequency to give a measure of how "good" a term is.
- **Bag-of-Words** and **TF-IDF** weighting is a fundamental and widely used weighting method.

