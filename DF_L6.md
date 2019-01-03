
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
- Defines a region of parameter space that is feasible, the **feasible set**.

> Design a plane (adjust parameters), that flies as fast as possible (objective function), but costs less than £100M (constraints)

### Minimising Differences

It is common to express problems in a form where the objective function is a **distance between an output and a reference is measured**. 

We have some function y' = f(**x**;θ) that produces an output from an input **x**, governed by a set of parameters θ, and we measure the difference between the oputput and some reference y:

         L(θ)=‖y′−y‖=‖f(x;θ)−y‖
---
### Types of optimisation

Discrete vs Continous:

If the parameters are in a continous space, the problem is one of **continous optimisation**, if the parameters are discrete, the problem is **discrete optimisation**.

*Examples*
Continous:
- optimising an plane wing for maximum lift, or minimum drag in certain wind adjustments

Discrete:
- Bin packing, where we want to find an assignment of elements to best occupy a set of bins with defined capacity. 

### Geometric Median Problem


**problem:**
- Find a median of a >1D data set.
- Usually done by sorting elements and taking the middle one. This **doesnt work** for higher dimensions.
- But the median can be defined as:
    - The vector that minimises the sum of distances, to all vectors in the dataset.
    - If taken a point **x**, sum all the distances of **x** to every other point
    - The lowest sum of a given **x**, will be the median
    

        L(θ) = ∑||θ − x|| for each x 

### Constrained Optimisation


If constraints on parameters, is beyod just minimising the function, then the problem is **constrained optimization**.

A constrained optimization might be written in terms of an equality constraint:

        θ∗=argminθL(θ) subject to c(θ)=0,
        
or an inequality:

        θ∗=argminθ∈ΘL(θ) subject to c(θ)≤0,

where c(θ) is a function that represents the constraints.

- An **equality constraint** can be thought of as constraining parameters to a surface, to represent a trade off. 
    - e.g. Where the total valye must remain unchanged, like the total weight of items allowed on a rocket.
- An **inequality constaint** can be thought of as constraining parameters to a *volume*, to represent bounds on values.
    - e.g. the range of knobs on a synthesizer (parameters lie within a box extending (-10,10) around the origin)

### Constraint Types

A **box constraint**:

Requirement that parameters (θ), lie within a box. For example: 0 < θ < 1 (all parameters in the positive unit cube) or θ > 0 (all parameters in the positive **orthant**)

A **convex constraint**:

Limited by a collection of inequalities, a box constraint is a specific subclass of convex constraints.

Equivalent to the feasible set being limited by the intersection of many **planes** (possibly an infinite number, in the case of curved convex constraints).

**Unconstrained optimization**: 

Does not apply constaints to parameters, any parameter in the search space is possible. Usually unhelpful results with this... "The plane wing will give most lift if 200miles long", which is clearly not feasible.


### Constaints and Penalties

As some optimization possibilities are not feasilble when put to practise (see above example). There are two ways to deal with this (even though we often represent θ as being in ℝ):

**Constrained Optimization**:
- Typical constraints will be specified as either a **convex region** or a simple rectangular region of space (**box constraint**)

Pros
- Guaruntees that solution will satisfy constraints
- Can use these constraints to speed up optimization

Cons
- May be less efficient than unconstrained optimization
- Fewer algorithms avaliable
- May be hard to specify a feasible region with the parameters avaliable.

**Soft constraints**:

- Apply penalties to the objective function to *discourage* solutions that violate the constraints.
- Used if constraints are particularily soft eg: "it doesnt matter if the length is 1.6m or 1.8m, but it cant be 10m"
- At each optimization, the optimizer stays the same but the objective function is modified:
    - L(θ′)=L(θ)+λ(θ), where λ(θ) is a **penalty function** with an increasing value as constraints are violated more.

Pros:
- any optimiser can be used
- can deal with *soft* constraints sensibly

cons:
- may not respect important restraints, especially if they are v sharp
- Can be hard to formulate constraints as penalties
- cannot take advantage of efficient search in constrained regions of space

### Objective Function Properties

Will have a **local minimum**, a point at which the function increases in every direction around that point. Any change in parameters around that point will cause an increase.

Is **convex** if it has a *single, global minimum*. 

**Convexity** implies that findind any minimum is equivalent to finding the global minimum -- the best possible solution. 

- We can stop searching a convex objective function if:
    -  We find a minimum, or,
    -  We can show that there is no minimum.

### Convex Optimisation

If the objective function is **convex** AND any constraints form convex portions of the search space, then this is called **convex optimization**. 

