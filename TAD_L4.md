# Text-As-Data
### Lecture 4 - Language Modeling
---

### Language Modeling

The task of building a **preditive** model of language. **The goal**: is to predict the *probability* of a sentence or sequence of words within a document.

A **language model** is something that specifies the following two quantities (for all words in the vocab):
- Probability of a **whole** sentence or sequence
    - Pr(w1, w2, ..., wn)
- Probability of the **next** word in a sequence
    - Pr(w(k+1) | w1, ..., wk)

##### How?

We first need to **count** and **normalize**. 

The **Maximum Likelihood Estimate**:

        The number of times a sequence is seen / the total sequence length
        Pr(w1, w2, …, wn) = #(w1, w2, …, wn) / N
        
Issues with this:
- Estimating probabilities from sparse observations is unreliable. For a new sequence that hasnt been seen before, there will be no solution.

**Markov Assumption**:
The next event in a sequence depends only on its **immediate past** (context). 

A model is often described by its **order**:

    The size of context window / n-gram length
    
EXAMPLE:

Given a sequence, [the dog barks], what’s the
conditional probability of the last word: Pr(barks|the, dog). 

- “the dog barks” occurs 56 times in a text collection
- “the dog” occurs 1190 times in a text collection
- What is the ‘order’ of this model?

Answer:

- Pr(barks|the, dog) = # (the, dog, barks) / # (the, dog)
- Pr(barks | the, dog) = 56 / 1190
-  Pr(barks | the, dog) = 0.047…
-  Trigram model (order 3)
---


### Smoothing

**Goal**: assign a low (non-zero) probablity to words or n-grams not observed in the text collection. 

Missing words should not have zero probability or occuring. Smoothing is a technique for estimating probabilities for missing (or unseen) words.

- Lower the probability estimates for words that are seen in  the document text
- Assign the "left over" probability to the estimates for the words that are not seen in the text
    - So that all probabilities sum to 1!

### Add-K / Laplace Smoothing

Assume that there were some additional documents in the corpus, where every possible sequence of words was seen exactly **k** times.

Then just increase frequencies by **k**:

    Pr(t/θ) = count(t) + k /
                ∑t counnt(t) + k|v|
    where v is the number of unique words in the vocabulary

---

### Evaluation

> A good language model should model the language well

Words that the model predicts as the next in a sequence should "fit" **grammatically** and **semantically**.

E.g. A trigram model captures more context than a bigram model, so it should be a "better" model.

We measure this:
- **Extrinsically**: measure of performance on a downstream application
    - e.g. spelling correction, speech regonition, translation etc.
- **Intrinsically**: desing a measure inherent to the current task
    - This is the challenge for language modelling  

### Entropy

**Entropy** is the measurement of the average uncertainty of information in a probability distribution. 

Informally, this is the ammount of "surprise" in each piece of information.

- A uniform distribution has high entropy because it is *hard* to predict a random draw in it.
- A peaked distribution has low entropy because it is *easy* to predict a random draw from it.

### Cross-Entropy

**Cross Entropy** H(P,Q) is a meausre of difference in two probability distributions, P and Q:
- True distribution **P**, actual sequence of words
- Predicted distribution **Q**, predicted sequence of words

It is the average negative log probability of our model for each word in a sequence.
Cross entropy >= entropy, our models uncertainty can be no less than the true uncertainty.

SEE LECTURE NOTES FOR EXAMPLE

---

### Data Compression

- A bigram model of a language could store words down at **6-bits** per word.
- A unigram model would require about **11-bits** per word. 
- A trigram gets this down to **4-bits** per word!

Better language models can also give us better data compressions.

### Preplexity

The perplexity is defined as:

    2^(cross-entropy)
    
A perplexity of **k** tells us that the model is as uncertain as if it had to choose from **k** elements with equal probability.

A *lower* perplexity means a better language model because predictions are closer to the true distribution.
---

### Practical Language Modeling issues

We introduce special START and END tokens at the beginning of a sequence. This allows us to model the likelihood of beginning or ending with a word.

We do probability computations in log space
- to avoid underflow of very small numbers
- adding is faster than multiplying
- sometimes easier to interpret
- log(p1*p2*...*pn) = log(p1) + log(p2) + ... + log(pn)





