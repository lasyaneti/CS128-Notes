# 03/23/2022: Class Templates

## Motivation
- Similar to function templates, class templates of similar classes that deal with different types require entirely new classes that have mostly the exact same code
- Class templates allow us to leave the types, parameters, local vars, etc. open 

## Class Templates: implement Stack
**Stack will be able to hold:**
```cpp
Stack<double> // doubles
Stack<int> // ints
Stack<char*> // pointers to char
```

**Example stack:**
```cpp
// definition
#ifndef STACK_HPP
#define STACK_HPP

class Underflow{};
class Overflow{};

template <class T>
class Stack {
public:
    // method declaration
    void Push(T value);
    T Pop();
private:
    static constexpr size_t kMaxSize = 200;
    T v_[kMaxSize];
    size_t top_ = 0;
};

// definition
// we also need to declare our functions as function templates
// indicate member function of class and function template

template <typename T>
void Stack<T>::Push(T value) {
    if (top_ == max_size) throw Overflow();
    v_[top_] = value;
    top_ += 1;
}

template <typename T>
T Stack<T>::Pop() {
    if (top_ < 0) throw Underflow();
    top -= 1;
    return v_[top_];
}

#endif
```

To instantiate class template, **you must specify the template argument**

## Class Templates and Separate Compilation
- For each template instantiation, the compiler creates its own copy of member functions for concrete type
- When we do "#include" the function declarations/class definitions are in essense copy and pasted into the function
- But with class templates, **again this won't be avalible till link time**
- Compiler must have access to complete definition to **class template definition** and **member function template definitions**
- Solution: in this class, we include definitions in .hpp header file 