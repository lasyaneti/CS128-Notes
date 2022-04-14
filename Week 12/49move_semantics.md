# 04/11/22: Introduction to Move Semantics

## Move Semantics
- Special member classes in C++98 (1998) require
    - Default constructor
    - Destructor, copy constructor, copy assignment operator (if you do one, you do all 3)
- Special member classes in C++11 (2011) require
    - Previous
    - PLUS move constructor
    - PLUS move assignment operator 

```cpp
// Move Constructor
Type(Type<T>&& rhs);
// Move Assignment Operator
Type& operator=(Type<T>& rhs);
```

- Rule of 3 -> **Rule of 5**: if you implement one, you must implement all five
- **Move Semantics**: special member functions that make it possible for compilers to replace expensive copy operations with less expensive moves

## Type&&
1. rvalue reference, which only binds to rvalues, used to identify objects that moved
2. universal reference which can mean either rvalue reference or an lvalue reference. dual nature allows it to bind to both r- and l- values

### lvalue
- Represents an object that occupies an identifiable location in memory 
- These can be modified
```cpp
int i = 0;
i = 4;
```

### rvalue
- Defined by exclusion, every expression is either an lvalue or rvalue and that an rvalue is NOT an lvalue
```cpp
int i = 0;
(i % 2) = 1;
// resulting value of i % 2 is TEMP, thus rvalue
```

## Consider Object Ownership...
- Transfer contents of objects being transfered, ex: nodes of list_a transferred to list_b
1. Create shallow copy: move addresses over
2. Terminate sharred resource, point to nullptr

## Transferring Ownership with std::move()
Ex 1
```cpp
std::vector<int> v1{1, 2, 3};
std::vector<int> v2 = std::move(v1);
// this calls vector's move constructor
// the std::move call becomes std::vector<int>&&, like below
// std::vector<int> move(std::vector<int>&& rhs)
```

Ex 2
```cpp
std::vector<int> v1{1, 2, 3};
std::vector<int> v2{4, 5, 6};
v2 = std::move(v1);
// first check self assignment
// free v2 memory, delete is called
// content/resource is sharred 
// (ownership is transferred) AKA terminate sharing
```

## Move Semantics for Doubly Linked List
```cpp
template <typename T>
DoublyLinekdList<T>::DoublyLinkedList(DoublyLinkedList<T>&& rhs) : head_(rhs.head_), tail_(rhs.tail_), size_(rhs.size_) {
    // initializer list performs shallow copy
    // resources are sharred
    // lets break sharred resources:
    rhs.head_ = nullptr;
    rhs.tail_ = nullptr;
    rhs.size_ = 0;
    // move complete
}

template <typename T>
DoublyLinkedList<T>& DoublyLinkedList<T>::operator=(DoublyLinkedList<T>&& rhs) {
    if (this == &rhs) {
        return *this;
    }
    clear();
    head_ = rhs.head_;
    rhs.head_ = nullptr;
    tail_ = rhs.tail_;
    rhs.tail_ = nullptr;
    size_ = rhs.size_;
    rhs.size_ = 0;
    return *this;
}
```

## Summary, etc.
![image](/Images/move_summary.png)

Compiler implicitly replaces expensive copy operations with less expensive moves.