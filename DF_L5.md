# Computational Linear Algebra
---

### Graphs as Matrices

(Like in Algorithmics 1)

We map an edge to a 1 in a v*v matrix where v is the number of nodes in a graph.

Basically an **adjacency matrix**

SEE PAGE 3 OF WEEK_5

---
### Computing Graph Properties

Once we have this binary matrix we can compute:
- The *out-degree* of each vertex (number of edges leaving the vertex)
    - the sum across the **rows**
- The *in-degree* (edges entering vertex)
    - the sum across the **columns**
- If the matrix is **symmetric** (equal to its transpose) the graph is **undirected**.
- A directed graph can be converted to an undirected one by computing A + A^t 
- If there is a non-zero diagonal, then there are vertices with edges to themselves

This adjaceny matrix can be upgraded to include edge weights. Instead of binary 1s, use weight values.

---
### Stochastic matrices

We can think of graphs as defining flows of "mass" through a network of vertices.

- If total flow out of a vertex is > 1, it is a **source** of weight (manufacturing things). 
- If the total weight out of a vertex is < 1 then it is a **sink** (consuming things).
- If the total flow out is exactly 1, then the mass is conserved by the vertex, it only ever *reroutes* things.

If a graph is conserving, then its adjacency matrix will be **stochastic**.

There are three kinds of stochastic matrix:
- **right stochastic**: each row sums to 1
- **left stochastic**: each column sums to 1
- **doubly stochastic**: both rows and columns all sum to 1

A stochastic matrix represents a graph where as much stuff that goes into the graph, comes back out of the graph and no node produces or consumes resources. **Doubly stochastic** means if the flow were reversed, it would still be a conserving graph.