There are many efficient methods for solving convex optimisation problems, including:

- The constraints anf objective are linear (**linear programming**)
- Quadratic objective function and linear constraints (**quadratic programming**)
- or some specialised cases (**semi-quadratic programming, quadratically constrained quadratic programming**)

### Continuity

An objective function is **continuous** for some very small adjustment to θ there is an *arbitrarily* small change in L(θ). No sudden jumps in value (smooth graph).

If a function is discontinous, local search methods are not guarunteed to converge to a solution. 

---

### Optimization Algorithms:
#### Iterative Optimisation

**Iterative optimisation** involves making a series of steps in parameter space. There is a **current parameter vector**, which is adjusted at each iteration, until optimization terminates after some **termination criteria** have been met.

Algorithm:

1. Choose starting point x_0
2. while objective function changing
    a. adjust parameters
    b. evaluate objective function
    c. if better solution found than any so far, record it
3. Return best parameter found

### Grid Search

Straight forward, but inefficient. 

Parameter space is sampled by equally dividing the feasible set by a fixed number in each dimension. 

The objective function is evaluated at each 
θ on this grid, and the lowest loss θ found is tracked. 

SEE LECTURE NOTES FOR GRID SEARCH DIAGRAMS

> While this is fine in 1D (just check 8 points) and 2D (just check 64 points), it breaks down completely if you have a 100 dimensional parameter space. This would need: 203703597633448608626844568
840937816105146839366593625063614
0449354381299763336706183397376

Density of grid search:
- If the objective function isnt v smooth, then a much denser grid is needed to catch any minima. 
- Optimisation problems usually have very high parameter numbers (1000s,10000000s...etc), which means is v inefficient 
- as grid search is *exponential* in the number o fdimensions of the parameter space

Pros:
- Works for any continous prarmeter space
- Requires no knowledge of the objective function
- Trivial to implement

Cons:
- **Incredibly** inefficient
- Must specify seach space bounds in advance
- Highly biased to finding things near the *early corners* of the space
- Depends heavily on number of divisions chosen
- Hard to tune so that minima are not missed entierly

Adaptive Grid Search Model:

**Adaptive grid search** can change the size of its divisions dynamically. First coarse, to find an approximate location, then followed by a denser search n that grid space and so on (only works well for convex functions with a single global minima).

### Random Search

Process is simple:
- Guess a random parameter
- Check the objective function
- If L(θ) < L(θ∗), set θ∗ = θ

Pros:
- Cannot get trapped in local minima
- Requires no knowledge of objective function's structure
- Very simple to implement
- Better than grid search (almost always)

Cons:
- *Extremely inefficient* 
- Must be possible to randomly sample the parameter space
- Results do not necessarily get better over time (bets result might be found in the first step or millionth)

### Locality

A class of algorithms that make *incremental* changes to a solution. 
- They are subject to getting trapped in a **local minimum** and not finding the **global minimum**. 
- But are more efficient than grid and random.

Hill climbing modification:

Hill climbing randomly samples configurations *near* the current best parameter vector. 

**Simple hill climbing** adjusts just one of the parameter vector elements at a time, examining each "direction" in turn, and taking a step if it improves things. **Stochastic hill** climbing makes a random adjustment to the parameter vector, then either accepts or rejects the step depending on whether the result is an improvement.

pros:
- Not much more complicated than a random search
- can be much faster than random search

cons:
- Hard to choose how much of an adjustment to make
- Can get stuck in minima
- Struggles with objective function regions that are relatively flat
- Requires that objective function is continuous

###Population

Applies some analogue of **evolution** to solving optimisation. Involves some:
- **mutation** (random variation)
- **natural selection** (solution selecting)
- **breeding** (interchange between solutions)

populations search pros:
- Easy to undertsand and applicable to many problems
- Requires only weak knowledge of objective function
- Can be applied to discrete and continuous problems
- Some robustness against local minima
- Great flexibility in parameterisation

cons:
- Many hyperparameters to tune which radically affect performance
- No guaruntee of convergence
- Slow compared to using stronger knowledge of objective function
- many evolutions are required

### Memory

We should keep track of the paths we took to good solutions so we can easily find them again. Instead of randomly going somewhere, checking the solution and then going somewhere else. If it is a kind-of-good solution, remember the path.

pros:
- can be very effective in spaces where good solutions are separated by large areas of bad ones
- Can use fewer evaluations of the objective functuon
- When it works, it really works

Cons:
- Moderately complex algorithm
- No guarantee of convergence
- Even more hyperparameters than genetic algorithms (populations)



