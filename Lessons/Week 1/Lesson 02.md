# 01/19/22: Objects, types, and values

## Terminology

| Term | Definition |
| ---- | ---------- |
| Type | Defines a set of possible values, along with a set of operations for that object |
| Object | Abstraction of a computer memory cell |
| Value | Bits in memory interpreted according to type |
| Variable | Named object |
| Declaration | Gives name to an object |
| Definition | Declaration that sets memory aside for an object |

## Primitive (built-in) Types
### bool 
- Logical values
- true or false
- Booleans are converted into integers (true is 1 and false is 0), logic is applied on this converted value, a nonzero result is true vs. a zero result is false
### char 
- Characters
- 'a', 'b', 'c'
- Each character has a constant integer value
- There are integral so logical and arithmetic operators can be applied to these
- Can store 26 English alphas, digits 0-9, basic punctuation characters 
- Escape sequence characters use backslashs: '\n', '\t', '\0', etc.
### int 
- Integer value: short, int, long
- 10, 29, 992492
- ints come in signed/unsigned form, signed is default for "plain" ints
- Integer literals: decimal (base 10)
  - Prefix: 0b is binary (base 2), 0 is octal (base 8), 0x is hexademical (base 16)
  - Suffix: U for unassigned literals, L for long literals

### double 
- Floating-point values, computer's approximation of a real number 
- 4.5, 6.3, 9.2
- The meaning of float (single-precision, suffix F) vs. double (double-precision) vs. long double (extended-precision, suffix L) are implementation defined 

## Compound Types
- Pointer type: int*
- Array type: char[]
- References: int&
- Data structures and classes

## Variables 
- Variables have 6 attributes: name, type, address, scope, value, lifetime
### Name
- Rules
    - First character must be a letter 
    - C++ is case-sensitive
    - Underscore is allowed, but if name starts with an underscore, convention indicates that it is a language facility
    - Keywords cannot be used as names
- Convention
    - Descriptiveness of a name should be proportional to the scope
    - Do not use abbreviations that others would not understand
    - Google C++ Style Guide
        - Names are all lowercase, underscores between words to represent spaces 
        - In Classes, we use a trailing underscore at the end

### Address
- Variable's location in machine memory 
- Alias: multiple names associated with the same address, any change to one alias changes all other aliases 

### Value
- The value is the contents of the memory cell associated with the variable

### Lifetime
- Binding between an attribute and an entity 
- **Allocation** is the process of taking the memory cell that is associated with the variable from the pool or available memory
- **Deallocation** is the process of replacing a memory cell back into the pool of available memory
- The lifetime is the time during which the variable is bound to a specific memory location

### Scope
- Part of the program where a variable name has meaning
- Most scopes are enclosed in curly braces
- Local (where variable is declared) vs. non-local (where variable is not declared)
- Two variables can have the same name in different scopes
- Nested scope allows to hide variables and have different uses for inner vs. outer scope
- Variables can be declared anywhere, but it is good practice to define them closest to the first use and initialize immediately after declaration

## Declaration
- Before the name, we must specific the type for the compiler
- Many declarations are also definitions, all the built-in primitive types have default values

``` cpp
const int i = 2;
```

| Specifier (optional) | Base type | Declarator | Initializer (optional) |
| -------------------- | --------- | ---------- | ---------------------- |
| const | int | i | = 2 |

### Declarator 
- Optional add-on for  base types
- Postfix binds tighter than prefix 
- These apply to individual names only 

| Declarator | What it is | Where |
| ---------- | ---------- | ----- |
| * | pointer | prefix |
| *const | constant pointer | prefix |
| & | reference | prefix |
| [] | array | postfix |
| () | function | postfix |

## Constants 
- Name starts with k, camel case capitalization 
``` cpp
const int kReadOnlyVariable = 7;
```

## Initialization and Assignment 
Initialization
- Before: box is empty
- After: box holds a coin
- Reinitialize: remove the first coin, put in new coin

Good practice: declare and initialize at the same time
``` cpp
int a = 5
```
Bad practice: declare and initialize seperately -> declare, initialized with random value, assignment
``` cpp
int a; // a has been allocated space
a = 5; 
```