# Text-As-Data
### Lecture 8 - Information Extraction
---

### Information Extraction Pipeline

1. **Named Entity Recognition** - detect and classify entities
2. **Coreference resolution** - Resolve pronouns to named entities
3. **Entity resolution** - Ground entities to a representation of 'world' knowledge
4. **Relation Extraction** - Classify relationships between entities

---
### Infromation Extraction

**Goal**: Discover/extract structured information from text
**How**: by mining lots of information from a corpus
(Machine reading of text)

    Information extraction =
    segmentation + classification + association + clustering

1. Extract **entities**
    - E.g, nouns, proper-nouns etc
2. Extract the **relations** between entities
    - E.g,  contains, is_a, regulates, causes...
3. Firgure out the larger **events** that are taking place.

##### Entities 

An **entity** is a single thing or concept that exists in the world. A named concept that exists across documents. The **definition varies based on task**. 

### Goals of IE

1. Organise information so that it is useful to **people**
    - Info boxes in Wikipedia
    - Summary of facts across an entire collections of news
2. Organize information so that it is useful for **machine algorithms**
    - Data analytics
    - New knowledge: Works-for(x, y) AND located-in(y, z) à lives-in(x, z)
    - Question answering (Next lecture)
---

### Named Entity Recognition

A base level IE task. Find things, and assign them a type. Must be able to **find** and **classsify** names in text.

### Evaluation

Metrics: **precision**/**recall**/**accuracy** (per entity mention, not token).

---

### Coreference Resolution

**Goal**: resolve different **mentions** of the same **entity**.

- Mention: a single 'chunk' (often a noun phrase)
- Entity: a grounded 'thing'

Linguistic note:

**Anaphora**: expression depends on *antecedent*
- "**Sally** arrived, but nobody saw **her**"

**Cataphora**: expression depends on *postcedent*
- "Before **her** arrival, nobody saw **Sally**"

SEE LECTURE SLIDES FOR COREFERENCE EXAMPLES

---

### Relation Extraction

Parses text into structured relations to populate a database/knowledge base.

**Resource Description Framework** (RDF) triples:

    <subject><relation><object>[optional context]

### How to Extract

1. Find mentions of entites
2. Extract relations from the context of the mentions of entites

E.g:
    
    "<Barack Obama> is the <president> of the <United States>."
    (Barack Obama, head-of-state, United States)
    
### Extracting richer relations using rules

**Intuition**: 
- Relations often hold between specific entities
- located-in (ORGANIZATION, LOCATION)
- founded (PERSON, ORGANIZATION)
- cures (DRUG, DISEASE)

Named entities aren't enough to determine context, must use relations to determine exact conext:

            cure   
    Drug    prevent  Disease
            cause


---

### Classification in supervised relation extraction

1. Find all pairs of named entities
2. Decide if 2 entities are related
3. If yes, classify the relation

### Distant supervision

- Use an existing large database to get huge # of examples
- Create lots of features from all these examples
- Combine in a supervised classifier


##### Distantly supervised learning of relation extraction patterns

1. for each relation
2. for each tuple in big database
3. find sentences in large corpus with both entities
4. Extract frequent features
5. Train supervised classifier using thousands of patterns

##### Issues with this

**False positives**:
- Some entities may have multiple relations
    - lives-in(Obama, Washington)
    - works-in(Obama, Washington)
- Presence of entities alone doesnt guaruntee relation is expressed

**False negatives**:
- Knowledge bases are incomplete
- System may correctly predict a relation which currently is not in knowledge base.

---

### Summary

Information extraction extracts structured relationships from text to put into a database.

Extracted *grounded* representations of entites in text:
- Named entity recognition
- Resolution
- Coreference

Relation extraction:
- Predict structured relationships between entities

Resulting in large knowledge bases of information used by search engines and increasingly in other companies (e.g, to answer customer support questions).

