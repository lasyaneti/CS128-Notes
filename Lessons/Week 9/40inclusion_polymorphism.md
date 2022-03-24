# 03/24/2022: Inclusion Polymorphism

## Name Hiding
As demonstrated below, redefining behaviors within scope can be use to hide data. If no match found in inner scope, outer scope is searched.

### **Base class**
```cpp
// Animal header file
class Animal {
public:
    std::string Speak();
private:
};

// Animal source file
std::string Animal::Speak() {
    return "Generic animal noise.";
}
```

### **Derived class #1**
```cpp
// Parrot header file
#include "animal.hpp"
class Parrot : public Animal {
public:
    std::string Speak();
private:
}

// Parrot source file
std::string Parrot::Speak() {
    return "Polly wants a cracker.";
}

// Driver
Parrot polly;
polly.Speak();
```

### **Derived class #2**
```cpp
// Parrot header file
#include "animal.hpp"
class Cat : public Animal {
public:
    std::string Speak();
private:
}
// Parrot source file
std::string Cat::Speak() {
    return "Meow";
}

// Driver
Cat bubby;
bubby.Speak();
```

## Function Overriding and Virtual Functions
```cpp
// Driver
Cat bubby;
Parrot polly;

Animal& bubby_as_an_animal = bubby;
Animal* ptr_poly_as_an_animal = &polly;

std::vector<Animal*> animals;
animals.push_back(bubby_as_an_animal);
animals.push_back(ptr_poly_as_an_animal);

for (auto& animal : animals) {
    std::cout << animal->Speak() << std::endl;
}
// prints "Generic animal noise." twice
```

Is there a way we can access derived class behavior when we observe a derived type object through the lens of a base type (like example above)?

### Virtual function
Compiler will look for function in derived and then go up inheritance heirarchy

```cpp
// Animal header file
class Animal {
public:
    virtual std::string Speak();
private:
};

// Animal source file
std::string Animal::Speak() {
    return "Generic animal noise.";
}
```

Cool because collection of a base type (in this case, std::vector< Animal* >) can still access behavior of its derived objects!

## Polymorphic Behavior
Regardless of underlying type, all objects will do what is appropriate for that type

## Abstract base classes and pure virtual functions
- In our animal example, notice that there is not species called "animal" out there.
- We created a category to group all species like cat, parrot, etc.
- So it doesn't make sense for us to be able to create an object of type Animal

### How can we model this behavior?
1. **abstract** base class = Animal behaves only as a base class, cannot be created directly
2. **pure virtual functions** = all functions are made virtual and "=0"
```cpp
virtual std::string Speak() = 0;

// not we CANNOT create animal object, below results in compiler error
Animal animal; 

// overrided beheavior in derived classes can still be accessed
```

## Virtual destructors
At the end of object lifetime, destructor is responsible for releasing all resources owned by that object

### Animals Created on Free Store
```cpp
// Base class
virtual ~Animal();

// Driver
Cat* bubby = new Cat;
Parrot* polly = new Parrot;

Animal& bubby_as_an_animal = bubby;
Animal* ptr_poly_as_an_animal = &polly;

std::vector<Animal*> animals;
animals.push_back(bubby_as_an_animal);
animals.push_back(ptr_poly_as_an_animal);

for (auto& animal : animals) {
    delete animal;
}
```