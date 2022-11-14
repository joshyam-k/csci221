## Introduction to C++

Similarities to C
- static type system with implicit conversion
- memory management
- preprocessor language
- compiled, not interpreted

C++ adds
- support for object oriented programming
- additional data types and keywords
- exception handling
- more library support

C++ is a superset of C, meaning that it can run C code!

### Compiling C++

- Make sure your compiler knows C++ (gcc vs g++)
- same preprocessor directives
- same implementation and interface split (headers vs bodies)
- same main function
- same makefile ideas
- source files are saved as `*.cpp` files (make suer to use an appropriate compiler)


### Namespaces

What happens if you want to use the same name more than once?
- in C you're out of luck
- in C++ you put it in a different namespace

Namespaces, much like classes, contain symbols
- functions
- types (classes, typedefs)
- variables (objects, constants)
- templates
- namespaces

### Using Namespaces

specified using `::`
- `std::cout << "string";` // use the std namespace cout
- the global namespace is used if none is specified
    - can be specified using `::cout`
- you can also pre-specify with the command `using`
    - specify a default namespace
        - `using namespace std;` 
        - don't do this in header files
    - specify a specific symbol
        - `using std::cout` 
    - you can have multiple `using` declarations


### Importing and Namespaces

There are often different ways to import the same functionality
- the difference is often which namespace the functionality is added to
    - `<string.h>` puts functions into the global namespace
    - `<cstring>` puts functions into the std namespace
    - `<string>` puts the C++ string class into the std namespace
    - in general don't make multiple copies of the same function

### Adding to a namespace

By default your code adds to the global namespace

If you want to add to a namespace you can do so like this

```
namespace Physics {
    constexpr G = 9.8;
}
```

This should go in the header file (you can also make nested namespaces)

### Operators in C++

- arithmetic operators
- boolean operators
- comparison operators
- bitwise operators
- ternary operator
- additional operators can be defined
    - based on objects


### Dataypes in C++

all old C ones

new ones
- bools
    - represent a boolean value (either true or false)
    - logical operators and comparisons (!, &&, etc) return bools
    - logical operators take bools as input
    - does this mean we have to change our conditions? (no, type-casting helps us)
- strings
    - 


### Pointers in C++

- store the address of other variables
- NULL is the default value for pointers in C (so we can check if a pointer is NULL)
- in C++ we have `nullptr` which is the default value for pointers in C++
    - means that the pointer does not point to a value
    - if you dereference `nullptr` it throws an expection
    - all that has changed here is the name lol
- allocating data
    - 












