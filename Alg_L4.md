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
