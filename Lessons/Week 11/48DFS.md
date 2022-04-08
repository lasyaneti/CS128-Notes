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

## HW: iterative dfs on graph with no helpers, works on cyclic graphs too
```cpp
std::vector<std::string> TrivialGraph::DepthFirstTraversal(const std::string& origin) {
  std::vector<std::string> visited;
  std::stack<std::string> stack;
  std::set<std::string> stack_elems;
  stack.push(origin);
  stack_elems.insert(origin);
  while (!stack.empty()) {
    std::string str = stack.top();
    stack.pop();
    // stack_elems.erase(str);
    bool in_vect = false;
    for (size_t i = 0; i < visited.size(); i++) {
      if (visited.at(i) == str) {
        in_vect = true;
      }
    }
    if (!in_vect) {
      visited.push_back(str);
      std::list<std::string> adj_list = graph_.at(str);
      for (std::string curr : adj_list) {
        bool in_stack = false;
        if (stack_elems.find(curr) != stack_elems.end()) {
          in_stack = true;
        }
        if (!in_stack) {
          std::cout << curr << std::endl;
          stack.push(curr);
          stack_elems.insert(curr);
        }
      }
    }
  }
  return visited;
}
```