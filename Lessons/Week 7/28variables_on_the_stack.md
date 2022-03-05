# 03/01/2022: Allocation of memory to variables on the stack

## Overview
**STACK**
- memory allocation to variables (named objects) on stack
- size of variables must be known
- see previous lesson for activation record

**FREE STORE**
- dynamic allocation of objects on free store
- we do not not need to know size of objects at compile-time
- memory can be requested at runtime

**STATIC/CODE**
- memory allocation for static and global variables

## Why the size of objects stored on stack miust be known at compile-time?
- If the size is known and the order in which activation record is pushed is also known **then the stack pointer is always at a fixed offset away**
- This way, past function calls can be be accessed at a known and predictable pointer distance!!!
- **PROBLEM**: an array with variable length is not supported by the C++ standard because we don't know how much space it needs in memory and **there is no standard offset for the stack pointer**!!
    - Variable lenght arrays (VLAs) are supported on C99 (C, not C++), some compilers allow you to do this because of extensions but you should not make VLAs in C++

## Stack Limitations
- **Array on stack**, we must know how to allocate for the array at compile-time, i.e. even before you read the data **==> free store takes of this later**
- Stack automatically dellocates space for that object once function returns, how to preserve objects in memory? **==> free store also takes care of this later**