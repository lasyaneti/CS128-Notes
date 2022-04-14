# 04/13/22: Introduction to Unique Pointers

## RAII and destructors revisited
- RAII is a technique for resource mangement based on scope
- Order for destructor calls:
    - Class destructor is called and body of destructor function is executed
    - Destructors for nonstatic member objects is called
    - Destructors for non-virtual base classes is called
    - Destructors for virtual base classes is called

## Applying unique pointer to data structures

Vector should be made using unique pointer
```cpp
array = std::make_unique<int[]>(capacity);
```

SinglyLinkedList should be made using unique pointer
```cpp
head_ = std::unique_ptr<Node<T>>
```

DoublyLinkedList should be made using unique pointer
```cpp
head_ = unique_ptr<Node<T>>
// node
next_ = unique_ptr
prev = raw pointer
```

BinarySearchTree should be made using unique pointer
```cpp
root = std::unique_ptr<Node<T1, T2>>
// node
parent = Node<T1, T2>*
left = std::unique_ptr<Node<T1, T2>>
right = std::unique_ptr<Node<T1, T2>>
```

## Behaviors of unique pointers
- **Parameterized constructor**: constructors new unique ptr object to passed resource
- **Destructor**: releases recourses currently held
- **Move assignment operator**: transfered ownership
- **Release**: releases ownership of resource to caller, who then is responsible for eventually deleting it 
- **Reset**: releases ownership of resource currently owned and takes ownership of object whose address is passed
- **Swap**: swaps owned resources with passed argument unique pointer object
- **Get**: returns raw pointer to owned resource 
- **operator bool**: checks whether unique ptr owns resource, i.e. get() != nullptr 
- **operator* and operator->**: returns resource owned by unique ptr
- **operator[]**: provides indexed access to resources