# Densest Subgraph Construction and Visualization
**Design and Analysis of Algorithms**  
**By:** Ismail Moataz  
**Date:** September 2026

## 1. Network Category: Collaboration Networks

### Description
Collaboration networks represent co-authorship relationships in academic research. In this project, each node represents an author, and an undirected edge exists between two authors if they have co-authored at least one paper together.

### Real-World Applications
- **Research Community Detection:** Identifying tightly-knit research groups and sub-fields.
- **Influence Analysis:** Finding key researchers and central hubs in specific scientific domains.
- **Recommendation Systems:** Suggesting potential collaborators based on network proximity.
- **Knowledge Dissemination:** Understanding how information and methodologies spread across scientific communities.

### Datasets Used
The following datasets from the Network Repository were used, spanning from small to very large scales:
| Dataset | Nodes | Edges | Description |
|---------|-------|-------|-------------|
| ca-netscience | 379 | 913 | Co-authorship in network science. |
| ca-CSphd | 1,882 | 1,739 | Computer Science PhD advisor-advisee relationships. |
| ca-GrQc | 4,158 | 13,422 | General relativity and quantum cosmology co-authorship. |
| ca-HepTh | 9,877 | 25,973 | High-energy physics theory co-authorship. |

## 2. Algorithms Overview

### 2.1 Greedy Peeling Algorithms
**Charikar's Greedy Algorithm**  
Iteratively removes the vertex with the minimum degree from the graph. It is a highly efficient 1/2-approximation algorithm with a time complexity of $O(m + n \log n)$ when using a min-heap.

**Greedy++ Algorithm**  
An advanced multi-pass variant of greedy peeling. It re-weights edges based on the "load" (degree at removal) of nodes in previous passes. This iterative re-weighting allows it to converge on denser subgraphs than the standard greedy approach while maintaining high scalability.

### 2.2 Maximum-Flow-Based Algorithms
**Goldberg's Exact Algorithm**  
Solves the Densest Subgraph Problem (DSP) exactly by reducing it to a series of maximum flow / minimum cut problems. It performs a binary search on the density parameter $g$, constructing a parametric flow network to find the exact optimal density.

**Exact Triangle-Density Algorithm**  
Instead of maximizing edges per vertex, this algorithm maximizes the number of triangles per vertex. It uses a specialized max-flow reduction where a node is created for every triangle in the graph. This method is exceptionally good at finding near-cliques, though it carries a higher computational cost due to triangle enumeration.

## 3. Empirical Results and Visualizations

### 3.1 Computational Cost Growth
The plot below shows the empirical execution time (in seconds) versus the number of nodes for all four algorithms. 
*(Note: Log-log scale used to highlight the polynomial scaling of exact algorithms vs. the near-linear scaling of greedy methods).*

![Computational Cost Plot](visualizations/computational_cost_plot.png)

**Key Takeaways:**
- **Greedy Methods (Charikar, Greedy++):** Scale almost linearly, making them ideal for massive graphs.
- **Exact Methods (Goldberg, Triangle-Density):** Show polynomial growth. Goldberg's scales well up to medium-large graphs, while Triangle-Density incurs high overhead from flow network construction.

### 3.2 Incremental Subgraph Construction
The video below visualizes the incremental construction of the densest subgraph for the `ca-netscience` dataset using Charikar's algorithm. It demonstrates how the algorithm peels away low-degree nodes to reveal the highly connected 9-node core (a perfect clique).

![Subgraph Growth Animation](visualizations/ca_netscience_growth.gif)

## 4. How to Run
1. Ensure Python 3.x is installed.
2. Install dependencies: `pip install python-igraph networkx matplotlib scipy`
3. Place the `.mtx` dataset files in the `datasets/` folder.
4. Run the main benchmarking script: `python code/benchmark.py`

## 5. References
1. Charikar, M. (2000). Greedy approximation algorithms for finding dense components in a graph.
2. Goldberg, A. V. (1984). Finding a maximum density subgraph.
3. Tsourakakis, C. E. (2014). The triangle-densest subgraph problem.
4. Network Repository: https://networkrepository.com/
