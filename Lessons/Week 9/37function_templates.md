# 03/21/2022: Function Templates

## Motivation
- Instead of copy pasting functions, can we create a default template type that can process all types passed to it? 
- Avoid redundant overloaded functions
- Avoid copy pasting in code, instead we give this task to the compiler to figure out
- **__PERFORM FIND AND REPLACE__**: Compiler will generate code from **function template** by replacing **template type** with **concrete type**

## Function templates
```cpp
template <typename T>
T MinVal(T a, T b) {
    return (b > a) ? a : b;
}
```

**typename**
- keyword that introduces a type parameter
- T represents arbitary type
- any type can be used as long as its behavior is template defined 
    - **T must support operator ">"**

**Instantiation** = process of replacing template parameter by concrete types 

## Template Argument Deduction
The following calls will result in an error because they pass 2 different types
``` cpp
MinVal(2, 2.4);
MinVal(2.4, 2);
MinVal(2, 'a');
```

How to handle this?
1. Cast arguments so they are the same type
```cpp
MinVal(static_cast<double> (2), 2.4);
```
2. Explicitly state what types T can hold
```cpp
MinVal<double>(2, 2.4);
```
3. Specify strict type in function template, let compiler figure out return type
```cpp
template<type T1, type T2>
auto MinVal(T1 a, T1 b) { ... }
```

## Templates and Separate Compilation
- The definition of function templates are often not available until link time
- BUT we cannot wait till link time to access the implementation details
- **THUS** in this class, we will define the function template in the header files (.hpp)

**Min.hpp**
```cpp
#ifndef MIN_H
#define MIN_H
// declation
template <typename T>
T MinVal(T a, T b);

// definition
T MinVal(T a, T b) {
    return (b > a) ? a : b;
}
#endif
```

**Min.cc**
```cpp
#include "Min.hpp"

// template functions must be defined in header file 
```