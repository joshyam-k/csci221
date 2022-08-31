## Introduction to C (con't)

In Python you can make a class, but there is no object oriented programming in C.

Arrays
  - multiple copies of a data type
  - laid out in contiguous memory
  - declared with size in brackets `int ages[10];` 10 says how many copies you want to have. Only declare with constants!
  - access with index `ages[0] = 28;`
 
enum
  - works like set of named constants `enum semester{Fall, Spring};`
  - values can be specified `enum year{Freshman = 1, Senior = 4, first = 1};` you can specify the same value for multiple named constants
  - treat like a normal variable `enum semester s = Fall;`
  - remember to use "enum" plus type name
  - can compare like an int `int i = 0; while (i < Senior) { ...`

struct (most commonly used outside of arrays)
  - how people did classes before there were classes
  - creates a structure consisting of multiple variables
 
 ```
 struct point2d {
  int x;
  int y;
 };
 ```
 
  - treat like a normal variable `struct point2d p;`
  - remember to use "struct" plus type name
  - access sub-variables with "." `p.x = 15; int new_var = p.x;`

union 
  - one variable that can take multiple types
  - choosees between other existing data types

```
union number {
  int i;
  float f;
};
```

  - treat like a normal variable `union number n`
  - access type with "."
  - `n.i = 15`, `n.f = 3.14`, `int new_var = p.x` (last one will result in some weird conversion of 3.14 to an int) (we dont use unions much)


















