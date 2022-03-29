# 01/27/21: Command Line Arguments

2 parameters can be passed to the main() function: 
- argc stores the argument count 
- argv stores the arguments in a vector, starting with argv[0] as the exec file commmand

``` cpp
#include <iostream>
#include <string>

int main(int argc, char* argv[]) {
    // you can use strings passed to the program from the terminal when it is executed
    std::string arg = argv[0];
}
```

If bash command is used incorrectly, the output is a "usage" error along with the exec name. 

When you need to deal with command line arguments:
- Check to see the number of arguments passed
- C style strings need to be converted into std::strings 
