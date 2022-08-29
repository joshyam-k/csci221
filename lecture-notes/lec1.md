## History of C

- Originally developed to reimplement the Unix OS
- Became one of the most popular languages (very fast, very powerful)

## Why we like C

- General-purpose
- maps efficiently to machine instructions
- small set of keywords
- low-level access to computer memory with byte-addressable pointers
- thus it's very popular for low level code (operating systems, drives, databases)

## What makes C different

- imperative (you tell a computer to do a thing and it does the thing, no object-oriented stuff)
- static type system with implicit conversion 
- variable scoping (if you declare variables inside a function and then try to use them outside of the function it will not work)
- memory mangement 
- preprocessor language 
- compiled, not interpreted (you sit down and write an entire C file and then you run a program on them that turns those software files into executable files and then you run the executable file with inputs)


## Translating code (From Python)

### Python
```
def abs_val(x): 
  if x < 0:
    return x * -1
   return x
``` 
### C
```
int abs_val(int x) {
  return x < 0 ? -x : x;
}
```
differences:
- scope style: {} (spaces do not matter for syntax)
- lines end with ;
- functions do not end with ;
- Types! (int)
- Operators

## Data Types in C

- every variable has a type (chosen at variable declaration, does not change)
- every function has a type

options:
- int (long or short, signed or unsigned)
- float
- double
- char
- void (the typeless type)
- no strings

## Type conversions in C

variables can be converted between types

```
double mins_to_hours(int mins) {
  return (double) mins / 60.0;
}
```
These conversions can happen implicitly
- variables are "promoted" to larger types

**Do not let the compiler do implicit type conversions**

ex:
```
double division(int x, int y){
  return x / y;
}
```
`division(5, 2)` will give us 2.0
- implicit conversion will happen in the return instead of in the calculation
- minimize conversions and make them explicit
- turn on compiler warnings to be notified 

## Operators in C

- Boolean Operators:
  - And: `x && y`
  - Or: `x || y`
  - Not: !x
  - Lazy evaluation (if trying x && y, if x is false then it will not even test y)

- Arithmetic operations:
  - addition, subtraction, multiplication, division, modulus (x % y)
  - but must be careful of types

- comparisons:
  - equality `x == y`
  - inequality `x != y`
  - less than, greater than
  - good practice to put constants first in comparison

- bitwise operators:
  - And: `x & y`
  - Or: `x | y`
  - Xor: `x ^ y`
  - right shift by y: `x >> y` (likewise leftshift by y)
  - dont confuse these with boolean operators

- shortcuts:
  - increment by one: `x++` 
  - increment by y: `x += y`
  - decrement by one: `x-`
  - divide by y and assign: `x /= y`

- other operators:
  - variable size: `sizeof(x)`
  - indirection
  - conditional expression: `x ? y : z` (evaluates to y if x is true, otherwise evaluate to z, essentially ifelse)













