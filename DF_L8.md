# Probability
---
### Axioms of Probability
There are only a few basic axioms of probability, from which everything else can be derived. Writing P(A) to mean the probability of event A:

**Boundedness:**

    0 ≤ P(A) < 1
    
All possible outcomes A, probabilities are 0, or positive and less than 1.

**Unitarity:**

    ∑P(A) = 1

For the complete set of possible outcomes A, something always happens.

**Sum Rule**:

    P(A ∨ B) = P(A) + P(B) − P(A ∧ B),
The probability of either outcome A or B happening, is the sum of the independant probabilities, minus the probability of both happening.

**Conditional Probability**:

    P(A|B) = P(A ∧ B) / P(B)
The conditional probability, is defined to be the probability that outcome A will happen given that we already know B to have happened.

### Distributions

A **probability distribution** how likely states of a random variable are. 

- P(X = x), the probability of random variable X taking on value x
- P(X), shorthand for probability of X=x
- P(x), shorthand for probability of specific value X=x

Note that we use P(A) to mean the probability of **event** A, not the random variable.

### Samples and Sampling

**Samples** are observed outcomes of an experiment. We can **sample** from a distribution, means simulating outcomes according to the probability ditribution of those variables.

**Uniform Sampling**:

Algorithms which generate continuous random numbers which are **uniformly distributed** at an interval. such as 0.0 to 1.0 

A **uniformly distributed** number has equal probability of taking on any value in its interval. 

A uniform distribution is notated U(a,b) meaning numbers drawn between a and b with equal possibility to any number in that interval. 

**Discrete sampling**: 

For a discrete probablity mass function we can sample outcomes according to any arbitary PMF using the following approach:
- choose any arbitrary ordering for the outcomes
- assign each outcome a "bin" which is a portion of the interval [0,1] equal to its probability.
- Draw a uniform sample in the range [0,1]
- whichever "outcome bin" it lands in is the sample to draw.
