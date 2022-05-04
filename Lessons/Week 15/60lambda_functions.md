# 04/28/22: Lambda Functions

## Intro
- An **anonymous function** is a function definition that is not bound to an ifentifier. 
- Anonymous functions are often arguments being passed to higher-order functions or used for constructing the result of higher-order functions that need to return a function. 
- Lambda expressions = easy to create function objects
    - Doesn't really add much new value
    - Just syntactical sugar 
- Lambda expressions is just an expressions
- **Closure** is the runtime object created by a lambda 
    - It can hold **copies of** or **references to** the captured data 

## Parts of a lambda expression
```cpp
[](...) mutable -> bool { do something, return true; }
// capture clause: lambda introducer
// parameter list (optional): lambda declarator 
// mutable specification (optional)
// trailing return type (optional)
// lambda body 
```

### Closure clause
- Captured by reference: prefix & 
- Captured by value: no prefix &
- Empty capture clause[] means lambda doesn't receive any variables from surrounding scope 
- [ & ] means all variables referred to are captured by reference
- [ = ] means all variables referred to are captured by value

### Parameter list
- Specify types and identifiers 

### Mutable specification 
- By default, captured by value variables are immutable 
- By writing mutable, captured by value variables are now mutable and **you can assign to them**

### Return type
- Often inferred so left empty
- But can specify explicitly 

### Lambda body
- Can contain anything an ordinary function contains
    - Captured vars
    - Parameters
    - Class data members
    - Statis storage (global vars)

## Lambda expressions as syntactic sugar for function objects
- Closure is instantiated from closure class
- Statements inside a lambda become executable instructions in the member functions

### Empty closure clause (no capturing)
```cpp
// lambda
auto lambda = [](const Movie& m) { return m.release_year < 1990; };

// equivalent code
class Functor {
public:
    bool operator()(const Movie& m) const { return m.release_year < 1990; }
};
```

### Capture by value
DATA MEMBER WILL BE CONSTANT!!! CANNOT DO (YEAR += 1) FOR EXAMPLE UNLESS WE MARK AS **MUTABLE**. 
```cpp
// lambda
unsigned int year = 1950;
auto lambda = [year](const Movie& m) { return m.release_year < 1950; };

// equivalent code
class Functor {
public:
    Functor(unsigned int year) : year_(year) {}
    bool operator()(const Movie& m) const { m.release_year < year; }
private:
    unsigned int year_; 
}
```

### Capture by reference
OBJECT CAPTURED CAN BE MODIFIED THE SAME WAY AS A PARAMETER PASSED BY REFERENCE!
```cpp
// lambda
unsigned int year = 1950;
auto lambda = [&year](const Movie& m) { return m.release_year < year; }
// equivalent code
class Functor {
public:
    Functor(unsigned int& year) : year_(year) { }
    bool operator()(const Movie& m) const { return m.release_year < year_; }
private:
    unsigned int& year_;
}
```