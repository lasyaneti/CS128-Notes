# 02/08/22: Pointers

## Review Terms
- **Type**: defines a set of possible values and a set of operations for an object
- **Object**: abstraction of a memory cell that holds a value of given type
- **Value**: set of bits in memory interpreted according to the type
- **Variable**: name of object
    - **Name**: letters/digits
    - **Address**: variable is associated with this machine memory address
    - **Type**: determines range of values that can be stored
    - **Value**: contents of memory cell or cells associated with the variable 
    - **Scope**: part of the program where the variable has meaning
    - **Lifetime**: object's lifespan from allocation to deallocation
- Different objects take up different space and can store a different range of objects

## Review Declaring Variables
4 parts as follows:
- **SPECIFIER** (optional), ex: const
- **BASE TYPE**, ex: int
- **DECLARATOR**, postfix/prefix name/symbol that tells you more about the variable 
    - prefix for pointers: *
    - prefix for constant pointers: *const
    - prefix for reference: &
    - postfix for array: []
    - postfix for function: ()
- **INITIALIZER** (optional), ex: = 5;

## Pointers
- Pointer is an object, its value is the address of another object
- In the example below, both p and i are variables of objects (pointer and int, respectively) and so have their own addresses. The point of a pointer is to get the address of i and store it as the value of p

``` cpp
int* p = nullptr; 
// p is a pointer to an integer object
// initialized here with null pointer, p currently points to nothing 

int i = 7;
p = &i; 
// address of i assigned to p, p currently points to i
```

## Making an indirect assignment through pointer
| **&p** | **p** | **\*p** |
| -- | - | -- |
| 0x7ffc73fa460 | 0x7ffc73fa467c | 7 |
 
Here, * is a unary operator in an expression, not variable declarator! It is dereferencing. It looks at pointer p -> goes to address of p -> gets that value of the object pointer points to

``` cpp
int i = 7;
int* p = &i;
int j = *p;
// int i stores 7, int j stores 7
*p = 4;
// int i stores 4, int j stores 7
```

## Declarator vs Operator (* and &)

### & operator. r stores reference to i
``` cpp
int i = 11;
int& r = i;
```

### * declatator, & operator. pointer p stores address of i
``` cpp
int i = 11;
int* p = &i;
```

### * declarator, & operator, * operator.
``` cpp
int i = 11;
int* p = &i;
*p = 2;
```
