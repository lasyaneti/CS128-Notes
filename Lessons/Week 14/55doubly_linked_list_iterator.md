# 04/20/22: Implementing Doubly Linked List Iterator

## Set-up
- current_ : Node<\T>*
- DoublyLinkedListIterator()
- DoublyLinkedListIterator(Node<\T>* ptr)
- operator*() const : T&
- operator++() : DoublyLinkedListIterator<\T>&
- operator++(int) : DoublyLinkedListIterator<\T>
- operator!=(const DoublyLinkedListIterator<\T> & other) const : bool
- operator==(const DoublyLinkedListIterator<\T>& other) const : bool

## Implementation
```cpp
template <typename T>
// TELL THE COMPILER THIS CLASS HAS IMPLEMENTED ITERATOR USING COLON
class DoublyLinkedListIterator: public std::iterator<std::forward_iterator_tag, T> {
public:
DoublyLinkedListIterator(): current_(nullptr){}
DoublyLinkedListIterator(Node<T>* ptr) { current_ = ptr; }
T& operator*() const { return current_->data; }
bool operator==(const DoublyLinkedListIterator<T>& other) const { return (current_ == other.current_); }
bool operator!=(const DoublyLinkedListIterator<T> & other) const { return !(*this == other); }
// iterator operators
DoublyLinkedListIterator<T>& operator++();
DoublyLinkedListIterator<T> operator++(int);
private:
    Node<T>* current_;
}

// pre-increment
// increment, return incremented value
template <typename T>
DoublyLinkedList<T>& DoublyLinkedListIterator<T>::operator++() {
    if (current_) {
        current_ = current_->next;
    }
    return *this;
}

// post-increment
// store current value, increment, return current
DoublyLinkedList<T>& DoublyLinkedListIterator<T>::operator++(int) {
    auto clone(*this);
    if (current_) {
        current_ = current_->next;
    }
    return clone;
}
```

## Update DoublyLinkedList<\T> to use iterator
```cpp
class DoublyLinkedList {
public: 
    // ...
    using iterator = DoublyLinkedListIterator<T>;
    iterator begin() { return DoublyLinkedListIterator<T>(head_); }
    iterator end() { return DoublyLinkedListIterator<T>(nullptr); }
private:
    Node<T>* head_ = nullptr;
    Node<T>* tail_ = nullptr;
    size_t size_ = 0;
}
```

## Use
- Without implementing iterators for containers, we cannot used range-based enhanced for-loop
- After implementation:
```cpp
DoublyLinkedList<int> list{std::vector<int>{10,20,30}};
for (auto val : list) {
    std::cout << val <<std::endl;
}

/* prints:
10
20
30 */

for (DoublyLinkedList<int>::iterator i = list.begin(); i != list.end(); ++i) {
    std::cout << *i << std::endl;
}

/* prints:
10
20
30 */
```