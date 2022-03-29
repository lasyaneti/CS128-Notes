# 02/28/2022: Functions and the stack

## Anatomy of program in memory
When we launch our program, it is partitioned into sections that are assigned "chunks" of memory. 
- **Code/static** = program code, global and static vars
- **Free store (heap)** = dynamically allocated objects
- __***EMPTY SPACE EXISTS HERE FOR STACK/HEAP TO GROW/SHRINK INTO IT***__
- **Stack** = automatic variables = automatic vars
Stack overflow is when these two opposing memory compartments collide, meaning that the stack is too full.

## The Stack
- **Activation record** pushed when function called and popped when function returns
- Activation record (stack frame) is responsible for
    - Housekeeping information
    - Arguments passed by value to the function
    - Local variables defined in the function
- Ex: with recursive function calls 
![Stack Function Calls](/Images/StackFunctionCall.png)
- Space required for function's activation record is known at compile time, so when the function is called that memory is automatically "**allocated**" on the stack, when the function is finished executing, that memory is "**deallocated**".

## Where the function finds the activation record
- Stack pointer moves in one direction as space is allocated for each function call 
- Stack pointer moves in the other direction as space is deallocated for each function return
- Each activation record similar to heterogenous array
- **In C++, the first activation record is main() call, deallocates when int is returned!!**

## Additional considerations
- Stack can grow either up or down depending on where the address is placed in memory. Convention is to have it go downwards (i.e. stack starts at the upper limit and "grows down" towards 0). 
- Hows parameters and variables are laid out within the activation record is unspecified and unpredictable, depends on compiler