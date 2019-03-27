# Strings and Text Algorithms
---
### Text compression

>A special case of **data compression** to save *disk space* and *transmission time*. This must be **lossless** i.e. the original must be **recoverable without error**.

>Examples of this include: compress, gzip (unix), ZIP (windows).

**Compression ratio**: **x/y**, where **x** is the size of the compressed file and **y** is the size of the original file.

From the *compression ratio* you can then work out the **percentage space saved**: (1- *compression ratio*)*100%

There are two main methods of compression **statistical** and **dictionary**.

---
### Statistical - Huffman Encoding

This is now lesser used, since **dictionary methods are more effective**.
- A fixed (ASCII) code is replaced by a **variable length** code for each character
- Every character is represented by a unique codeword (bit string).
- Then frequently occuring characters are represented by shorter codewords

No codeword will be the prefix of another codeword, which allows for unambiguous decompression.

Huffman encoding is **based on a binary tree**:
- Each character is represented by a leaf node
- The codeword for a character is given by **the path from the root to the appropriate leaf** (left-branch=0, right-branch=1)
- The characters are arranged in a binary tree based on their **frequencies** occuring in the text.
- Therefore most occuring characters will have shorted paths (01 instead of 0111001), hence taking up less space more often.

### Huffman encoding - Algorithmic Requirements

Building the Huffman tree (with text length **n** and distinct characters **m**): 
- O(n) time to find the frequencies.
- O(m logm) time to construct the code (while using a heap to store nodes).
    - Build heap where nodes are characters/frequencies takes **O(m)** time. 
    - Find and remove two minimum weights **O(log m)** time.
    - then insert new weight (sum of minimum weights) **O(log m)** time.
- Therefore **O(n + m\*logm)** overall.

Since **m** is essentially a constant, it is really **O(n)** time.

Compression and Decompression are both **O(n)** time assuming **m** is constant.

The **problem** with Huffman encoding: **some representation of the tree must be stored with the compressed file**.

>An alternative to storing the tree is to use adaptive Huffman encoding, where the same tree is built by the decompressor as charcters are encoded/decoded. This will slow down compression and decompression (But not by much if done right!)

---
### Dictionary - LWZ Compression

This is the basis of unix gzip compression.

The dictionary is a **collection of strings**
- Each with a *codeword* that represents it
- the codeword is a *bit pattern*
- But it can be interpreted as a non-negative integer

The dictionary is built **dynamically** during compression (and also during decompression). 
- The initial dictionary will contain all the single characters in the string
- When encoding a character, it looks left in the string and if (char + charToLeft) is not in the dictionary
- It **adds that sequence to the dictionary**
- Next time that sequence comes along it can be represented as a whole by one integer

SEE LECTURE NOTES FOR ALGORTHM

### LWZ Variants

**Constant codeword length**: The dictionary will have a fixed capacity, so when its full - just stop adding to it and use the current amount of codewords for sequencies

**Dynamic codeword length**: Start with reasonable codeword length (say 8), then when dictionary is full, just add 1 to codeword length which DOUBLES the ammount of codewords avaliable

**LRU Version**: When dictionary is full and codeword length at max - current string replaces **L**ast **R**ecently **U**sed string in dictionary

Complexity of compression and decompression both **O(n)** for a text of length **n**. As it essentially is one pass through the text.

---

# Strings
### String Comparison

How similar, or different are two strings? 
OR
Given two strings, of lengths *m* and *n*, what is the **smallest number of basic operations** needed to transform one string to the other. 

**Basic Operations**: 
- *insert*, a single character
- *delete*, of a single character
- *substitute*, one character by another

> The **distance** between two strings **s** and **t** is defined as - "the smallest numberof basic operations needed to transform **s** to **t**.

String comparison algorithms use **dynamic programming**, the problem is solved by building up solutions to sub-problems of ever increasing size. 

LOOK AT YT VID FOR STRING COMPARISON ALGORITHM

---

### String/Pattern search

The basic string searching problem:
- given a text *t* (of length *n*) and a string/pattern *s* (of length *m*)
- Find the position of the first occurence of *s* in *t*
- usually *n* is large and *m* is small

---

### Brute Force Algorithm

Given a text *t* and a string/pattern *s*, find the position of the first occurence (if any) of *s* in *t*. 

Basic algorithm (exhaustive search):
- set the current starting position in the text to be zero
- compare text and string characters left-to-right until:
    - entire string is matched
        - end
    - character mismatches
        - advance starting position in the text by 1, and repeat
- Continue until a match is found or the text is exhausted

##### Complexity:
Worst case is **O(mn)** where m is length of text and n is length of pattern. Often just *1* comparison is needed to show a mismatch, so can expect **O(n)** on average.

---
### KMP Algorithm

The **Knuth-Morris-Pratt** algorithm. 
Complexity is O(m + n) worst case.

Wors as an **on-line** algorithm:
- it removes hte need to 'back-up' in the text
- involves pre-processing the string to build a border table
- border table: an array **b** with entry **b[j]** for each position *j* of the string
- If there is a mismatch on *j*:
    - we remain on the current text character
    - the bored table tells us which string character should next be compared with the current text charcter. 

##### Definitions for KMP:

A **substring** of string *s* is a sequence of consectutive characters of *s*. 
- if *s* has length *n*, then **s[i...j]** is a substring for *i* and *j*
- 0 <= j <= j <= n-1

A **prefix** of *s* is a substring that begins at position 0.
- **s[0...j]** for any *j*
- 0 <= j <= n-1

A **suffix** of *s* is a substring which ends at position n-1.
- **s[i...n-1]** for any i
- 0 <= i <= n-1

A **border** of a string *s* is a substring that is both prefix and suffix and cannot be the string itself.
- e.g. **s = acacgatacac**
- **ac** and **acac** are borders

1. The algorithm goes through the text until it hits a mismatch character. 
2. It then checks to see whether or not the substring of the pattern until the mismatch has a **suffix which equals the prefix** (or a border)
3. If yes, the algorithm will continue searching the text, from the end of the prefix.
4. If no, the algorithm will start again from the start of the pattern, searching the text from the index after the mismatch character

#### Complexity:
- KMP can run in O(n+m) time
- O(m) for setting up border table
- O(n) for conducting the search

---

### Boyer-Moore Algorithm

Almost always faster than brute-force and KMP. Usually many characters are skipped without even being checked. The pattern is scanned **right-to-left**. 
##### Basic algorithm:
- When checking through text **t** for pattern **s**
- If a mismatched charcter (bad character rule):
    - check that character is not contained elsewhere in **s**
        - If its there, align that character with original mismatch
        - If not, align start of **s** with the next character
        - Begin next check
- If there is a match of characters, and then a mismatch (good suffix rule)
    - check through **s** for occurence of matched substring
        - If there, align with substring
        - If not, align start of **s** with the next character in text
        - Begin next check

