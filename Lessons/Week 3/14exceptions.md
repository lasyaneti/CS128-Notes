# 02/03/22: Exceptions

When an unexpected condition occurs, you can handle it by throwing an exception

## Try-Catch
### main()
``` cpp
try {
    double area = AreaRectangle(-10, 10);
}
catch (const std::runtime_error& e) {
    // handle the error 
    // set area to 0 by default when any and all errors thrown
    area = 0;
}
```

### actual cpp file
``` cpp
double AreaRectangle(double width, double height) {
    double area = width * height;
    if (area < 0) {
        throw std::runtime_error("InvalidArea");
    }
}
```

## Notes
- NEVER use exceptions to handle local-errors, i.e. catching errors right there in the same file 

## <stdexcept>
- You cannot "throw std::exception", but you can throw any children exceptions
- **std::runtime_error(std::string)** is thrown during runtime 
- **std::logic_error(std::string)** is an exception thrown during runtime for logical errors
- **std::invalid_argument** is thrown to alert the user that the input is invalid 

## Pre/Post Conditions
| Precondition | Postcondition |
| ------------ | ------------- |
| A condition/predicate must be true just prior to the execution of some section | A condition that must be true after the execution of some section of code |
| If the precondition is violated, the effect of the code is undefined | Provided a valid precondition, we should arrive at the valid postcondition, though sometimes we'll need to check |