# Memory and Ownership
---
### Quickfire Recap
Memory:
- Every *byte* in memory has its own 64-bit long address.
- Every variable in C is stored at a **constant location in memory** that **will not change** over its lifetime.
- Can identify a varibale's location by its *address*.
- The address operator (&) will return the address of a variable and sizeof() will return its size.

Pointers:
- A **variable's address** can be stored as a **pointer variable**. It is stored like any other variable.
- The dereference operator (*) allows access to the value of the address we are pointing to.
- A pointer to variable 'x' has data type 'x *'
- **Void pointers** are generic and **cannot be dereferenced**
- Use the macro NULL to represent a pointer that points to nothing. Dereferencing this will crash your program!


Memory Management Challenges:

- When allocating memory, the progammer is responsible for freeing the memory again after use.
- *Free* must be called, **exactly once for each piece of memory allocated**
- If the memory is not freed after allocation it is called a **Memory Leak**.

---

# OwnerShip

To organise we adopt the concept of *ownership*. We identify **a single entity** which is **responsible for managing a location in memory**.

>For example:
In a Binary Tree, the parent **owns** its children and the parent is responsible for allocating and freeing the memory used by its children.

C does not follow this model but C++ has a feature which follows the idea of ownership. 

### Ownership in C++

In C++ the *ownership* of a heap memory location can be expressed in the code. This is done through **RAII** (Resource Aquisition is Initialisation).

The management of a resource is tied to the lifetime of a variable on the stack.
- The *allocation* of the resource is done when we *create* the variable.
- The *deallocation* of the resource is done when the variable is *destroyed*.

In C++ this is implemented by the 'struct' datatypes with two member functions (methods):
- The *constructor* which is called when creating values
- The *deconstructor* which is called when a variable exits its lexical scope.

If we want to store a bunch of integers on the heap, we define a **struct** data type, which has a *constructor* and a *deconstructor*.

        struct ints_on_heap {
            int * val;
            //constructor
            ints_on_heap(int size){
                val = (int*)malloc(sizeof(int)* size);
            }
            //deconstructor
            ~ints_on_heap(){
                free(val);
            }
        };
        typedef struct ints_on_heap ints_on_heap;

When initializing a variable on the stack with this datatype it will **automaticaly allocate memory on the heap** and then will **free memory** when it reaches the end of the variables lexical scope.

### Modern Memory Management in C++

C++ provides some common datatypes that are built with RAII for easy and non-leaking memory management.

To store multiple values of the same type on the heap use **std::vector** as below:

        int main(){
            //memory is allocated on creation
            std::vector<int> v = {1,2,3,4,5,6} 
            //use v
        } //memory is freed automatically
        
To store a single value on the heap, smart pointers should be used:
- **std::unique_ptr** for unique ownership
    - Default case, where a single variable is *owning* the value on the heap. 
- **std::share_ptr** for shared ownership
    - Common in *multi-threaded programming*, where it's not possible to identify a single owner. 
        


