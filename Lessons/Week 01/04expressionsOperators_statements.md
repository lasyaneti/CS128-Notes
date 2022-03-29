# 01/21/22: Expressions and Statements

- Arithmetic operations are the same as basic math 
- The smallest piece of programming language that has meaning is called a token

## Basic Concepts 
Unary operator: -7
Binary operator: 7 + 3
Ternary operator: x = a ? b : c
Both: 8 - 7

## Grouping Operators/Operands
**Precedence**
- Multiplication/division have higher precedence than addition/subtraction
- Ex: 3 + 4 * 5 = 23

**Associativity**
- Arithmetic operators are **left to right** associative, ex: 20 - 15 - 3 = 2 
![Arithmetic Operator Precedence](/Images/ArithmeticOperatorPrecedence.png)

- Assignment operators are **right to left** associative
``` cpp
int i = 0
int j = 1
i = j = 5; // i gets 5, not 1
```
![Logical Operator Precedence](/Images/LogicalOperatorsPrecedence.png)

**Order of Evaluation**
- Unspecified, it changes based on the implementation 
``` cpp
int i = f1() * f2();
// under the assumption that f1 and f2 are manipulating the same data
```

## Statements
Simple statements in C++ end with a semicolon 
``` cpp
int n = 3;
```
The most simple statement is an empty statement
``` cpp
;
```

Compound statements, AKA blocks, are bound by curly braces and not terminated by semicolon

## Branching: if/else
If statements are executed if conditional is true
``` cpp
std::cout << "Freeze warning should ";
if (temperature <= 32)
    std::cout << "be issued." << std::endl;
else
    std::cout << "not be issued." << std::endl;
```

The else branch need not be specified if the program is modified like so:
``` cpp
std::cout << "Freeze warning should ";
if (temperature > 32)
    std::cout << "not" << std::endl;
std::cout << " be issued." << std::endl;
```

Branches of if statements are scopes, i.e. variable created inside cannot be accessed from outside.

Else if is a compound statement 
``` cpp
if (number % 15 == 0) {
    // statement 1
} else if (number % 3 == 0) {
    // statement 2
} else if (number % 5 == 0) {
    // statement 3
} else {
    // statement 4
}
```

Convention (Google C++ Style Guide)
- Use curly braces for if, else if, else
- Put one space between the following
    - if and the opening parenthesis
    - closing parenthesis and the curly brace
- NO spaces between the parentheses and the condition 
- Break line after opening brace, all subsequence else/if statements must be on the same line with a space 

Principles of if 
- Write the common cases first, usual oines later
- Encode complex boolean expressions in methods, naming methods the meaning of the expression 

## Branching: switch
- Allows selection based on comparison of a value against several constants
- Each case is terminated by **break**
``` cpp
switch (op_code) {
    case 0: {
        z = x - y;
        break;
    }
    case 1: // fall through because NO BREAK
    case 2: {
        z = x + y;
        break;
    }
    default: {
        assert(false);
    }
}
```

Technicalities and Convention
- We must switch on the value of an integer, char, or enumeration type 
- Case label must be known at compile time, i.e. no variable
- Case label values must be unique 
- If there is no break, you should make a comment that fall through is intentional
- Remember to end cases with break!
- If conditional is not enumerated value, you should always have a **default case**

## Iteration: while loop
- Repeatedly execute a statement as long as the condition is true
- Condition must converge to smaller steps so the loop can terminate 
``` cpp
int x = 10;
while (x > 1) {
    std::cout << x << std::endl;
    x = x - 1;
}
```

## Iteration: do-while loop
- Similar to while, but it is guarunteed to execute at least once since the condition is checked at the end
- std::cin takes input from keyboard
``` cpp
int x = -1;
do {
    std::cout << "Enter a positive number: ";
    std::cin >> x;
} while (x <= 0);
```

## Iteration: for loop
- Similar to while, but the management of the conditional is at the top
- This is easier to understand
- Variables created in the initialization of the for loop can only be used inside the loop, increment the control variable only inside the header 
Header contains:
- Initialization of the control variable
- Continuation criterion
- Step operation 

Program below prints squares of numbers 1 through 10, inclusive
``` cpp
for (int i = 1; i <= 10; ++i) {
    std::cout << i << '\t' << pow(i, 2) << std::endl;
}
```

## Loop Control
- **break** = terminates the loop entirely
- **continue** = ends the current iteration and continues with the subsequent iteration
