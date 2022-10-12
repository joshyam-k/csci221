## Linking

Benefits of Linkers
- modularity: program can be written as a collection of smaller files, rather than one monolithic mass, can build libraries of common function
- efficiency: separate compilation so if you change a file you can recompile it and then relink rather than recompiling every single source file, you can also compile files concurrently (in parallel), you save space using linking because you don't need to make a copy of a library for each program that you run, you can just have one copy that your programs reference


What Linkers do
- symbol resolution: programs define a reference symbols (global variables and functions). they are stored in a symbol table in the object file (`.o`). the linker associates each symbol reference with exactly one symbol defintion
- relocation: merge separate code and data sections into single sections, relocates symbols from their relative locations in th `.o` files to their final absolute memory locations in the executable
- updates all references to these symbols to reflect their new positions

Object file types
- relocatable object file `.o`
- executable object file `a.out`
- shared object file `.so`

Executable and Linkable format: standard binary format for object files
- be able to recognize that these sections exist 

Linker Symbols
- global symbols: symbols defined by module m that can be referenced by other modules (non-static C functions and non-static global variables)
- external symbols
- local symbols: symbols defined and referenced exclusivley by module m, (static)

- If a name is a global variable and is not static it will not be in the symbol table
- static functions do show up in the symbol table though
- variables local to a function do not get put in the symbol table (arguments and variables created within a function)
- printf is in the symbol table

Static variables
- local static C variables stored in either .bss or .data so they are non stored on the stack


The linker does not type check so you can run into a lot of nasty problems

Avoid global variables if you can
- otherwise
    - use static if you can
    - initialize if you define a global variable
    - use extern if you reference an external global variable
- ex: use `extern int g;` this is telling us that someone somewhere else is defining g
    - when linking files that use g it will find where g is defined and connect all of its references to that value

Relocation
- relocatable object files merged into an executable object file



