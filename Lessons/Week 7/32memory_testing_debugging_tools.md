# 03/04/2022: Tools of testing and debugging memory issues

## Memory Safety
**Out of Bounds**
- Occurs when accessing address beyond allocation
- Causes crashes/corrupt other data
```cpp
const unsigned int kArraySize = 10;
int* array = new int[kArraySize];
// out of bounds occurs because <= array size (OFF BY ONE ERROR)
for (unsigned int i = 0; i <= kArraySize; i++) {
    array[i] = 0;
}
```

**Use After Free**
- Attempting to access memory after deallocation
- Write to freed memory gets lost, read from freed memory is garbage
```cpp
struct Node {
    int data = 0;
    Node* next = nullptr;
};

Node* n1 = new Node{1};
n1->next = new Node{2};
while (n1 != nullptr) {
    delete n1;
    n1 = n1 -> next;
}
```
- Pointers and arrays touch hardware directly; segmentation fault, bus error, core dumped = uninitialized or invalid pointer

**Memory Leak**
- Causes memory usage to balloon while program is open
- Problematic in long-running programs
- Array off by one error when not initialized on the free store, the typical out of bounds error is not thrown
- Forgetting to return a value

## Tools

### ASan
- AddressSanitizer (ASan)
- Detects out of bounds, use-after-free, use-after-return, double-free/invalid-free
```
clang++ ... -g -fsanitize=address,null -fno-omit-frame-pointer
```

### UBSan
- Detects undefined behavior: null pointers, array out of bounds, divide by zero, interger overflow, implicit conversions
```
clang++ ... -g -fsanitize=undefined
```

### Valgrind
- Detects memory leaks (memcheck), invalid pointer use, uninitialized variables
- Standalone tool not in compiler, use while running code
- Slows execution between 10-50x
```
clang++ ... -g
```
**Use specific tool when you run the code**
```
valgrind --tool=memcheck program_name
```