# 03/31/2022: BST Construction, Insertion, Destruction

## Class setup and node configuration
Node
```cpp
template <typename T1, typename T2>
struct Node<T1, T2> {
    Node* parent = nullptr;
    Node* left = nullptr;
    Node* right = nullptr;
    T1 data;
    T2 key;
}
```

BinarySearchTree
```cpp
template <typename T1, typename T2>
class BinarySearchTree {
public:
    BinarySearchTree();
    BinarySearchTree(const T1& data, const T2& key);
    BinarySearchTree(const BinarySearchTree& source) = delete;
    BinarySearchTree& operator=(const BinarySearchTree& source) = delete;
    ~BinarySearchTree();
    void Insert(const T1& data, const T2& key);
    void Clear();
private:
    Node<T1, T2>* root_;
    Clear(Node<T1, T2>* n);
};
```

## Construction
### Default Constructor
```cpp
template <typename T1, typename T2>
BinarySearchTree<T1, T2>::BinarySearchTree() : root_(nullptr) {
    // 
}
```

### Parameterized Constructor
```cpp
template <typename T1, typename T2>
BinarySearchTree<T1, T2>::BinarySearchTree(const T1& data, const T2& key) : root_(nullptr) {
    // do not use NEW or allocated for memory in the initialization list 
    // do that in here:
    auto* temp = new Node<T1, T2>;
    temp->data = data;
    temp->key = key;
    root_ = temp;
}
```

## BST Insertion
Similarly to successor/search, traverse tree knowing that nodes are arranged in specific order.
```cpp
template <typename T1, typename T2>
void BinarySearchTree<T1, T2>::Insert(const T1& data, const T2& key) {
    auto new_node = new Node<T1, T2>;
    new_node->data = data;
    new_node->key = key;
    // if tree is empty
    if (root_ == nullptr) {
        root_ = new_node;
        return;
    }
    // similar to successor code
    auto* iter = root_;
    auto* parent = root_;
    while (iter) {
        parent = iter;
        if (key < iter->key) {
            iter = iter->left;
        } else {
            iter = iter->right;
        }
    }
    if (key < parent->key) {
        parent->left = new_node;
    } else {
        parent->right = new_node;
    }
    new_node->parent = parent;
}
```

## Destruction
- Preorder traversal doesn't work because it will result in massive memory leak
- Inorder traversal also doesn't work because of subtree memory leak
- Postorder traversal is the ideal method of deallocation

```cpp
template <typename T1, typename T2>
void BinarySearchTree<T1, T2>::~BinarySearchTree() {
    Clear();
}

template <typename T1, typename T2>
void BinarySearchTree<T1, T2>::Clear() {
    // call overloaded definition of clear
    Clear(root_);
    root_ = nullptr;
}

template <typename T1, typename T2>
void BinarySearchTree<T1, T2>::Clear(Node<T1, T2>* n) {
    // perform post order traversal
    if (n != nullptr) {
        Clear(n->left);
        Clear(n->right);
        delete n;
    }
}
```