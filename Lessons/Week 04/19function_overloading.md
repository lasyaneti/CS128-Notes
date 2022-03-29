# 02/11/22: Function overloading 

- Compiler decides which function to call by comparing arguments
    - Exact match (int passed, int found)
    - Match through promotion (char passed, int found)
    - Match using standard conversions (int passed, double found)
- If there isn't an exact call, and the compiler finds multiple compatible matches, it will report an **ambiguous call error**

``` cpp
bool AreEqual(int a, double b);
bool AreEqual(double a, int b);

// call made
AreEqual(2.5, 3.4);

// results in error: call to 'AreEqual' is ambiguous
```

## Guidance
- Use overloading when functions perform same operation (name same) but needs to handle significantly different data types
- Else, construct functions with different names