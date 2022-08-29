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
def abs_val(x): 
  if x < 0:
    return x * -1
   return x
   
### C
int abs_val(int x) {
  return x < 0 ? -x : x;
}



