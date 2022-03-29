# 29/03/2022: BST and BST traversal

## Intro
Organized binary tree data structure
- Key and data
- Pointers to left, right, parent
- At most 2 children
- Node order satisfy
    - y node in left-subtree of node x: y.key < x.key
    - y node in right-subtree of node x: y.key >= x.key

```cpp
Node<T1, T2>* parent;
Node<T1, T2>* left;
Node<T1, T2>* right;
// ex: data = student name, key = student UIN
T1 data;
T2 key;
```

- **Empty/Null tree**: no nodes
- **Height**: button up (longest path to leaf)
- **Depth**: top down
- **Height-balanced BST**: abs(left subtree height - right subtree height) <= 1

## Inorder Traversal
Process root of subtree BETWEEN processing values in left subtree and right subtree
```cpp
void InorderTreeWalk(Node<T>* node) {
    if (node != nullptr) {
        InorderTreeWalk(node->left);
        // process node
        InorderTreeWalk(node->right);
    }
}
```
![image](/Images/bst_inorder_traversal.png)
**Processing order: 4, 8, 10, 12, 14, 20, 22**

## Preorder Traversal
Process root FIRST, then values in either subtree
```cpp
void PreorderTreeWalk(Node<T>* node) {
    if (node != nullptr) {
        // process node
        PreorderTreeWalk(node->left);
        PreorderTreeWalk(node->right);
    }
}
```
![image](/Images/bst_inorder_traversal.png)
**Processing order: 20, 8, 4, 12, 10, 14, 22**

## Postorder Traversal
Process root LAST, after all values in either subtree
```cpp
void PostorderTreeWalk(Node<T>* node) {
    if (node != nullptr) {
        PreorderTreeWalk(node->left);
        PreorderTreeWalk(node->right);
        // process node
    }
}
```
![image](/Images/bst_inorder_traversal.png)
**Processing order: 4, 10, 14, 12, 8, 22, 20**
