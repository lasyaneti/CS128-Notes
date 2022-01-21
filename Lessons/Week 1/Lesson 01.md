# 01/18/21: Howdy, World!

## The Writing Process
- **Analysis**: requirements, figure out what should be done
- **Design**: determine overall system structure
- **Implementation**: writing code, debugging, and testing
- **Repeat**: development process requires iterations of improving solutions

## Language Syntax and Semantics
- Syntax is structure, semantics is meaning 
- It is possible to have syntactically correct statements, that are semantically wrong, ex: the statement is not doing what is intended or the statement causes the program to crash/produce an incorrect answer/behave incorrectly

## Classic First C++ Program
``` cpp
#include <iostream>

int main() {
    std::cout << "Hello, World!" << std::endl;
    return 0;
}
```

- Standard io is not a part of the core language, it must be included explicitly 
- All C++ applications must have a **main() function**, it is the entry point in the application
- Returning zero here signifies successful termination 
- Braces { } denote a code block, the body of the function
- std::cout is an output stream bound to the text terminal, any output the code generates is shown there 
- std::endl is also defined from iostream, it terminates the line
- std tells the program that this entity is defined in the standard namespace
- << is an insertion operator used to insert objects (in out case: "Hello World!") in output stream
- In C++, "double qoutes" denote strings