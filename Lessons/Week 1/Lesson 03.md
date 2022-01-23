# 01/20/22: Type Conversions

## Narrowing Conversion
- Value is converted to type that cannot store to the original precision
- Not safe because value can be changed in conversion process
- Ex: double to float, because double is "larger" than float 

## Widening Conversion
- Value is converted to type that can store values of more precision than the orignal 
- Ex: int to double

## Implicit Type Conversion
- Automatic conversion of values from one type to another = coercion 
- Narrow type to wide type 
- For example, mixed-type expressions: 3.1 + 5 = 3.1 + 5.0 = 8.1 (result is double)

## Explicit Type Conversion
- C++ requires casting to perform this type of conversion 
``` cpp
// static_cast<type_to_cast_to>(value_to_cast)

static_cast<double>(5);
static_cast<int>('a');
```

## Safe vs. Unsafe Type Conversions 
| Safe | Unsafe |
| ---- | ------ |
| bool to char | char to bool |
| bool to int | int to bool |
| bool to double | double to bool |
| char to int | int to char |
| char to double | double to char |
| int to double | double to int |