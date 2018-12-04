# Memory and Pointers
---
### Computer Memory
>Oxford Dictionary: "the part of the computer in which data or program instructions can be stored for retrieval."

We can think of memory as a very long one-dimensional array. Where instead of indicies, we use **names** to identify variables.

Every **Byte** in memory has its **own address**, on 64bit machines, memory addresses are 64-bits (or 8 bytes) long.

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

### Constant pointers

Pointers can be unmodifiable in three ways:
1. The pointer itself i.e. *the address*, cannot be changed.
2. The *value* we are pointing to cannot be changed
3. *Both* value and pointer cannot be changed

        1.float * const ptr;
        2.const float * ptr;
        3.const float * const ptr;
        
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

