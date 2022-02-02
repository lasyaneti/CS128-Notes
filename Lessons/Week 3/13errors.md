# 02/02/22: Software and Errors

## Readable Code
- Use meaningful names
- Don't use names that are super close with tiny, missable differences 
- Use pronounceable names
- Avoid single-letter variables
- Pick one word per concept 

## Compile Errors
- Finds syntax (ex: missing semi colon) and type errors (ex: assigning literal to variable of different datatype)

## Link-Time Errors
- Errors when linker is trying to combine object files into an executable program 
- Once names are defined, the linker must be able to find their definitions, references, etc.
- Linker also alerts if you defined a function in more than one way

## Runtime Errors
- Detected by computer: int division by 0
``` cpp
int numerator = 1;
int denominator = 0;
int result = numerator / denominator; 
```

- Detected by library: index out of range  
``` cpp
std::vector<int> my_values {1, 2, 3};
for (int i = 0; i <= my_values.size(); i++) {
    std::cout << my_values.at(i) << std::endl;
}
```

- Detected by user-code: we write our own code to error-handle 
``` cpp
int positive_val = 0;
std::cin >> positive_value;
if (positive_value <= 0) {
    return 1;
}
```

## Logic Errors
- Also occur at runtime
- When the code itself is not doing what is intended