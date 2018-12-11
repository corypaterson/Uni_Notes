# Task Systems
---
### Quickfire Recap
- C++ provides **thread** facilities similar to PThread but easier to use.
- For this the type ointerfaces **auto** and **lambda** should be used.
- The idea of temporary **ownership** of a **std::mutex** to provide mutual exclusion without the possibility to forget to unlock.
- To make data structures thread safe we can **encapsulate** an un safe version anf provide a threadsafe interface to them.
- A **task** is an abstraction of a thread, where we think about communication between tasks (not low level synchronisation mechanisms).
- **std::async** launches a task and communicates its result via a **std::future**.
- A **std::future** is the reading end of a communication channel. The writing end is called a **std::promise**.
---
### Task Management

LOOK AT LECTURE SLIDES FOR CODE IMPLEMENTATION


