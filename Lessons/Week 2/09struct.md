# 01/27/22: struct

## struct 
- std::vector holds elemets of the SAME type
- structs can hold arbitrary types 

``` cpp
struct Contact {
    std::string first_name;
    std::string last_name;
    long phone_number;
    std::string email;
}; 

// this defines a new type called CONTACT consisting of items you can store as entry in say, a phone book!

// use dot (.) notation to access elements
Contact person;
person.first_name = "Lasya";
person.last_name = "Neti";
person.phone_number = 123456789;
person.email = "abc@illinois.edu";

// uniform initialization
Contact person = {"Lasya", "Neti", 123456789, "abc@illinois.edu"};`
```

## Shortcomings of structs (right now)
- No mechanism for figuring out if two structs are equal (like the Java objects equals() function)
- No mechanism to print contents of a struct (like Java object toString() function)

## Google C++ Style Guide for structs 
- struct type name must start with capital letter nad have a capital letter for each new word, no underscores
- Data members are all lowercase with underscores between words 
- Use a struct **only** for passive objects that carry data 
- Use **struct** over **pair** or **tuple** since they are more structured, especially when elements can have meaningful names

### file: contact.h
``` cpp
#ifndef CONTACT_H
#define CONTACT_H

#include <string>

struct Contact {
    std::string first_name;
    std::string last_name;
    long phone_number;
    std::string email;
};

#endif
```

### file: main.cc
``` cpp
#include <iostream>
#include "contact.h"

int main() {
    Contact person = {"Lasya", "Neti", 123456789, "abc@illinois.edu"};
}
```