
# Optimisation
---
### Overview
There are two main parts to an optimisation problem:

**Parameters**:
- The things we can adjust.
- Might be a scaler or a vector or array of values, denoted θ.
- Prameters exist in a **parameter space** -- The set of all possible configurations of parameters, Θ.

**Objective function**:

- a function that **maps the parameters** onto a *single numerical measure* of how good the configuration is, L(θ).
- The output of the objective function is a **single scalar**.
- It is a quantitave measure of "goodness"

The desired output of the optimisation algorithm is the parameter configuration that **minimises** the objective function.

        optimal(θ) = argminL(θ)
                       θ∈Θ
                       
Most optimisation problems also have one more component:

**Constraints**:
- The limitations on the parameters.
- 