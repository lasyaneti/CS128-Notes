# 03/23/2022: Inheritance

## Motivation
- Classes can model both concrete and abstract objects 
**Modeling: truck -> fire truck, concrete truck**
- Truck models general overall behavior
    - Fire truck has the same behaviors as generic truck, but also details that specifically make it a fire truck
    - Concrete truck has the same behaviors as generic truck, but also details that specifically make it a concrete truck

You could create 3 separate classes but that would use a lot of copy/pasted code. You could create one "Super Truck" that had the behavior of all 3 trucks but that isn't efficient, giving unnecassary features to the truck. **Inheritance allows us to create a heirarchy of behavior**: 
- parent class 
- subclass 1.1, subclass 1.2 
- subclass 1.1.1, subclass 1.1.2, subclass 1.2.1, subclass 1.2.2

Every child truck has the attributes of its parent class(es).

## Inheritance
**IMPLEMENTATION INHERITANCE**
- Derived classes can take advantage of existing behavior (data and member functions) in parent classes
```cpp
// Forward() is a behavior of parent class Truck, but subclasses model this behavior as well
// calling on object
FireTruck ft;
ft.Forward();
```
**INTERFACE INHERITANCE**
- Given visibility is public, the derived classes can do everything that the base class can do
```cpp
// passing object by reference
Firetruck ft;
GotoLocation(ft);
void GotoLocation(const Truck& t) { ... }
```

## Visibility of Inheritance
``` cpp
class Truck {
public:
    // if Truck class definition is known, these can be accessed
    int x;
protected:
    // only Truck and Truck children can access
    int y;
private:
    // only THIS Truck can access
    int z;
};
```

Ex: FireTruck - **public inheritance** - "is-a"
```cpp
class FireTruck : public Truck {
/* 
FireTruck knows its parent
if FireTruck is known, it is also known that FireTruck inherits from Truck
-- x still public
-- y still protected 
-- z cannot be accessed by FireTruck (private in Truck)
*/
}
```

Ex: FireTruck - **protected inheritance**
```cpp
class FireTruck : protected Truck {
/* 
only FireTruck, FireTruck children know they inherit from Truck
-- x is protected (accessible to FireTruck/its children)
-- y still protected 
-- z cannot be accessed by FireTruck (private in Truck)
*/
}
```

Ex: FireTruck - **private inheritance** - "implemented-in-terms-of"
```cpp
class FireTruck : private Truck {
/* 
only FireTruck, FireTruck children know they inherit from Truck
-- x is private (accessible to FireTruck only)
-- y is private (^^)
-- z cannot be accessed by FireTruck (private in Truck)
*/
}
```

## Inheritance, conceptually
- If you do not provide a constructor/destructor in base class, compiler will create one, **called implicitly**
- If we do not provide a constructor/destructor in derived class, compiler will create one
- When derived constructor/destructor are called, the base class constructor/destructor are implicity called 

**Initializer list can initialize parent class items**
```cpp
// base class constructor
Parent::Parent(std::string str) : str(str) { ... }
// derived class constructor
Child::Child(std::string str) : Parent(str) { ... }
```

- If derived class hasn't defined a data member/function, compiler will look in parent class. 
- **Overloading an operator in derived class does not trigger the base class definitions.**

This way parent is always resposible for its portion and child is reponsible for its portion.  
```cpp
Child& operator=(const Child& other) {
    // initialize base portion
    Parent::operator=(other);
    // initialize child portion
    // define 
    return *this;
}
```

## Additional Examples
- Data members of base type are constructed by base constructor, derived portion is contructed by derived constructor

**BASE: TRUCK**
```cpp
Truck::Truck(unsigned int weight, FuelType fuel_type, unsigned int length, unsigned int height) : weight_(weight), fuel_type_(fuel_type), length_(lenght), height_(height) {
    // base constructor
}
```
**DERIVED: FIRETRUK**
```cpp
FireTruck::FireTruck(unsigned int weight, FuelType fuel_type, unsigned int length, unsigned int height, unsigned int water_capacity) : Truck(weight, fuel_type, length, height), water_capacity_(water_capacity) {
    // derived constructor
    // notice call to base constructor in initialization list
}
```

- References/Pointers
```cpp
// only base type components are stored here
// shifting perspective of EXISTING object
Truck& big_red_truck_base = big_red_truck;
Truck* ptr_to_big_red_truck_base = &big_red_truck;

PassedByReference(big_red_truck);
// look at big_red_truck through lens of base

// object slicing
// creating a NEW object
Truck red_truck = big_red_truck;

PassedByValue(big_red_truck);
// object slicing
```

