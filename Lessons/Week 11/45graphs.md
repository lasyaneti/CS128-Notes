# 04/04/2022: Graphs

## Set
- Mathematically, the set is a collection of distinct objects

## Graph
- **vertex** set: finite, nonempty
- **edge** set may be empty, elements are 2-element subset of vertex set (edge bridges 2 vertices)

### Example
![image](/Images/graph.png)
- Vertex set: {x1, x2, x3, x4, x5, x6}
- Edge set: { {x1, x2}, {x1, x3}, {x2, x5}, {x3, x4}

## Graph Types
- Direction
    - Undirected: edge goes both ways 
    - Directed: edge must be specified in both directions to go both ways
![image](/Images/degree.jpg)
- Edge 
    - Simple: no two edges connect the same pair 
    - Multigraph: more than 1 edge can connect same pair of vertices
- Loop: node connected to itself
- Cycle: circular path exists connecting back to starting node
![image](/Images/cycle.jpg)

## How are graphs useful
- Social networks: collaboration, influence, hierarchy, etc
- Transportation networks: airports, roads
- Biological networks