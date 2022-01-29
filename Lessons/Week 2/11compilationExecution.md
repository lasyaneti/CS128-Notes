# 01/28/21: Compilation and Execution

## Compilation Pipeline (broken down further below)
1. HelloWorld.cpp and header files (.h)
2. **Preprocessor** (translation unit) -> temp file -> fed to compiler
3. Compiler takes source code -> generates **assembly file** (.s)
4. Assembler takes assembly files -> generates **object code** (.o)
5. HelloWorld.o and library object code -> goes through **linker** 
6. Linker -> **executable** HelloWorld

## Preprocessor
- "#ifndef XXX_H" checks if that header file is defined already, if yes the body doesn't run
- if not, "#define XXX_H" is right below it and triggers the declaration
- "endif" ends the header file declaration

## Compiler
- Looks at variables to make sure everything is declared correctly 
- Type checking
- **Assembly code** (.s) is the generated output

## Assembler
- Converts assembly code into **object code** (.o), i.e the generated output
- Object code is binary code

## Linker
- All object code is aggregated at the end once each source file is processed = and fed to the linker 
- Every object code file must be mentioned specifically to be collected 
- **Executable** is the generated output -> use this to run main and get your output 