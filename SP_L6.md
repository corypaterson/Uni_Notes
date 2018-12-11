# Introduction to Concurrency and PThreads
---
### Quickfire Recap of all Lectures
So far we have learned:
- **Data types** give bit representations in memory a meaning.
- **Structs** allows us to implement custom data structures (like linked lists or trees).
- Every variable is stored at **a fixed location in memory**.
- A **pointer** is a variable storing the address of a memory location.
- Memory on the **stack** is **automatically** managed.
- Memory on the **heap** must be managed **manually**.
- To organise resource and memory management we should think about **ownership**.
- In C++ **ownership** is implemented by tying the resource management to the **lifetime** of a stack variable (via *constructors* and *deconstructors*)
- There are a set of **smart pointers** and **containers** for easy and non-leaking memory management.
- **static/dynamic anaylsis tools** and **debuggers** help to detect and fix bugs.
---
### Concurrent Systems Programming

>Concurrency: 
The ability of **different program parts** to be executed **out-of-order** or in **partial order**, without affecting the result.

There are two classes of methods for enabling concurrency in programming.

Shared Memory Communication:
- *Shared memory locations* are **read** and **modified** to communicate between concurrent components.
- Needs **coordination** to ensure that the communications **happens safetly**.
- Threads are used this way.

Message passing communication:
- *Message-passing concurrency* is considered a more robust form of concurrent programming.
- Examples are:
    - Erlang
    - CSP-Style coms in Go.
- **More discussed in the H/M course.**

But how is concurrency different to parallism?
- *Concurrency* is a **programming paradigm**.
    - Is the **composition of independantly executing processes**.
    - Is done with threads.
- *Parallelism* on the otherhand is just about making your programs **run faster**.
    - While threads do make your program faster, processors should be able to run parrallel operations already.
    - The **simultaneous execution of computations**
### Proccesses vs Threads
Every C program is executed as a *process*. These processes can be **executed simultaneously**. When run simultaneously the operating system will make sure that each process is given its **own memory address space** and that processes can not access the memory of another.

A *thread* of execution is an **independant sequence of program instructions**. Multiple threads can be executed at once. A different *process* can have **multiple threads sharing the same address space of the process**. These threads are used to implement concurrent programs.

### Thread Implementations

For C we use the *PThread* Library.

Threading implementations are conceptually very similar:
- A thread is *created* and starts executing a specifying function.
- A thread *terminates* either by:
    -  Calling **exit**
    -  or, when the **specifying function terminates**
-  *Communications* between threads is performed by **modifying the state of shared variables**.

### Race Conditions

A *race condition* occuyrs when the result of a computation depends on the sequence in which threads execute. They are almost always **problematic**.

When using shared memory communication, **mutex** should be used to ensure that race conditions do not occur (very tricky in large practical systems). 

### Condition variables

In concurrent systems a component is often waiting for a condition to become true. A thread can constantly check if the condition is true:

        pthread_mutex_lock(&m);
        while(!cond) {
            pthread_mutex_unlock(&m);
            //wait
            pthread_mutext_lock(&m);
        }

This is called **busy waiting** and a bad practise as it wastes CPU clock cycles doing nothing.

A better design is where a thread is notified by another thread when the condition is changed. For this we use condition varibales.

**COMPLETE THESE NOTES**

### Bounded Buffer

A bounded buffer is a buffer with a fixed size. *producers* **insert elements** into the buffer while *consumers* **remove elements**.

We must ensure that:
- **producers** wait while the buffer is **full**.
- **consumers** wait while the buffer is **empty**.
- Threads resume work when space or data is availiable again.
- Condition variables can be used to achieve this.

The bounded buffer is an example of a *monitor* - an object that allows safe access to a variable (the buffer).

Bounded Buffer Implementation:

- Implemented as a **ring buffer**
- Two condition variables (add and remove) signal the two different conditions (buffer is full or empty).
- Before **inserting or removing** an element **the size of a buffer is checked** and the threads wait if there is not space or data in the buffer.
- After inserting or removing an element the thread signals that space or data or both is now available

### Semaphore

A *semaphore* holds an integer counter together with two operations **wait** and **signal**. 

**Wait** decrememts the counter and blocks if it is less than zero. **Signal** increments the counter and wakes waiting threads. We can count how many items of a resource are used and block access if no resources are available. The semaphore can be used to **ensure an unsafe bounded buffer implentation is used correctly**.

A **binary semaphore** (with a count of 1) is similar to a mutex, as it allows single thread access into a critical section. Although a mutex can only be reset from within the thread that locked it (not the case for a semaphore!).






