# 01/31/22: Build Systems (make)

## Make
- "Makefile", case-sensitive 
- Building rool that describes how to get an output 
- Make files need to be intended with tabs 
- **See below**: output, input, recipe + steps 
- Blackslashes (\\) break it into different lines

```  Makefile
bin/main.out: src/main.cc
    slang++ -stc++2- -stdlib=libc++ ... etc ...
```

## Make - variables
- set with "=" 
- evaluated with "$(_)"
- ex: clang++ is stored in CXX, so you don't have to enter it everytime 

``` Makefile
CXX = clang++ 

bin/make.out: src/main.cc
    $(CXX) 
```

## Make - evaluating multiple rules 
Can update variables as it goes depending on which files have changes made to them 

## "phony" targets
- These run independently of the file system status 
    - exec: run the compiled program with specific arguments
    - test: build and run unit tests
    - clean: remove any generated or cached files

## Automatic variables
- $@: name of the rule's output
- $<: the first dependency
- $>: all dependencies
- $: the directory of the output