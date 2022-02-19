# 02/17/22: Streams and Input Validation

## Reading from a Stream
- The operator<< is white space delimited 

### Example 1: string
``` cpp
std::std first_name;
std::string last_name;
std::cout << "Enter your name: ";
std::cin >> first_name >> last_name;
```

If the user enters "michael nowak", **std::cin reads it like this**
| m | i | c | h | a | e | l | | n | o | w | a | k | \n |

The variables are stored as follows:

- **first_name**
| m | i | c | h | a | e | l |

- **last_name**
| n | o | w | a | k |

### Example 2: decimal
``` cpp
int whole_part;
char throw_away;
int fractional_part;
std::cout << "Enter floating-point number: ";
std::cin >> whole_part >> throw_away >> fractional_part;
```

If the user enters 3.14, the variables will be fillied as follows:

- **whole_part**
| 3 |

- **throw_away**
| . |

- **demical_part**
| 1 | 4 |

## Format Read Errors
Use __**stream states**__ to your advantage when reading from ifs file
- __**ifs.good()**__ = true if the previous read succeeded, no errors in stream
- __**ifs.bad()**__ = true if unrecoverable error occured
- __**ifs.fail()**__ = true if either unrecoverable error or formating/recoverable error occured (check in comparison with ifs.bad())

## Recover from a Format Read Error

- __**ifs.clear()**__ = the state of the stream resets to default
    - good() is true
    - bad() is false
    - fail() is false

- __**ifs.ignore(1, '\n')**__ = ignores the character that is mismatched, flow by you and ignore it 
    - first arg = # of chars to ignore
    - second arg = ignore till # or chars or till next whitespace 

- Use the following code to ignore all characters until specific character is observed
``` cpp
#include <limits>

ifs.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
ifs.ignore(std::numeric_limits<std::streamsize>::max(), '\t');
std::cin.ignore(std::numeric_limits<std::streamsize>::max(), ';');
```