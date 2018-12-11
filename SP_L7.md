# Threads in C++
---
### Quickfire Recap

- **Concurency** is a programming paradigm to deal with lots of things at once.
- Whereas **parallelism** is just about making programs run faster.
- **Threads** execute concurrently inside of the same **process** and share the **same address space**.
- Communication between threads happens by shared memory, but careful synchronisation mechanisms are used to make sure this happens safely.
- **Race Conditions** can be avoided by the concept of *mutual exclusion* which we ensure by using a **mutex**.
- **Condition variables** are a synchronous mechanism to avoid *busy waiting* for a condition to become true.
- We can design data structures like the **bounded buffer** that internally use synchronous mechanisms to ensure a safe usage. We call such objects *thread-safe* access **monitors**.
---
