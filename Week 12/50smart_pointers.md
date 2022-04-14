# 04/12/22: Introduction to Smart Pointers

## Cons with raw pointers
- Declaration doesn't mention whether it points to single object, array, etc.
- Declaration doesn't reveal whether there is any memory to be deallocated/object to be deleted 
- If you determine that you need to destroy some memory, how should this deallocation be done? Ex: delete, delete[], or defined delete function for obejct? 
- Hard to tell when we are left with dangling pointers 
- Incorrect deletion can lead to memory leaks, etc. 

## Smart Pointers
- Behavior is similar to raw pointers, but they also safegaurd against the pitfalls 
```cpp
#include <memory>

std::unique_ptr<T>

std::shared_ptr<T>

std::weak_ptr<T>

std::auto_ptr<T> // only use if u need to compile code with the 1998 compiler (C++98)
```

## std::unique_ptr
- Used for **exclusive-ownership resource management**
- Acquire resource in constructor, release in destructor
- **Copy semantics are disabled** (NO COPY CONSTRUTOR, NO COPY ASSIGNMENT OPERATOR), no opportunity to share resource 
- Move semantics tranfer ownership from dynamically allocated object to another, since no copies. 

```cpp
std::unique_ptr<int> ptr = make_unique<int>(7);
```

## std::shared_ptr
- Used for **shared-ownership resource management**
- No specific shared_ptr will own the object, the last shared_ptr object standing destroys the object pointed to 
- **Copy semantics are defined** to allow shared behavior
- **CONTROL BLOCK**: keeps track of how many pointers point to this object (reference count), once pointers are deleted, object moment is automatically deallocated

```cpp
std::shared_ptr<int> ptr = make_shared<int>(7);
auto ptr2 = ptr;
auto ptr3 = ptr;
```

## std::weak_ptr
- Smart pointer but acts like shared, but doesn't participate in shared ownership
- Useful for cyclic relationships with clear hierarchy
- Doesn't maintain reference count
- **This pointer knows when it dangles**
- Usually created from std::shared_ptr<T>
- Doesn't have a deference operation
- Not used in this class much... 

## std::make_unique, std::make_shared
- make_unique used to initialize unique pointer objects (at least C++14)
- make_shared used to initialize shared pointers (at least C++11)