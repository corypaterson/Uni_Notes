# Text-As-Data
### Lecture 1 - Text Processing Fundementals
---

### What is Text?

At the lowest level, text is a string or **stream** of characters. Some characters may be *mark-up*, which can be removed with an HTML parser.

The Text Processing Pipeline:

1. Download webpage
    - Strip the HTML if necessary
2. **Tokenize** the text
3. Select tokens of interest
4. Create a **Natural Language Toolkit** (NLTK)
5. Normalize the words
6. Build a vocabulary

---

### Tokenisation

(After HTML markup is removed)

The **tokens** or *seperate terms* need to be identified.
- A sequence of characters needs to be separated into tokens (roughly "words") 
- A token is a *meaningful* sequence of characters

This may be done by splitting on punctuation, or splitting on whitespace characters.

---

### Normalization

##### Morphology:

**Morphemes** are the small meaningful units that  make up words.

**Stems** are the core meaning-bearing units. Whereas, **Affixes** are the bits and pices that are joined to steams for grammatical function.

**Lemma**: same stem, roughly the same word sense
E.g. **cat** and **cats** = same lemma

**Wordform**: the full inflected surface form
E.g. **cat** and **cats** = different word forms

##### Stemming:

The process of *reducing* inflected words to their **stem** or root form.

The output after removing affixes may not be a word:

    Computing, Computer, Computation, Compute = Comput

Porter's Algorithm is the most common English Stemmer (see lecture slides for examples).

Very fast, easy to implement and usually effective.

##### Lemmatization:

The process of *grouping* together the different inflected forms of a word to a **base form**.

Lemmatization has to find the correct dictionary headword form. Uses context to be more precise.
E.g. meeting (noun) vs meet (verb)

Process is slower than stemming.

---

### Text Processing Summary

1. Segmenting/tokenizing terms in running text
2. Normalize tokens into a normal reduced form
3. Segment long sequences of tokens (usually into sentences)


- Tokenization is easy, but hard to do well.
- It has its complications:
    - Contractions -> what're
    - Numbers -> 555,500.50
    - Multiword expressions -> rock 'n' roll
    - Useful punctuation -> m.p.h, Ph.D, AT&T
    - URLS -> http://www.google.com/
    - Runaway tokens #getbusylivingorgetbusydying

- The Penn Treebank defines one common tokenization that is used in standard NLP tasks

- Text normalization (and usually stemming) are almost always required

- Tokenization and Normalization is language specific
    - Need to detect one or more languages in the text being processed
    - Unicode and a variety of text encodings (be careful!)

---

### Text Representation

Text Collections:

For a large collection of text documents we define various properties:

- **Type** - an element of the vocabulary
- **N** - number of all token occurences (word count)
- **V** - vocabulary, the set of all types (unique normalized tokens). Stored in a dictionary.


We can represent a piece of text by the terms that occur in it. Mathematically, its a vector for each document.

**One-hot** encoding uses a vector to store 1s and 0s depending on wether a term occurs in the given document. 1 yes, 0 no. We consider this as representing eahc document as a **set** of its terms.

##### Implementing One-hot Encoding

To be able to transform documents from a stream of tokens into a one-hot encoding we need:

1. To know for each term, what its offset is in the dictionary/vocabulary
2. The dimension of the vector i.e. the size of its map

If we meet a new term while processing a new document then we add a new entry to the dictionary.

But, if we already have a **frozen** (full) dictionary, then new words are given the value 'UNK' for unknown terms.

##### Alternatives to a Dictionary

A dictionary can become very large.

One option: **truncate** the dictionary, removing rare words (most likely misspellings or unimportant words).

Another option: **hashing**. Words are directly mapped to vector indicies with a hashing function, no memory is required to store the strings of a dictionary. 

Hash collisions are typically dealt with by using freed-up memoru to increase the number of hash buckets.

This greatly simplifies implementation and **impoves scalability**.


##### Text Representation Summary

- Defined vocab and dictionary (that stores the vocab)
- Efficiently represent text as a vector
    - **one-hot encoding**
- Practiced turing a document into a vector of terms - **vectorizing** text.

---

### Set Based Similarity

Many text applications are based on comparing similarity of text (grouping tweets or new articles about same events). 

##### Jacard Similarity:

Jacard similiarity coefficient can be used to calculate the similarity of sets. It defines the size of the **intersection** *divided* by the **union** of the sample sets of vectors (vocabularies).

        J(A,B) = A∩B / (A + B) - A∩B
        
Gives a number between 1 and 0, with 1 indicating the most similar (which can then be expressed as a percentage).

EXAMPLE:

d1: "James decided to quit smoking, but it was not an easy decision"
d2: "Though it was not an easy decision, James decided to quit smoking"

        J(A,B) = 11 / (12 + 12) - 11
                = 0.84615
                = 85% similar





