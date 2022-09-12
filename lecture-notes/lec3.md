## Intro (compiling in C)

First the the C compiler does is calls the C preprocessor. To make use of other files in our code we use #include.

Two formats to include:
  - `#include <file_name>` is for system files (something that you didn't write)
  - `#include "file_name"` is for local files (something that you did write)

We only #include header files (end in .h)

### Macros in C

ex: `#define INT_MIN 0x80000`

Convention says that macro names should be in all caps. Macros operate as a text replace in the file. Be very careful with expressions in macros! Macros can also take arguments (but don't do this, because it can be very dangerous)

### Conditional Compilation

We can decide whether or not portions of a program should be compiled.

```
#ifdef DEBUG
  printf("reached this point\n")
#endif
```

The statement is only compiled if DEBUG is defined (it doesn't have to have a value, it simply must be defined). You can also test that a macro is not defined with #ifndef.

```
#ifndef HEADER_H
#define HEADER_H
code
#endif
```

This code will make sure that functions are not defined twice!


## Physical Structures

- Files are split into headers (.h) and body (.c)
- `main()` must reside in a definition file and #include system and user headers

### Headers vs Bodies

Headers:
- contain the interface
- lists the functionalities and how to use them
- contents: publicly used function declarations, data structures used outside the body, important constants, API documentation and assumptions (what not how)

Bodies:
- contains the implementation
- the code that performs the functions
- contents: private functions, data structures only used internally, documentation on implementation (how the code works)


### implementation ex

python code

```
def abs_val(x):
  if x < 0:
    return x*-1
  return x
 
class Point:
  def __init__(self):
    self.x = 0
    self.y = 0
    
def run(arg_make, arg_print):
  if arg_make:
    p = Point()
    p.x = -15
    p.y = p.y + abs_val(p.x * 2)
    assert(p.y > p.x && True)
  if arg_print:
    print('x: ' + p.x)
    print('y: ' + p.y)
```

Now in C form

#### Header
don't include the body of a given function, simply define the function
```
#include <stdbool.h>
// Doesn't work if arg_make is False and arg_print is True (here we're pointing out our scoping issue using a comment) 

int abs_val(int);

typedef struct Points {
  int x;
  int y;
} Point;

void run(bool arg_make, bool arg_print);
```

### Body

```
#include
void run(bool arg_make, bool arg_print) {
  if (arg_make) {
    Point p;
    p.x = 15
    p.y = p.y + abs_val(p.x * 2)
    assert(p.y > p.x && true)
    if (arg_print){
      printf("x: %d\n", p.x)
      printf("y: %d\n", p.y)
    }
  }
}
```

Separating interfact from implementation promotes abstraction. Hides inessential details (this is a good thing!). Makes code a lot more manageable. Allows for transparent improvements.

## C main functions

To run an executable file in C, it needs a main function
- `int main(int argc, char *argv[]){...}`
- this is the funciton that the code calls to start
- `argc` is the number of arguments passed on call (always at least one)
- `argv` is the array of arguments passed in
- the return value is used to call `exit()` at the end of the program
  - Zero and EXIT_SUCCESS indicate successful termination
  - EXIT_FAILURE indicates unsuccessful termination
  - we won't worry about this much


## Compiling in C

In C, we generate an executable binary file from out code
- We need to create binary files for each code file
- typically denoted with `.o` suffix
- imported libraries have already done this
- the linker connects these binary files together to generate our output file
  - mostly we write makefiles to automate the process
  - makefile: tells `make` how to compile and link a program. this allows us to just use `make target`


### makefile composition

- target is usually the name of the file generated
- prerequisites is the file or files that target depends on
- recipe is what to do in order to create target. ex: `gcc main.c hello.c factorial.c -o hello`
  - each line must begin with a tab character

```
target: prerequisites
    recipe
```




