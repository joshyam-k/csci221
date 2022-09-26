## Indirection and Arrays

Let's say we want a function that returns multiple values. How can we do this?
- one option is to use a struct (but it's excessive to do this everytime)
- modify a shared value

Sharing data
- functions communicate through arguments and return values
- these values are copied for use by the other function (this makes it really hard to share data)
- we would like to have different functions use the same object

How do we share objects between functions when all values passed are copied?
- we make use of indirection
- passed values *point* to real data

### Pointers

Store the address of other variables. Can connect multiple variables to one object which gives us the behavior that we're looking for. Pointers can change to point to different objects.

Declaration:
```
int obj1 = 7;
float obj2 = 0.5;
int* point1 = &obj1;
float* point2 = &obj2;
```

`t*` is the type of a pointer to an object of type t. `&` operator returns the address of the object

Dereferencing: getting the value that is stored in the memory address pointed to by the pointer
```
int obj3 = *point1;
*point1 = 8;
```
`*operator` returns the value of the pointer.
- the line `*point1 = 8` will change obj1 but not obj3 because the operation happens after obj3 is set to the pointer.

### Capturing Memory Addresses
- `&` can ge the address of anything that has a memory address
- functions, local variables, fields of structs, array elements
- in general, for any exp for which `exp = ...` is syntactically valid, we can write `&exp`
- you also cannot get the address of non-pointer variables

### Aliasing
- multiple variables referencing the same object
- caused by pointers
- data can change without the variable ever being modified

```
int obj1 = 7;
int* point1 = &obj1;
*point1 = 8;
int a = obj1 + 2;
```
`a` results in 10. So we have changed the data in obj1 without every modifying it directly

Now back to returning multiple values!
- use pointers as arguments in a function
- thus our function can return one of the values that we want while modifying another object via pointers that the user can access after the function has run

### Pass by Value vs Pass by Reference

Pass by Value
- arguments are values
- deep copies (completely different)
- change limited to local function

Pass by Reference
- arguments are pointers to values
- shallow copies (aliasing of one object)
- change by one function seen by all
- done with pointers in C

### More about pointers
- a pointer is just a type (so you can have a pointer to any type as well as a pointer to a pointer)
    - `int** point1;`
- what if a pointer does not point to an object? a pointer is just an address and many addresses are out of range for your program.
    - these are invalid
    - never set pointers to values (except for NULL)
    - NULL is the designated value for pointers that do not point to objects

NULL is the default value for pointers. Means that the pointer does not point to a value.
- dereferncing NULL throws a null pointer exception
- so everytime you dereference a pointer you need to know that that pointer is not null.

Pointers and Structs
- just like other types, we can create pointers to structs


### Memory Model
Variables live in local memory
- the variables of a function are grouped in a frame
- each function currently being called has its own frame (when main calls a function then we create a frame for that function)
- each function can only manipulate the variables in its frame 
    - each function only "knows about" the variables in its frame
    - as functions are called, their frames are added to the stack
    - as functions finish, their frames are removed from the stack
    - different frames can have variables with the same name (once again because functions can only manipulate variables in their frame)
    - size of frame is based on variables in function

Stacks
- a data structure with three operations
    - push adds to the top of the stack
    - pop removes the top of the stack
    - top lets you look at the top of the stack
- so stacks are "last in, first out"
- frames of memory are a stack

Returning stack vars
```
int* bad() {
    int a = 1;
    return &a;
}
```
this is bad (if you couldnt tell). We're returning the address of a variable on the stack, but then the stack frame that holds that variable is being deallocated and so we no longer have access to that variable. This is a huge security vulnerability. Do not return pointers to local variables. So how should we return pointers?

### Allocating Data
How can we create data that survives function completion?
- it cannot go on the stack

Long living data needs to go on the **heap**
- a portion of memory dynamically managed at runtime
- data needs to be allocated
- size needs to be tracked (thats because the size is not written anywhere thats accessible by your code)

C function for allocating data: `malloc` 
- takes as input the size of data desired (use sizeof() operator to determine this)
- the function returns the address of the start of the allocated block (or NULL if you are out of memory)
- you should probably NULL-check everything that comes out of `malloc`
- `int* a = malloc(sizeof(int));` if you then print the value pointed to by a you get undefined behavior since memory is not initialized (you just get whatever was there)

C function for allocating initalized data: `calloc`
- this takes an input how many desired data blocks and their size (again use sizeof() for latter arg)
- the function returns the address of the start of the allocated block
- `int* a = calloc(1, sizeof(int));` 
- memory is initialized (all blocks are set to zero). this is usually safer

### Deallocating Data
variable creation occurs in two ways
- functions add to stack
- allocation adds to heap

variables on the stack are removed with frame
- when are variables on heap removed? When you *manually* deallocate them
- using the function `free();`
- `free(y);` removes the data block pointed to by y from your program
- any data not freed is still treated as in-use by system (known as a memory leak)
















