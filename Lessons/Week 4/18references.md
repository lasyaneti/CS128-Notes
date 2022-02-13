# 02/10/22: References and argument passing

## References
**Pass by value** 
- This is when the parameter is an object and a value is copied into the parameter object for initialization
- Changes made in the function do not change argument because we are working with copies created at parameter initialization
``` cpp
int add(int a, int b) { return a + b; }

int main() {
    int i = 4;
    int j = 6;
    int k = add(i, j);
}
```

**Swap variables**
- Works when swap occurs in main()
``` cpp
int main() {
    int i = 1;
    int j = 2;

    int temp = i;
    i = j;
    j = temp;
}
```

- Passing by value doesn't work with swap function!!! The code below doesn't actually swap the values of int i and j
``` cpp
int Swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int i = 1;
    int j = 2;
    swap(i, j);
}
```

Can functions change the actual value of variables? YES! This is where we use pass by reference

## Creating references 
- Reference: an alias or nickname for an object
- They both refer to the SAME object (same address) 
``` cpp
int i = 1;
int& ii = i; // reference for i
int j = 2;
const int jj = j; // constant reference, read-only
```

All references MUST be initialized at the point of declaration because they cnanot be re-referenced to another object! **Compilation error:**
``` cpp
int& a;
```

References cannot bind to literals! Only variables of objects. 
``` cpp
int& a = 11; // error
```

We are allowed to take a reference to const to a literal though:
``` cpp
const int& a = 11;
```

## Pass by reference
In this example, changes made in the passed reference will always be reflected in the actual objects bound to the reference. 
``` cpp
void swap(int& a, int& b) {
    int temp = a;
    a = b;
    b = temp;
}

int main() {
    int i = 1;
    int j = 2;
    swap(i, j);
}
```

## When to pass by reference


## Guides for passing arguments 