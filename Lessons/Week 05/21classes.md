## 02/14/22: Introduction to classes

## What is a class?
- User-defined type that has representation:operations::attributes:behaviors 
- Class is a template from which objects of the class-type can be created 

## struct vs. class
- Members of a struct are PUBLIC by default, can be accessed with dot notation (c.r)
- structs are used in data structures where the members can take any value 
``` cpp
struct Color {
    int r;
    int g;
    int b;
}
```

- Members of a class are PRIVATE by default, cannot be accessed with dot notation (c.r)
``` cpp
class Color {
    int r_;
    int g_;
    int b_;
}
```

## Writing a class
- **accessor**: function that returns the value stored in a private data member
- **mutator**: function that stores a value in private data member or mutates its state
- Prefix function name like so "class_name::function_name", :: is called the score resolution operator

## C++ class structure
### color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
    // include elements of Color's interface
    // any functions in any class can access these public data members 
    void r(int rr);
    void g(int gg);
    void b(int bb);
    int r() const;
    int b() const;
    int g() const;

    private:
    // include elments of Color's implementation
    // private data members can only be accessed by members that are part of that class
    
    // convention to mark private local variables followed by an underscore
    int r_;
    int g_;
    int b_;
    // static marks that these variables are shared across all instances of this class
    static constexpr int kMaxColorValue = 255;
    static constexpr int kMinColorValue = 0;
};
#endif
```
### color.cpp
``` cpp
#include "color_hpp"

// mutator
void Color::r(int rr) {
    if (ValidColorValue(rr)) {
        r_ == rr;
    } else {
        throw std::runtime_error("Invalid Value");
    }
}

// accessors
// const appears after call to indicate that function will not change state of object for which it is called 
int Color::r() const {return r_; }
int Color::g() const {return g_; }
int Color::b() const {return b_; }

// helper function
bool Color::ValidColorValue(int value) const {
    if (value >= kMinColorValue && value <= kMaxColorValue) {
        return true;
    } else {
        return false;
    }
}
```

### main.cpp
``` cpp
int main() {
    Color c;
    c.r(255);
    std::cout << c.r() << std::endl; // prints 255
    c.r(11);
    std::cout << c.r() << std::endl; // prints 11
    c.r(-30); // THROWS ERROR: INVALID VALUE
    return 0;
}
```
