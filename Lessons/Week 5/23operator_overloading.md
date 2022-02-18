# 02/16/22: Operator Overloading

- Overloaded opeator has the same number of parameters as operator has operands, number of paramters defines unary vs binary
- We can only overload existing operators, cannot invent new ones

## Calling non-member overloaded operator
Using the operator on arguments of suitable type
- something + something_else

Using the familiar function call syntax
- operator + (something, something_else)

## Calling member overloaded operator
Frequently used
- something + something_else
- something.operator+(something_else)

## Guidelines for member vs non-member operators
**MEMBER**
- Assignment (=), subscript([]), call(()), and member access (->) 
- Compound assignment operators (+=, -=, etc.)
- Operators that change state of object
**NON-MEMBER**
- Symmetric operators defined as non-members
- We want to use symmetric operators in expressions with mixed types 

## Example 1: overloading operator = 
File name: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
        Color& operator=(const Color& rhs);

    // etc... same definitions as before
};

#endif
```

File name: color.cpp
``` cpp
#include "color.hpp"

// rhs is color object that is being passed
// indicate member function by adding "Color::"
Color& Color::operator=(const Color& rhs) {
    // since part of color class, this function has raw access to private data members r_, g_, b_
    r_ = rhs.r_;
    g_ = rhs.g_;
    b_ = rhs.b_;
    // convention: return self reference to object 
    return *this; 
}

// etc... other definitions 
```

## Example 2: overloading operator += 
File name: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
        Color& operator+=(const Color& rhs);
    // etc... same definitions as before
};

#endif
```

File name: color.cpp
``` cpp
#include "color.hpp"

Color& Color::operator+=(const Color& rhs) {
    r_ (r_ += rhs.r_) / 2;
    g_ (g_ += rhs.g_) / 2;
    b_ (b_ += rhs.b_) / 2;
    return *this;
}

// etc... other definitions 
```

## Example 3: overloading operator-- (postfix)
File name: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
        Color& operator--(int);
    // etc... same definitions as before
};

#endif
```

File name: color.cpp
``` cpp
#include "color.hpp"

Color& Color::operator--(int) {
    Color old_state = *this;
    // do something, define yourself based on what you think behavior should look like
    return old_state;
}

// etc... other definitions 
```

## Example 4: overloading operator + 
File name: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

class Color {
    public:
        // definitions
    private:
        // definitions
};

// since declaration outside class, we pass both args
Color operator+(const Color& lhs, const Color& rhs);

#endif
```

File name: color.cpp
``` cpp
#include "color.hpp"

Color operator+(const Color& lhs, const Color& rhs) {
    Color blend;
    // non-member function, use accessors and mutators
    blend.r( (lhs.r() + rhs.r()) / 2 );
    blend.g( (lhs.g() + rhs.g()) / 2 );
    blend.b( (lhs.b() + rhs.b()) / 2 );
    return blend;
} 

// etc... other definitions 
```

## Example 5: overloading operator << 
File name: color.hpp
``` cpp
#ifndef COLOR_HPP
#define COLOR_HPP

#include <iostream>

class Color {
    public:
        // definitions
    private:
        // definitions
};

// insertion operators must be defined as on-member
std::ostream& operator<<(std::ostream& os, const Color& color);

#endif
```

File name: color.cpp
``` cpp
#include "color.hpp"

// returning reference to stream
std::ostream& operator<<(std::ostream& os, const Color& color) {
    os << color.r() << '\t';
    os << color.g() << '\t';
    os << color.b();
    return os;
}

// etc... other definitions 
```