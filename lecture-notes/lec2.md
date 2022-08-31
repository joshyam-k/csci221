## Introduction to C (con't)

In Python you can make a class, but there is no object oriented programming in C.

### Arrays
  - multiple copies of a data type
  - laid out in contiguous memory
  - declared with size in brackets `int ages[10];` 10 says how many copies you want to have. Only declare with constants!
  - access with index `ages[0] = 28;`
 
### enum
  - works like set of named constants `enum semester{Fall, Spring};`
  - values can be specified `enum year{Freshman = 1, Senior = 4, first = 1};` you can specify the same value for multiple named constants
  - treat like a normal variable `enum semester s = Fall;`
  - remember to use "enum" plus type name
  - can compare like an int `int i = 0; while (i < Senior) { ...`

### struct (most commonly used outside of arrays)
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

### union 
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


### typedef
  - so far we've had to use "data_type typename" every time we want to use one of these structures
  - typedefs allow us to avoid this
 
```
typedef struct trees {
  int height;
  int age;
 } tree;
```
  - can just use type name of typedef;d type `tree t;`
  
  
## Control Structures in C

### if statements
  - standard functionality (controlled with {}) 
  - 
```
if (condition) { 
  operation; 
  } 
  else { 
    operation; 
  }   
```
  - else if must be constructed (no elif equivalent)

### while loops
```
while (condition) {
  operation;
}
```
  - also supports do while loop

```
do {
  operation;
} while (condition);
```
  - ensures the operation is run at least once


### for loops
```
for (state1; condition; state2) {
  operation;
}
```
  - runs statement 1 at the beginning
  - checks the condition before starting an interation
  - runs statement 2 at the end of the iteration
  - so in reality it does this
```
state1;
while (condition) {
  operation;
  state2;
}
```


### switch-case structures
  - designed to allow for choice of multiple options

```
switch (expression) {
  case val1:
    operation1;
  case val2:
    operation2;
  default:
    operation3;
 }
```
  - tries to match expression against vals in order
  - when a match is found, begin operations
  - completes all following operations (matching val2 results in operation2 and operation3)

### break
  - leaves the current control structure
  - no more loop operations
 
### continue
  - leaves the current control structure
  - may be additional loop iterations
```
while (condition1) {
  if (condition2) {
    continue;
  }
}
```
  - in this case continue will leave the innermost control loop structure
  - it will leave the if and go back and check condition1
  - again, it affects the inner most loop! 


Back to switch cases for a moment
  - write something like this to run an if else type control flow using break;

```
switch (expression) {
  case val1:
    operation1;
    break;
  case val2:
    operation2;
    break;
  default:
    operation2;
}
```
this time once a condition is met it will only run the single operation associated with that condition


### Variable Scope
- variables defined outside of functions are called global variables (try not to use them unless you have a really good reason for them)
- it's better practice to define variables at the start of a function or loop in which they will be used


## Compiling C

You've written some code- what's next?

### The C Preprocessor Language

C code + Makefile -> (preprocessor) Compiler -> Executable 

- typical C program consists of statements in two languages
  - the C prepreocessor language (all directives start with #)
  - the C proper
- First thing the C compiler does is call the C preprocessor
  - a program that processes all the C preprocessor directives

### File inclusion

- `# include *filename*`
  - `<filename>` if file lives in a standard library 
  - `"filename"` for your files (will look in the directory that you're in)

### macros: macro defitions, macro functions

`# define MACRO_NAME value`

ex: `# define pi 3.14121592`

importantly you do not need a value! also it literally is a replace all in terms of functionality
  - you might not add a value if you want to be able to check if the object exists (see below)

### conditional compilation

check if macros are or are not defined

`# ifdef MACRO_NAME`
`# ifndef MACRO_NAME`

so you can do

`# ifndef INT_FUNCS.H`
`# define INT_FUNC.H`
... code ...
`# endif`











































