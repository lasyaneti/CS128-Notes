# 04/07/2022: Depth-First Search (DFS)

## Analogy: Search in Maze
- pick any passage you can go down, but unroll a string on your way there so you can find your way back
- mark all intersections and passages when you visit them so you know when you arrive at them again
- retrace steps till you find a new passage to take 

## DFS intro
- recursive call
    - if we encouter edge v-u
    - or skip the edge if u is marked as visited
- once all edges incident to vertex v are processed, we "return" to continue exploration from vertex w that led us to v

## DFS walkthrough
- maintain a marked list to keep track of visited 
- as you traverse, consult adjacency list
- if all nodes in adjacency list are visited, it will return from recursive call 