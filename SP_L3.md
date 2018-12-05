# Memory and Pointers
---
### Computer Memory
>Oxford Dictionary: "the part of the computer in which data or program instructions can be stored for retrieval."

We can think of memory as a very long one-dimensional array. Where instead of indicies, we use **names** to identify variables.

Every **Byte** in memory has its **own address**, on 64bit machines, memory addresses are 64-bits (or 8 bytes) long.

### Stack vs Heap
*Automatic* lifetime variables are stored in memory in **The Stack**. The **size** of every variable in the stack must be known **prior to execution**.
>Automatic variables are given memory at the start of entering a lexical scope and the memory is then freed upon exiting.

For many reasons however, we wont always know this.

Therefore we manage the memory by **dynamically requesting** and **freeing** memory. This is done in memory in **The Heap**. 

To do this, the **'malloc'** function is used:

        void* malloc(size_t size); //defined in <stdlib.h>

If malloc fails, a void pointer is returned, therefore we must check to see whether memory has been allocated successfully before continuing with the function.

After finishing with a variable, **'free'** must be called to deallocate the memory. If this is not done, it is called a **Memory Leak**.

### Variables in memory

Every variable in C is stored at a constant memory location, until the variable's **lexical scope** is exited. Therefore, variables can be accessed by their addresses in memory. 

- The address operator - & can be used to print the address of a variable  

        int main(){
            int x = 42;
            printf("&x = %p\n", &x);
            OUTPUT: Address of x.
        }
---
# Pointers

A **pointer** is the **address of another variable**, stored as a variable.
To **dereference** a pointer and read the data stored at that location the * operator is used

        int x = 42;
        int * ptr = &x;
        printf("%p points to &d", ptr, *ptr);
        
Sometimes there is no meaningful value for a pointer at a certain time. We use the macro **NULL** to represent a pointer that points to nothing. **Dereferencing** a NULL pointer will **crash your program**.

WARNING: Never return a pointer to a local variable from a function, as the lifetime of a pointer is the same as the variable it is pointing to, therefore will point to nothing.

### Constant pointers

Pointers can be unmodifiable in three ways:
1. The pointer itself i.e. *the address*, cannot be changed.
2. The *value* we are pointing to cannot be changed
3. *Both* value and pointer cannot be changed

        1.float * const ptr;
        2.const float * ptr;
        3.const float * const ptr;

### Arrays and Pointers.

If we have an array, every time we reference it, it's memory size will be [number_of_elements*4] Bytes. Whereas using a pointer to reference it, will only need 8 Bytes (size of a pointer).

---
# Data Structures with Pointers
 Pointers and structs are useful in building data structures.

### Linked List

A linked List contain nodes with a **value** and a **pointer to the next node**.

        struct node {
                char value;
                struct node * next;
        }
        
        int main() {
            struct node c = {'c', NULL};
            struct node b = {'b', &c};
            struct node c = {'a', &b};
        }
We use a **pointer** to iterate over the linked list:

        struct node * ptr = &a;
        //while a node exists
        while(ptr){
            //print value
            printf("%s\n", (*ptr).value);
            //next pointer
            ptr = (*ptr).next;
        }
        
### Binary (Search) Tree

        struct node {
            char value;
            struct node * leftChild;
            struct node * rightChild;
        }
        
To search through a data structure like this, it is quite easy. 
1. If search value = the current node's value
    - return current node
2. Else if value < current node & left isn't NULL
    - go down left branch
3. Else if value > current node and right isnt NULL
    - go down right branch
4. Else return NULL

        node * find(char value, node * current){
            if(current.value == value){
                return current;
            }
            if(value < current.value && current.LeftChild != NULL){
                return find(value, current.LeftChild);
            }
            if(value > current.value && current.Right != NULL){
                return find(value, current.rightChild);
            }
            return NULL;
        }



