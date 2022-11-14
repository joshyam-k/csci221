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
    - C++ supports C strings (arrays of characters with NUL character)
    - C++ also has a designated string type (requires `#include <string>`)
        - acts like an array of characters
        - `string name = "josh yam"`
        - can also access using methods `name[3];` \\ h
    - how do we know which type of string we have?
        - any literal string like "hi there" is a C string
        - to convert between the two types: `string("text")` (C string to C++ string)
    - concatenate using `+` or `+=`
    - `string s1 = "Ty";` `sl += "ler"; \\ "Tyler"`
    - strings are mutable and can be changed `s1[4] = '@` \\  Tyle@
    - If you get bugs they are likely due to type errors (trying to do things on C strings that can only be done on the C++ string type)
    - strings are classes that have methods
        - `string_name.method_name(arguments)`


### Pointers in C++

- store the address of other variables
- NULL is the default value for pointers in C (so we can check if a pointer is NULL)
- in C++ we have `nullptr` which is the default value for pointers in C++
    - means that the pointer does not point to a value
    - if you dereference `nullptr` it throws an expection
    - all that has changed here is the name lol
- allocating data to the heap
    - C++ keword for allocating data: `new` 
    - this takes as input the type of data desired
    - the function returns the address of the start of the allocated block
    - `int* an_int = new int;`  // allocate one element
    - `int* an_array = new int[length_of_array];` // allocate array
    - memory is initialzed to the default value of the type you're trying to create
- deallocating data on the heap
    - now in C++ we use the delete keyword 
    - `int* y = new int;`
    - `delete y;`
    - removes the data block pointed to by y from the program
    - for arrays use `delete []`

### Pass by value vs pass by reference

C++ is a language which can do pass by reference using pointers, but you can also do it with reference semantics
- uses `&` in function declaration (not in call)

this is telling our function that our arguments are ints, but are being passed as if they are pointers
```
void swap(int& a, int& b){
    int temp = a;
    a = b;
    b = temp;
}
```

you can act like you passed values in terms of your syntax, while allowing the behavior to act as though you passed pointers.

### Default arguments

- supplying a default value makes an argument optional
- all arguments with default values must appear last in the list

### Console Input and Output

Done through streams
- a stream can be thought of as a flow of objects
- input involves taking objects from the stream
- output involves adding objects to the stream
- makes use of `<<` and `>>` operators
- also used for file input/output

Console Output
- done using the `cout` stream
- `cout << expression << expression ...`
- `cout << "You are " << age << " years old"` (does not require strings as input)
- ending lines done using `endl` (same as `\n` but more compatible with all operating systems)
- `cerr` for error mesages

Console Input
- `cin` stream
- `cin >> string_variable;`
- performs type conversion (consumes and discards leading whitespace, for numeric data it stops at first character that does not match type)










