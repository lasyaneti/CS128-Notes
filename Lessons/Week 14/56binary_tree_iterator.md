# 04/21/22: Implementing Binary Tree Iterator
This implementation will perform an inorder traversal for a Binary Search Tree

## Implementation
```cpp
template <typename T1, typename T2>
class BinarySearchTreeIterator: public std::iterator<std::forward_iterator_tag, T1> {
public:
    BinarySearchTreeIterator(Node<T1, T2>* iter_init);
    BinarySearchTreeIterator<T1, T2>& operator++();
    T1& operator*() const { return iter_->data; }
    bool operator==(const BinarySearchTreeIterator<T1, T2>& other) { return (iter_ == other.iter_); }
    bool operator!=(const BinarySearchTreeIterator<T1, T2>& other) { return !(iter_ == other.iter_); }

private:
    Node<T1, T2>* iter_;
    std::stack<Node<T1, T2>*> stack_;
}

template <typename T1, typename T2>
BinarySearchTreeIterator<T1, T2>::BinarySearchTreeIterator(Node<T1, T2>* iter_init): iter_(iter_init) {
    if (iter_ == nullptr) {
        return;
    }
    while (iter_ != nullptr) {
        stack_.push(iter_);
        iter_ = iter_->left;
    }
    iter_ = stack_.top();
    stack_.pop();
}
```
At this point, we have a node pointer to the first element in the BST

## "next" Operation
![Image](/Images/BST_iterator.png)
```cpp
template <typename T1, typename T2>
BinarySearchTreeIterator<T1, T2>& BinarySearchTreeIterator<T1, T2>::operator++() {
    if (!stack.empty()) {
        iter_ = stack_.top();
        stack_.pop();
        // now we need to set this up 
        // in a way such that the next of 8 is 10
        // not 20 or the other nodes 
        if (iter_->right != nullptr) {
            auto* curr = iter_->right;
            while (curr != nullptr) {
                stack_.push(curr);
                curr = curr->left;
            }
        } 
    } else {
        iter_ = nullptr;
    }
    return *this;
}
```

## Changes to BST class
```cpp
template <typename T1, typename T2>
class BinarySearchTree {
public:
    // ...
    using iterator = BinarySearchTreeIterator<T1, T2>;
    iterator begin() { return BinarySearchTreeIterator<T1, T2>(root_); }
    iterator end() { return BinarySearchTreeIterator<T1, T2>(nullptr); }
private:
    // ...
}
```