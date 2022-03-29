# 28/03/2022: Introduction to Trees

## Intro 
- Non-linear, hierarchial ordering
- **Root**: top node of the tree
- **Leaf**: node with no children
- **Siblings**: children nodes of same parent
- **Depth**: number of edges from node to root (top-down: root is 0 -> +1 as u go down)
- **Height**: number of edges in the longest path from node to leaf 
    - Height of leaf = 0
    - Height of tree = number of edges in the longest path from root to leaf (group-up: node is 0 -> +1 as u go up)
- **Subtree**: tree within a tree

## Binary Trees
Each node has max 2 children
```cpp
// data members
Node<T>* parent;
Node<T>* left;
Node<T>* right;
T data;
```

## Trees with Unbound Branching
- A tree with similar traversal as a singly linked list: go to leftmost child and traverse through right-side siblings.
- Each node has an arbitrary number of children
```cpp
// data members
Node<T>* parent;
Node<T>* left-child;
Node<T>* right-sibling;
T data
```

## Other Tree Representations
- Trees can be stored in an array