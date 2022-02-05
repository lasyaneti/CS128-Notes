# 01/04/21: Testing and Debugging 

## Assert 

- If the result is false, the program will terminate immediately and print an error (includes line number of error)
- Asserts are useful to check if post-conditions are met

### driver.cc
``` cpp
#include <cassert>

int kLargestPossible = 1000;
int num_of_elements = -1;
assert (kLargestPossible >= num_of_elements);
assert (num_of_elements > 0);
```

## error in standard out
a.out: driver.cc:12: int main(): Assertion 'num_of_elements > 0' failed.

## Assert vs. Exceptions
- Asserts are used to detect programming errors made by us
- If we receive input from an external source, this is ideal for the use of exceptions

## Formal Testing
- **Unit Testing**: 
    - Written by programmers for programmers
    - The intent is to test the system at the lowest level, in isolation from the rest of the system
    - Ideally you should have 100% coverage, 90%+ is the goal
- **Component Testing**:
    - Written against individual components of the system
    - To check that something we are building is working, like classes/struct/etc.