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