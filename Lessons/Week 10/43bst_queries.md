# 30/03/2022: BST queries

## Minimum and Maximum 
- Nodes are already arranged in ordered fashion in BST
- Highly efficient algorithm because:
    - All values lesser than parent are found in theleft subtree 
    - All values equal to or greater than parent are found in the right subtree
    - We don't even have to look at the value of the node as we traverse

### **Minimum node: keep stepping left**
```cpp
template <typename T1, typename T2>
auto* TreeMin(BinaryTreeNode<T1, T2> curr) {
    while (curr->left != nullptr) {
        curr = curr->left;
    }
    return curr;
}
```

### **Maximum node: keep stepping right**
```cpp
template <typename T1, typename T2>
auto* TreeMax(BinaryTreeNode<T1, T2> curr) {
    while (curr->right != nullptr) {
        curr = curr->right;
    }
    return curr;
}
```

## Searching 
- Use BST ordering to make searching efficient 
- Choose left or right traversal based on value of current node with respect to item we are searching for

### Recursive Solution
```cpp
template <typename T1, typename T2>
auto* TreeSearch(BinaryTreeNode<T1, T2> curr, T2 key) {
    if (curr == nullptr || curr->key == key) {
        return curr;
    }
    // make a decision 
    if (key < curr->key) {
        return TreeSearch(curr->left, key);
    } else {
        return TreeSearch(curr->right, key);
    }
}
```

### Interative Solution (rolled)
```cpp
template <typename T1, typename T2>
auto* TreeSearch(BinaryTreeNode<T1, T2> root, T2 key) {
    BinaryTreeNode<T1, T2> curr = root;
    while (curr != nullptr && curr->key != key) {
        if (key < curr->key) {
            curr = curr->left;
        } else {
            curr = curr->right;
        }
    }
    return curr;
}
```

## Successor 
In order traversal: 4, 8, 10, 12, 20, 22
![image](/Images/bst_inorder_traversal.png)


### Successor of In Order Traversal
- Successor of node x is node with smallest key greater than x->key
```cpp
template<typename T1, typename T2>
auto* TreeSuccessor(BinaryTreeNode<T1, T2>* node) {
    // does it have a right subtree?
    if (node->right != nullptr) {
        // if yes, you know that the next key should be the minimum value in that right subtree
        return TreeMinimum(node->right);
    }
    // if not, we have to go one level up and go right
    BinaryTreeNode<T1, T2>* successor = node->parent;
    // if node is left of its parent, do not enter while loop, simply return the parent
    while (successor != nullptr && node == successor->right) {
        // if node is right of its parent we need to work our way till we point to a node is in left subtree of parent (KINDA, more compilated but we try to find the fake next right node)
        // complicated case bc parent cannot be successor when node is right of parent 
        node = successor;
        successor = successor->parent;
    }
    return successor;
}
```

### Consider cases in this order:
1. node has right subtree
2. node does not have right subtree, and is left of its parent
3. node does not have right subtree, and is right of its parent