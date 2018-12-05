# Ownership and Debugging
---
### Quickfire Recap
Ownership:
- To organise resource and memory management we adopt the cocept of *ownership*.
- In C++ the management of a resource is tied to its lifetime on the stack.
    - **Allocation** upon creation.
    - **Deallocation** upon deletion.
- This is done by:
    - The *constructor* when creating values
    - The *deconstructor* when exiting the variable's lexical scope.
- C++ provides common datatypes with this already implemented for non-leaking memory managenent:
    - **std::vector** for multiple values.
    - **std::unique_ptr** for single values.
