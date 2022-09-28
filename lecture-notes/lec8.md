## Arrays
- multiple copies of a data type
- laid out contiguously
- declared with size in brackets `int ages[10];`
    - need to track size manually
- size of frame on the stack is based on the variables in a function and the compiler needs to know how large the stack frames are at compile time
- so at compile time you need to know how large your array is (so it cannot depend on the data)

But indirection and memory allocation allows us to create variable size arrays!
- `int* a = malloc(sizeof(int));` creates a block of data somewhere that is the size of an integer
- `int[] b = malloc(5 * sizeof(int));`
- pointers and arrays use malloc in the same manner!
- In C, **arrays and pointers are the same thing!**
    - variables of array type can receive pointer type values and vice versa
    - neither track size
    - but both can use array notation
    - and both can use pointer arithmetic

### Pointer Arithmetic
Pointers and arrays are both the address of the first data element in the block
- `*a` is the same thing as `a[0]`
- indexing computes the address of the ith element and dereferences it
- `a[1]` refers to the element one _type_ over from `a`
- `&a[1]` is the same as adding `sizeof(_type_)` to `a`
- pointer arithmetic allows you to do math with pointers
    - unit of change is the sizeof the type pointed to
    - `a + 1 == &a[1]`
    - `a[i]` is just syntax for `*(a + i)` 

Write a function that creates a copy of an array
- you can just copy the pointer
- allocation is needed
- don't change the pointer after allocation
- loop through the data

```
int* array_copy(int* arr, int size){
    /*need to allocate memory for a new array in the heap */
    /*otherwise our copy would get washed away once the function completed */
    /* so we create a pointer to allocated memory in the heap */
    int* copy = malloc(size * sizeof(int));
    /* now we need to copy the indiviual values into our new array */
    for (int i = 0; i < size; i++){
        copy[i] = arr[i];
    }
    return copy;
}
```
freeing the copied array's memory in the heap is the responsibility of the caller here

### Out of Bound access
`int* arr = malloc(5 * sizeof(int));`
- if you access `a[5]` you get undefined behavior
- results can change across runs

### Undefined Behavior
- security vulnerability
- software bugs
- so why does C have undefined behaviors? (because C was written when we were bad at writing programming languages)

### Type-Casting Pointers
- you can cast pointers to other types `char* c = (char*) b`
- `c[4]` is now the first byte of `b[1]`
- when type casting, we must be mindful of alignment
- in practice only cast pointers to void or char types

### Void Pointers
- `void*` is the type of an array of voids
- this is not a type in C
- more accurately `void*` is the address of the first element of an array
    - dont know element type (and size)
    - dont know number of elements
- we use `void*` to write generic operations on arbitrarily typed arrays
    - requires knowledge of element type and quantity

### Strings
- there is no type string in C
- strings are just arrays of charactesr use type `char*` or `char[]`
- the syntax "hello" is just an array containing each of the individual characters
- `char* s1 = "hello;"` then `printf("%s\n", s1)` but printf doesnt know the size of the array so how does it know the size of the string??
    - the end of a string is indicated by the NUL (not NULL) character (written '\0') 
- thus, s1 is an array of six characters and `s1[5] == '\0'`

The `<string>` library
- contains lots of useful functions for working with strings
- `strlen` returns the number of characters in a string
- `srcpy` copies all the characters of a string to a new destination
- there are many more utility functions

In memory
- strings can live in three places
    - in the DATA segment
        - syntax `char *s1 = "hello";` these strings are read-only and these strings should not be freed
    - in the heap
        - using malloc and free. Important to allocate enough space for the NUL character
    - on the stack
        - should not free, just use generic array notation















