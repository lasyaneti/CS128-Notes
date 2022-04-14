# 04/14/22: Introduction to Shared Pointers

## unique_ptr vs shared_ptr
- No shared pointer owns the object
- The last std::shared_ptr<T> object standing will destroy the object being pointed to
- Parts of the **Control Block**
    - Reference Count
    - Weak Count
    - Other data (custom deleter, allocator, etc.)
- [Documentation](https://en.cppreference.com/w/cpp/memory/shared_ptr)

## Implement sharred_ptr
```cpp
template <typename T>
class SharedPointer {
public:
    SharedPointer(T* address_shared_object);
    SharedPointer(const SharedPointer<T>& source);
    SharedPointer<T>& operator=(const SharedPointed<T>& source) = delete; // if you like, you can define but the reason for this is so you cannot set one shared_ptr to another
    ~SharedPointer();
    T* Get() { return holder_; }
    T& operator*() { return *holder_; }
    size_t UseCount() { return *reference_count_; }
    bool Unique() { return *reference_count_ == 1; }
private:
    T* holder_;
    size_t* reference_count_;
}

// constructor
template <typename T>
SharedPointed<T>::SharedPointer(T* address_shared_object) : holder_(address_shared_object), reference_count_(nullptr) {
    reference_count_ = new size_t(1);
}

// copy constructor
template <typename T>
SharedPointer<T>::SharedPointer(const SharedPointer<T>& source) : holder_(source.holder_), reference_count_(source.reference_count_) {
    (*reference_count_) += 1;
}
// destructor
template <typename T>
SharedPointer<T>::~SharedPointer() {
    (*reference_count_) -= 1;
    if ((*reference_count_) == 0) {
        delete holder_;
        delete reference_count_;
    }
}
```