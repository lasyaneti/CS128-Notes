# 01/24/21: Introduction to Functions

## Writing Functions Well (clean code)
Functions are important because they organize any program by compartmentalizing behavior. Functions should have the following:
- Intuitive and consistent names
- One level of abstraction
- Not longer than 40 lines
- Ideally 0-1 arguments, no more than 3! 
- Use if/else statements to call functions
- Top-down narrative


## Functions (based on # of arguments)
### Monadic Functions
Reasons for writing functions with 1 argument:
- Ask a question about the object
- Perform an operation on an object, returned transformed object 

Function name should be in the verb-noun pair form.

### Dyadic Functions
These are sensible when parameters have a natural ordering. Still, convert to monadic when possible. These function names should be desriptive and tell you what information you need to provide for both arguments, i.e. programmer shouldn't have to take a second look at the function signature 

### Triadic Functions 
Use only after careful consideration, ex:
``` cpp
// triad
Circle MakeCircle(int x, int y, int radius) { } ;

// dyadic
Circle MakeCircle(int center, int radius) { } ;
```

## More Notes
- Functions should only do one thing, it should be predictable behavior 
- All of the things we need to know to call a function should be there in the first line
- Do not pass booleans!
- Repeated code increases risk for error
- Refactoring code into functions helps compartmentalize behavior
- Line breaks in functions indicates seperate thoughts, use them carefully!

## C++ Syntax
- base type (return type)
- identifier (name)
- list of parameters seperated by commas
- function body

## C++ Functions
Function declaration
``` cpp
int Square(int x);
```
Function definition
``` cpp
int Square(int x) {
    return x*x;
}
``` 
In our case, we will do the declaration of the function in the header file (.h), define the function in a different file (.cc), and include the file in our main file. **This way, we never need to see the C++ files, the header file tells us all the functions avalible to us and what informatin they use/return!** 

### my_math_ops.h
``` cpp
#ifndef MY_MATH_OPS_H
#define MY_MATH_OPS_H

    int Square(int x);

#endif
```

### main.cc
``` cpp
#include <iostream>
#include "my_math_ops.h"

int main() {
    int num = 0;
    // take user input
    std::cin >> num;
    // function call
    int num_squared = Sqaure(num);
}
```

### my_math_ops.cc
``` cpp
#include "my_math_ops.h"

int Square(int x) {
    return (x * x);
}
```

## What happens when function is called?
1. Function's parameters are initialized
2. Control is transferred to Square 
3. Return value is transfered back to calling function

## HW Tip
``` cpp
// Use division by 10 to chop int by 1 digit
// Use modulo by 10 to retrieve last digit

int n = 123;
int lastDigit = 0;

n = n / 10;
lastDigit = n % 10;
// NOW: n is 12, lastDigit is 2
n = n / 10;
lastDigit = n % 10;
// NOW: n is 1, lastDigit is 1
```