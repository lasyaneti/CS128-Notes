# 03/03/2022: Two-dimensional arrays on the free store

## Pointer Review
- Pointer stores an address to an object 
- Writing "new int" returns address from free store
- Pointer and new operator go hand in hand 

```cpp
// POINTER TO A POINTER TO AN INT
int** p = new int* {new int{7}};

/*
above is the same as
int** p = new int*;
*p = new int{7};
*/
```

## 2d arrays on free store

## Passing 2D arrays 
- Requires you to pass row and col dimensions because arrays are not aware of their size
- Pass the inner array of pointers instead of a pointer to the array of pointers!