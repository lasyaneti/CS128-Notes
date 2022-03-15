# 03/07/2022: RAII and dynamic memory in classes

## What is RAII?
- RAII = Resource Acquisition is Initialization
- Resource management in C++ is initialization (construction) and clean up (destruction) based on scope
- Objects with score are destructed when code exits the scope
- Objects created using **new**, on the free store, need to be cleaned up by us using **delete**

## example: VectorInt
Simplified version of std::vector<int>

**Header File**
```cpp
#ifndef VECTORINT_HPP
#define VECTORINT_HPP

class VectorInt {
public:
    VectorInt(size_t size, int init_value);
    ~VectorInt();
    size_t size() const { return size_; }
    size_t capacity() const { return capacity_; }
    int& operator[](size_t index);
    const int& operator[](size_t index) const;
    VectorInt& push_back(int value);

private:
    void InitArray(int init_value);
    void Grow();
    void Resize(size_t new_capacity);
    int* array_;
    size_t size_;
    size_t capacity_;
};

#endif 
```

**C++ File**
```cpp
#include "vectorint.hpp"

VectorInt::VectorInt(size_t size, int init_value) : array_(nullptr), size_(size), capacity_(size*2) {
    try {
        // maybe there is no memory avaliable
        array_ = new int[capacity_];
    } catch (const std::bad_alloc&) {
        // no need to clean up since first and only dynamically allocated object
        // just rethrow expection 
        // useful when you have 2 dynamically allocated objects and first works but second throws error - you handle it by creating space for it 
        throw;
    }
    InitArray(init_value);
}

void VectorInt::InitArray(int init_value) {
    for (size_t index = 0; index < size_; index++) {
        array[index] = init_value;
    }
}

// no return type for destructor, just like constructors
VectorInt::~VectorInt() {
    delete[] array_;
}

VectorInt& VectorInt::push_back(int value) {
    if (size == capacity_) Grow();
    array_[size_] = value;
    size_ += 1;
    // return self reference
    return *this;
}

void VectorInt::Grow() {
    Resize(capacity_ * 2);
}

void VectorInt::Resize(size_t new_capacity) {
    int* copy = new int[new_capacity];
    int index_to_copy_till = 0;
    if (new_capacity > size_) {
        index_to_copy_till = size_;
    } else {
        index_to_copy_till = new_capacity;
    }
    for (size_t i = 0; i < index_to_copy_till; i++) {
        copy[i] = array_[i];
    }
    delete[] array_;
    array_ = copy;
    size_ = index_to_copy_till;
    capacity_ = new_capacity;
}
```