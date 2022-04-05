# 04/05/2022: Graph Representations

## Terminology
- **Connected**: there is a path from every vertex to every other vertex in the graph
- **Not connected**: set of connected components, there are vertices that cannot be reaches in a path 
- **Acyclic**: graph with no cycle, ex: TREE!!
- **Path**: sequence of vertices that are visited 
- **Length** of path or cycle: number of edges visited
- **Density**: proportion of possible pairs of vertices that are connected by edges
    - Sparse: few possible edges present
    - Dense: few possible edges missing
- **Adjacent**: 2 nodes are adjacent if an edge exists between them

## Vertex Naming & Edge Notation
- Undirected graph
    - 0 through V-1 for vertices
    - v-w connected edge between node v and w, in this case w-v refers to the same edge

## Graph Representation Alternatives
The following representations both have **space** and **time** tradeoffs.

### Adjacency-Matrix representation
![img](\Images\graphmatrix.png)
- row = source, col = destination
- colored values show us that it is undirected (every edge goes both ways)
- val = 1 if (i, j) in E, else 0
- **0(V^2) memory**, independent of # of edges in graph G
- preferred when |E| is closer to |V|^2
- uses more memory, but efficient to look up node edge connections

### Adjacency-List representation
![img](\Images\graphlist.png)
- list contains pointers to linked list
- index = source, list = connected to 
- uses less memory, efficient to search list to determine edge edge connections

## Etc.
- Matrix representation is inefficient for sparce graph because u are just taking memory for a bunch of 0's, list is more efficient for that
![img](\Images\graphrep.png)
