# 03/08/2022: Copy Semantics

## Default copy semantics
- Copies over all data members' values 
- For arrays/objects (dynamically allocated objects), the address is copied over, AKA pointer is moved 
- This is a shallow copy because both objects share one dynamically allocated object

## Shallow vs. Deep Copy
- Default copy mechanism is **shallow copy**, i.e. object is copied exactly as is
- In a **deep copy**, objects pointed to are copied first 
    - After deep copy, each identifier has same values, stored in distinct objects, each gets its own dynamically allocated array

## Implementing Deep Copy
**Copy Constructor for 2d array**
```cpp
Array2D::Array2D(const Array 2D& other) {
    if (rhs.array_ == nullptr) {
        Array2D();
    } else {
        width_ = other.width_;
        height_ = other.height_;
        array_ = nullptr;
        try {
            array_ = new int[width_ * height_];
        } catch (...) {
            throw;
        }
        for (int i = 0; i < (width_ * height*); i++) {
            array_[i] = other.array_[i];
        }
    }
}
```

**Copy Assignment Operator**
```cpp
Array2D& Array2D::operator=(const Array2D& other) {
    // first ALWAYS check for self assignment
    if (this == &rhs) {
        return *this;
    } 
    if (other.array_ == nullptr) {
        Array2D();
    }
    int* temp = nullptr;
    try {
        // if 0, leave as nullptr
        if (other.height_ != 0 && other.width_ != 0) {
            temp = new int[other.height_ * other.width_];
        }
    } catch (...) {
        throw;
    }
    delete[] array_;
    array_ = temp;
    width_ = other.width_, height = other.height_;
    // copy over elements
    for (int i = 0; i < (width_ * height_); i++) {
        array_[i] = other.array_[i];
    }
    // return self reference
  return *this;
}
```

**Destructor**
```cpp
Array2D::~Array2D() { delete[] array_; }
```

| **Copy Constructor** | **Copy Assignment Operator** |
| ---------------- | ------------------------ |
| Returns: nothing | Returns: self-reference |
| Member function | operator= overload |
| Parameter: reference to same type const object | Parameter: reference to same type const object |
| Initialize data members -> allocate new memory (check errors) -> deep copy from source | Check for self-assignment -> allocate new memoery (check errors) -> deallocate old dynamically allocated array -> initialize data members -> deep copy from source -> return self reference |

## C++ Rule of Zero
- C++ compiler provides default operators with default semantics
- **If you can avoid defining default operation (copy constructor, copy operator, destructor) you should do so**
- If you don't need them, don't define them!

## C++ Rule of Three
- If either copy constructor, copy assignment, or destructor is defined, **you should imeplement other 2 as well**
- If you want deep copy, you need to implement that behavior across all the functions 
- If you implement one, implement all!