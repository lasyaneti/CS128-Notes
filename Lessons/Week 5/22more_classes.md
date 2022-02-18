# 02/15/22: Introduction to Classes, cont.

## Constructors, Destructors
- Object initialization doesn't automatically initialize the object's built-in types
- Constructors help us guarantee valid values for these built-in types

### Default Constructor
File: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
        Color();
    private:
        int r_;
        int g_;
        int b_; 
};
#endif
```

File name: color.cpp
``` cpp
#include "color.hpp";

Color::Color(): r_(0), g_(0), b_(0) {
    // values initialized using the constructor
    // initializer list 
}

// define other functions
```

## Parametrized constructors
File name: color.hpp
``` cpp
Color(int rr, int gg, int bb);
```

File name: color.cpp
``` cpp
Color::Color(int r, int g, int b): r_(r), g_(g), b_(b) {
    // check that assigned r_, g_, b_ values are valid 
}
```

## DO NOT use C++ assignment, use INITIALIZATION!!!
File name: color.cpp
``` cpp
#include "color.hpp"

Color::Color() {
    //  old C++ practices, use the above initializer list instead
    r_ = 0;
    b_ = 0;
    g_ = 0;
}
```

## Prevent narrowing conversion 
File name: color.cpp
``` cpp
#include "color.hpp"

Color::Color() : r_{0}, g{0}, b{0} {
    // check variable validity
}
```

## Public / Private Distinction
- Clean interface
- Easy debugging, only fixed set of functions can access data

**Guidance for attributes**
- Public = the value assigned will work regardless 
- Private = the value assigned to an object must be checked/conform to some requirements

## Interfaces
Good interface
- Small as possible, easy to understand/debug/maintain
- Complete
- Type safe, no confusing argumnet orders
- **const** correct

## Private member functions
- These can only be called by other functions in that class
- Keep public interface as minimal as possible

## Non-member helper function
- These do not access the representation of the instantiated object 