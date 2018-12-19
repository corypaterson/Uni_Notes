# Fundemental Algorithms & Data Structures

---

### The Stack
Basic Operations: 

        create //create an empty stack
        isEmpty //check if a stack is empty
        push //insert new item to top of stack
        pop // delete and return item on top of stack
    
Order of removal: **LIFO** - Last In First Out
Representations of a stack:
- as an **array**
    - the bottom of the stack is "anchored" to one end of the array
    - all operations are **O(1)**
- as a **linked list**
    - again all operations are **O(1)**
---
### The Priority Queue
Basic Operations:

        create //create an empty queue
        isEmpty //check is a queue is empty
        insert //insert a new item at back
        delete //delete and return item at front

Order of removal: **highest priority first**

Representations of a Prio-Queue:

In all cases *create* and *isEmpty* are O(1).
- **unordered list**
    - insert is O(1), delete is O(n)

(Need to find the element to delete with lowest priority and can just insert anywhere since unordered.)

- **ordered list**
    - insert is O(n), delete is O(1)

(Need to find the correct place to insert, and since ordered can delete from front of list)

- **heap**
    - insert and delete are O(log n)
---

### Complete Binary Trees
A complete binary tree with n nodes has:
- The **minimum possible height**

A tree of height **h** can have **at most (2^h+1)-1** nodes. Therefore the height of a complete binary tree with **n** nodes is the smallest such that **h= [log2(n+1)-1]**

-  The **maximum number of nodes at each level** (except the last).
- The nodes of the last level are as **far to the left as possible**.

PROPERTIES:
- Let **T** be  a complete binary tree.
- If **T** is of height **h**, then it has at most **(2^h+1)-1** nodes.
- If **T** ha **n** nodes, then its height is **[log2(n+1) - 1]**.
- If **T**  has **n** nodes then, the number of leaf nodes is **[n/2] rounded up**
- If **T** has **n** nodes then, the number of branch nodes is **[n/2] rounded down**
---

### Heaps

A binary **heap** is a *complete binary tree* with an **item stored at each node** and each item has a **value** (or priority).

The property of a heap:
- For **every node**, the value of its item is **greater than or equal to** the value of all items in descendant nodes (therefore the larget item is stored at the root).
- A **min-heap** is similar except the *smallest value is stored at the root*.

Operations:
        
        insert //a new item
        build //a heap containing a given set of items
        delete //the item with largest value (root)
        impose //the heap property on a particular node (all other nodes must be heaped)

Complexity of heap operations:
- Any algorithm involving O(1) steps at each level has complexity **O(log n)**
    - Holds for **insert**, **impose** and **delete**.
- Build has an easy **O(n log(n))** version (just repeated insertions) but can be done as **O(n)** too.

### Insertion

        insert item in new leaf node; //end of array
        while(item not in root && item > parent){ swap item with parent };
If an item is inserted at the bottom of the heap, we then check it with the parent and keep swapping until it is in place, this gives **O(log n)** complexity.

### Impose

        while (badItem not in leaf && badItem < largerChild){ swap badItem with largerChild };

This will occur **when deleting a node which is not a leaf**, as when deleting a node, it is replaced with the last leaf - creating a **bad node** that is out of place.

### Deletion

        swap root value with last leaf;
        delete last leaf //now root node;
        impose heap property on bad value;
        
When we delet an item, we **first swap it with the last element in the heap**, then **delete it from the end**. After this **impose the heap property** on the bad node now at the original place of deletion, the heap property will then be restored and value is deleted.
### Build

        for each(non-leaf node in bottom-to-top right-to-left order){ impose heap property on node};

### As an 'Integer Heap Class'

We take a representation of a heap with size **n** as an array of size **n** - If we take node at index **I**:

- Children of node **I**, if they exist, are nodes with index **2i+1** and **2i+2**
- Parent of node **I** is the node **[(i-1)/2] rounded down**

Therefore can write methods such as:

        get_Parent(index){
            return ((index-1)/2);
        }
        
---
### HeapSort()

This works like selection sort but is more efficient, as a heap is represented as an array, this will sort an array of integers.

        build sequence into heap;
        for items in array{
            find largest unsorted item //in index 0, O(1);
            swap it into position n-1-i //its correct place, O(1)
            reduce size of heap by 1; //O(1)
            impose heap property on position 0 //O(log n)
        }
The loop is iterated n-1 times and each iteration takes O(log n) time. Hence heapsort is O(n logn) worst case.


