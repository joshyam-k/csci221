## Compiling C

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



