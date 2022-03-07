# 03/03/2022: An implicit contract with the free store manager

## The contract
- **CLAUSE 1**: must return memory borrowed, else **MEMORY LEAK**
- **CLAUSE 2**: must immediately stop using memory that is returned, else **DANGLING POINTER**
- **CLAUSE 3**: should not return memory that is not borrowed/return memory twice that is borrowed once, else **RUNTIME ERROR**

## Clause 1
Memory leaks occur when we dynamically allocate memory for an object, but fail to ever deallocate it

**__Incorrect way to deallocate:__** problematic because we have no way to access 7 and deallocate it!!
```cpp
// p is a pointer to a pointer to an int
int** p = new int*(new int(7));
delete p;
p = nullptr; 
```
**__Correct way to deallocate:__** delete the intermediarys first and then the address stored in p
```cpp
int** p = new int*(new int(7));
delete *p; *p = nullptr;
delete p; p = nullptr;
```

## Clause 2
- Dangling pointer is when you try to use a pointer to a piece of memory that has been deallocated 

```cpp
int* p = new int(7);
delete p; // dangling pointer
p = nullptr; // no longer dangling!
```

## Clause 3
```cpp
// single pointer p
int* p = new int(7);
delete p;
delete p; // ERROR

// double pointers to same object
int* p = new int(7);
int* op = p;
delete op;
op = nullptr;
delete p; // ERROR because pointer was deallocated
```