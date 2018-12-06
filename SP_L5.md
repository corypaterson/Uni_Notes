# Ownership and Debugging
---
### Quickfire Recap
Ownership:
- To organise resource and memory management we adopt the cocept of *ownership*.
- In C++ the management of a resource is tied to its lifetime on the stack - RAII (Resource Allocation is Initialising.
    - **Allocation** upon creation.
    - **Deallocation** upon deletion.
- This is done by:
    - The *constructor* when creating values
    - The *deconstructor* when exiting the variable's lexical scope.
- C++ provides common datatypes with this already implemented for non-leaking memory managenent:
    - **std::vector** for multiple values.
    - **std::unique_ptr** for single values.

---
### Ownership Transfer

When modelling unique ownership **std::unique_ptr** should be used. A *tree* can be modelled this way, where the **parent is uniquely responsible for each of its children**:

        struct node {
            const char * value;
            std::vector< std::unique_ptr<node> > children;
            
            node(const char * v){
                value = v;
            }
        }

To transfer ownership of a unique resource we use **std::move**:

        COMPLETE OWNERSHIP TRANSFER NOTES

---
### Bugs and Finding them

A number of tools can be used to identify and understand bugs:
- **Debuggers**, run a program in a controlled environment where we can investigate its execution.
- **Static Analysis** tools, reason with a program's behaviour *without running it*.
- **Dynamic Analysis** tools, *add instructions to a program* to detect bugs at run time.

**GDB** and **LLDB** are two popular debuggers for C/~C++.

### Segmentation Fault

A *segmentation fault* is raised by the hardware notifying the notifying the OS that your program has **tried to access a restricted area of memory**. At this point the operating will **imediately terminate your program**.

Common examples of program seg-faults are:
- **Dereferencing a NULL pointer**
- **Writing to read-only memory**
- **A buffer overflow** (accessing memory outside of an allocated buffer)
- **A stack overflow**, triggered by recursion without a base case

To detect a seg-fault, after starting lldb and using the run command. Type '**bt**' to backtrack through the stack and find the line leading to the seg-fault.

**Break Points** can also be used to debug code while using GDB and LLDB. *Break points* are points at which the execution is stopped and we can investigate the program's state.

### Static Analysis

A *static analysis* reasons about the code without executing it.

The compiler performs some static analysis every time you compile your code e.g. *type checking*

Enabling -Wall and Werror flags is the best way to detect errors with your compiler as it enables all warnings and makes all warnings fatal errors.

