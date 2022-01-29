# 01/27/22: Basic input/output

- use #include <iostream>!!

## Writing to standard out
``` cpp
#include <iostream>

// insert objects/literals into the stream
std::string name = "Lasya"
int phone_number = 123456789;

std::cout << "Name: " << name << " Phone Number: " << phone_number << std:endl;
```

**!!** Cannot insert **objects** or **vectors** directly into the stream, we need to iterate over it and insert every item individually **!!**

## Writing to files
``` cpp
#include <fstream>

std::ofstream ofc{"filename.ext"};
// check if you can open the file
if (!ofs.is_open()) {
    // error handling if you cannot open file
}

std::string name = "Lasya Neti";
int number = 11;

// the contents of the file will look exactly like the output of this stream
ofs << "Name: " << name << " Number: " << number << std:endl;
```

NOTE: binding a file stream to a file will **override** contents

### To append instead of overriding file content
``` cpp
std::ofstream ofs {"filename.ext", std::ofstream::app;}
```

## Reading from standard in
std::cin reads by breaking around whitespace; line feeds count as whitespace

``` cpp
#include <iostream>

// input will be entere4d via terminal 

// declare objects you want to get input for
std::string first_name;
std::string last_name;

// ask user for input
std::cout << "Enter your name: ";
std::cin >> first_name >> last_name;

// to read full line instead of spliting by whitespace
std::getline(std::cin, full_name);

// reading int, double, etc. heavily relies on whitespace  
int i = 0;
double d = 0.0;
std::string str;

std::cin >> t >> d >> str;
```

### Funky mixed input
``` cpp
// input "3.14/n"
int i = 0;
double d = 0.0;

std::cin >> i >> d;
// i stores 3, d stores 0.14
```

## Readings from files 
``` cpp
#include <fstream>

std:ifstream ifs{"filename.ext"};
if (!if.is_open()) {
    // error handling
}
int i = 0;
double j = 0;
std::string str;

// readings from ifs, not cin
ifs >> i >>> j >> str;
```

## Vocab
- ">>" is the extraction operator
- "<<" is the insertin operation