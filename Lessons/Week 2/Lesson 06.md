# 01/26/22: Compound Data

## std:vector<element_type>
- Vectors work similar to arrays, **sequence of elements** that can be accessed by **index** (starts with 0)
- Vector stores elements and size
- See all vector functions at the [API](https://en.cppreference.com/w/cpp/container/vector) 


``` cpp
#include <vector>

// initialize with list 
std::vector<int> v = {1, 2, 3, 5};

// declare with vector size 4
std::vector<double> v(4);

// declare with vector size and specified default value
std::vector<double> v(4, 1.5);

// access elements
v[2];
v[2] = 10;

// better way to access elements because it throws an obvious error when index greater than vector size
v.at(2);
v.at(2) = 20; 
```

### Traverse Vector
``` cpp
// for loop
for (size_t index = 0; i < v.size(); ++index) {
    std::cout << vect.at(index) << " ";
}

// enhanced for loop
for (int val : v) {
    std::cout  << val << " ";
}
```

### Vector push_back()
``` cpp
std::vector<int> vect;

vect.push_back(10);
// vect is now: [10]
vect.push_back(1);
// vect is now: [10, 1]
```

## 2D Vector 
``` cpp
// each type within the bigger vector is an int vector
std::vector<std::vector<int>> vect;
std::vector<int> a = {1};
std::vector<int> b = {2, 3};
vect.push_back(a);
vect.push_back(b);

// access 2D vector
vect.at(1).at(1); // = 3

// declare 2D vector with size
unsigned int height = 4; 
unsigned int width = 2;
std::vector<std::vector<int>> = vect(height, std::vector<int>)(width, 0);

/* vect looks like
|---|---|
| 0 | 0 |
|---|---|
| 0 | 0 |
|---|---|
| 0 | 0 |
|---|---|
| 0 | 0 |
|---|---|
*/
```

### Traverse 2D Vector
``` cpp
for (size_t row = 0; row < vect.size(); ++row) {
    for (size_t col = 0; col < vect.at(row).size(); ++col) {
        std::cout << vect.at(row).at(col) << " ";
    }
    std::cout << std::endl;
}
```

## std::string
- All functions avalible at [API](https://www.cplusplus.com/reference/string/string/)

``` cpp
#include <string>

std::string full_name : "Lasya";

// concatenate
full_name = full_name + " Neti"; 

// substring
std:string first_name = full_name(0, 5);

// char at
char c = full_name.at(0);
```

## std:map<type_key, type_value>
- key-value pairs
- Keys must be unique  
- If key has no pairing, value is assigned default value
- [API](https://www.cplusplus.com/reference/map/map/) 

``` cpp
#include <map>

std::map<std::string, long> phone_book;
phone_book["Bob"] = 123456789;

// at
phone_book.at("Lasya"); // returns ERROR

// insert 
std::pair<std::string, long> pair;
pair.first = "Lasya";
pair.second = 123456789;
phone_book.insert(pair);

// insert returns a pair::second boolean -- true if new mapping inserted, false if key already existed
// do not use these right now!
auto result = phone_book.insert(std::pair<std::string, long>("Lasya", 1234567890);
if (result.second == false) {
    std::cout << "Value already exists" << std:endl;
}
```

### Iterating over map
``` cpp
for (auto const& [key, value] : your_map) {
    std::cout << key << ":" << value << std::endl;
}
```