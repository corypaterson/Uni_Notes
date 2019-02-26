# Text-As-Data
### Lecture 7 - Natural Language Processing
---

**Goal**: for computers to process or understand natural language in order to perform tasks that are useful.

NLP involves:
- **Syntax**
    - Identifying the syntacitc roles of words in sentences.
- **Semantics**
    - Worrying about the meanings of the words, phrases or sentences.
- **Pragmatics**
    - Worrying about how communicative context affects meaning.

---

### A Typical NLP Pipeline

1. Tokenization and lemmatization
2. Sentence boundary detection
3. Part-of-speech-tagging
    - Identify nouns, verbs etc...
4. Parsing (dependancy)
    - Diagramming sentences
5. Named Entity Recognition
    - Detect and classify entities
6. Coreference resolution
    - Resolve pronouns to named entities

### The Supervised ML Model Approach

**Training**:
1. Collect a set of representitive training documents
2. Label each piece of text with its label
3. Design feature extractors appropriate to the text and classes
4. **Train** a classifier to predict the labels from the data

**Testing**:
1. Receive a set of test text
2. Run model **inference** to label each piece of text
3. Appropriately output the label
4. Evaluate correctness of predicted labels

---

# Text Sequence Models
### Part-of-speech tagging

**Input**: A sequence of tokens
**Output**: An assignment of POS tags for each word in the input.

Used as an early stage in an NLP pipeline. Helps with determining the meaning behind words (e.g, 'lead').

### Hidden Markov Model

SEE LECTURE SLIDES FOR NOTES

---
# Parsing: Tree Structured Prediction

Types of parsing:
- Constituency/phase-structure
- Dependency
- Semantic/frame
 **Goal**: Find the best tree.

##### Formal Definition

> A dependency structure for a given sentence is a **directed graph** originating out of a unique and artificially inserted **root node**, which we always insert as the left most word.

Dependancy graph has the following properties:
- It is weakly **connected**
- Each word has exactly **one incoming edge** (except the root, which has none).
- **Acyclic**

### Dependancy Parsing

Given a sentence, draw edges between pairs of words, and label them. The result should be a tree.

SEE LECTURE SLIDES FOR EXAMPLE GRAPHS

---

### Transition Based Parsing

Transition parsing, builds a parse tree by a **sequence of actions** (transitions).

**Set-up** (state):
- A **buffer** initialized with the words
- A **stack** to store state:
    - words under consideration for more edges
- Dependency **arcs** (edges)
    - The partially-constructed tree

**Arc-Standard** pasring:
- **shift**: pop from buffer, push to stack
- **Left-arc**: add left edge (removes child from stack)
- **Right-arc**: add right edge (removes child from stack)

### Analysis:

For N tokens:
- O(N) shift operations (one for each token)
- O(N) reduce operations (one for each edge)
- **O(N) = linear time parsing** (if the right transitions are chosen).

Actions are irreversible. Therefore the coreect action must be chosen every time (could be more than one correct transition).

SEE LECTURE NOTES FOR EXAMPLE


### How to choose transitions

Treat this as a **search problem**.

**Goal**: complete the parse tree
**Path**: sequence of actions (transitions)
**Best**: highest scoring (according to model score)
Should pick the highest scoring transition at each step. 

---

### Parsing Summary

Syntactic parsing aims to find **phase-structure** in sentences and word-word relations.

**Dependency parsing**:
- Word-word relations 
- Parsing generates dependency trees by predicting edges or pruning edges
- Transition based-parsing formulates adge prediction as a classification task

### NLP Summary

NLP provides us with tools to model language beyond simple lexical features.

Sequence models like HMM and CRFs allow us to label break apart patterns in language:
- Part-of-speech tags
- Sentence or word breaks
- Patterns in language discourse

**Tree structured prediction**:
- Predict complex patterns in language
- Critical for advanced applications (upcoming lectures).









