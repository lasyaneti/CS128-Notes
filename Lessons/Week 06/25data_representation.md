# 02/21/22: Data representation

## Positional number system
- Any positive integer b > 1 can be chosen as base 
    - decimal (b = 10)
    - binary (b = 2)
- The value that a digit contributes is based on it's position
    - Decimal Ex: 124 = 1(10^2) + 2(10^1) + 4(10^0) = 1(100) + 2(10) + 4(1)

## Binary to Decimal
1. Double the leftmost digit
2. Add the result to the next digit on the right
3. Double that sum
4. Add the result to the next digit
5. Repeat until the last integral digit is added, final sum is equivalent

## Decimal to Binary
1. Subtract the largest possible power of base-2 from N1
2. Subtract the largest possible power of base 2 from the result
3. Continue this process until a difference of zero is obtained
4. Place a bit value of 1 in place values of those powers subtracted and a bit value of 0 elsewhere

## Binary Addition Facts
- 0 + 0 = 0
- 1 + 0 = 1
- 0 + 1 = 1
- 1 + 1 = 0 (carry forward 1)
- 1 + 1 + 1 = 1 (carry forward 1)
