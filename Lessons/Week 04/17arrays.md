# 02/08/22: Arrays

- These arrays are stored in the **stack** 
- Understanding arrays helps us better understand std::vector 

## Declaration
- **ALWAYS** store the size of the array in a variable when you declare because **arrays do not know their size!**
- They do not have any behavior to be called
- The size of arrays must be constant and known at compile time 

``` cpp
// create array x will store 7 int elements 
constexpr int x_size = 7;
int x[x_size];

// declare and initialize array y 
int y[] = {1, 2, 10, 3};
int y_size = 4
```

## Access
``` cpp 
int first_element = x[0];
int last_element = x[x_size - 1];
```

## Hack for finding array size
This formula divides the byte size of the entire array by the byte size of the first element, since all elements are of the same type this is shoyld give you the size of the array. **This only works in the same code block where the array is declared though**.
``` cpp
int x[] = {1, 1, 2, 2};
constexpr int size_x = sizeof(x) / sizeof(x[0]);
```

## Passing arrays
- When passed to a function, arrays decay into a pointer and loses all information
- We can still interact with the actual array using pointer arithmetic
- The address to the 0th element is stored in the name of the array when decayed, we can move the pointer along the array from element 0 to element i (whichever index we want), dereference int at that index in the array, and access it

## Array Limitations
- Size not known
- Potentially waste space or run out of space when we create arrays with unknown size
- Current best method is to use std::vector and .push_back()
- Array indices are not checking before accessing, so if we access an index out of range, it won't alert us with an error, it will just keep running 