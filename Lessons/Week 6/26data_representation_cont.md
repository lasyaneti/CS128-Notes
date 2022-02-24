# 02/22/22: Data representation cont.

- Store negative numbers as their additive inverse of their positive counterpart
- If you are adding a positve integer (like 3) to a negative one (like -3), note that the summation doesn't have to add up to 4 bits of 0, you just have to have the last 4 bits as 0 - the rest can be manipulated to make addition easier.

**Ex: adding 3 + (- 3)**

  0 0 1 1
\+ 1 1 0 1
..........
1 0 0 0 0 

- The 1 at the front get's thrown away because it has no value (also remember in binary 1 + 1 = 0 with a 1 carry forward)
- Use two's complement for negative integer numbers 
  - Flip all digits and add 1 
- Largest number in 4-bit: 2^(4-1) - 1 = 7 = binary 0111
- Smallest number in 4-bit: -2^(4-1) = -8 = binary 1000

## HW: 8-BIT CONVERSION DECIMAL TO BINARY (all integers)
``` cpp
#include "converter.hpp"

std::string Base10toBase2(int base10_value) {
  if (base10_value > 127 || base10_value < -128) {
    throw std::invalid_argument("Input out of bounds");
  }
  // POSITIVE
  if (base10_value > 0) {
    std::string binary;
    int binaryNum[32];
    int i = 0;
    while (base10_value > 0) {
      binaryNum[i] = base10_value % 2;
      base10_value = base10_value / 2;
      i++;
    }
    for (int j = i - 1; j >= 0; j--) {
      binary += std::to_string((binaryNum[j]));
    }
    std::string eightbit_binary;
    for (int i = 0; i < 8 - binary.length(); i++) {
      eightbit_binary += "0";
    }
    eightbit_binary += binary;
      return "0b" + eightbit_binary;
    }
    
    // NEGATIVE
    if (base10_value < 0) {
      base10_value *= -1;
      std::string binary;
      int binaryNum[32];
      int i = 0;
      while (base10_value > 0) {
        binaryNum[i] = base10_value % 2;
        base10_value = base10_value / 2;
        i++;
      }
      for (int j = i - 1; j >= 0; j--) {
        binary += std::to_string((binaryNum[j]));
      }
      std::string eightbit_binary;
      for (int i = 0; i < 8 - binary.length(); i++) {
        eightbit_binary += "0";
      }
      eightbit_binary += binary;

      // find two's complement 
      // PART 1: flip digits
      for (int i = 0; i < eightbit_binary.length(); i++) {
        if (eightbit_binary.substr(i, 1) == "0") {
          eightbit_binary.replace(i, 1, "1");
        } else if (eightbit_binary.substr(i, 1) == "1") {
            eightbit_binary.replace(i, 1, "0");
        }
      }

      // PART 2: add 1
      for (int i = eightbit_binary.length() - 1; i >= 0; i--) {
        std::string current = eightbit_binary.substr(i, 1);
        if (current == "0") {
          eightbit_binary.replace(i, 1, "1");
          return "0b"  + eightbit_binary;
        }
        eightbit_binary.replace(i, 1, "0");
      }
     }
  
  // ZERO
  return "0b00000000";
}

```