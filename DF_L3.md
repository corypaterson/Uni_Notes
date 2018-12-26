# Visualisation
---
### What is it?

The representation of data for human visual perception. It **endcodes abstract mathematical objects** into a form that **humans can draw meaning from**. 

Examples range from bar chart, to sophisticated volume readings.

Visulisation purposes:
- to build intuition about relationships and structure in data
- to sumarise large quantities of data
- to help decision makers make quick judgements on specific questions

Basic Categories:
- plots of 1D array data, like histograms
- plots of 2D array data (x,y), like scatter plots 
- plots of 2D arrays data x, like contour plots 

These are all datasets represented as tables of numbers.

---
### Grammar of Graphics

**Stat**
- A Statistic that is computed from data which is then mapped onto visual features with the intent of *summarising data*.
- Example: the median of a dataset

**Mapping**
- A mapping represents a transformations of data attributes to visual values. It maps selected attributes to visual vaues using a *scale* to give units.
- A **scale** specifies the transformation of data into units to give meaning.
- A **guide** is a visual reference that indicates the meaning of a mapping. (tick marks, labels etc.)

**Geom**
- The geometric representation of data after it has been mapped, includes points lines etc.

**Coord**
-A coordinate system which connects mapped data onto points on the plane. The configuration of geom and guides depends on the coord.

**Layer**
- A plot of one set of geoms, with one mapping on one coordinate system. Multiple layers can be layed on one coordinate system.
- Example: two lines for two different years of production rates

**Facet**
- A different view of the same data set, on a separate coordinate system.

**Figure**
- Comprises of a set of one or more facets

**Caption**
- Every figure has a caption which explains the visulisation to the reader


---

### Box plot

A box plot is a visual summary of an array of values. It computes multiple stats of a data set and shows them in a single *geom*. 

The values shown are usually:

- The **interquartile range** (the range between 75% and 25% of the dataset)
- The **median** value 
- The **extrema**, represents the 2.5% and 98.5% (the whiskers of the graph)
- The outliers (points outside the extrema) marked as circles

### Smoothing

Finding a simplified version of the dataset by removing fast changes in values. A good smoothing of data removes obscure details and reveals attributes of interest to the reader.