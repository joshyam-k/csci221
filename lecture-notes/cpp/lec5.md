## Smart Pointers and Generics (final lecture!)

The STL containers accept many different types, but how does it do this?

```
vector<int>
vector<point2d>
```

as long as the class is implemented properly, STL containers can accept it

### C++ templates

A template is a function or class that accepts a type as a parameter.
- you define the function or class once in a type-agnostic way
- when you envoke the function or instantiate the class, you specify types or values as arguments to it
- At compile-time the compiler will generate the "specialized" code from your template using the types you provided

to implement you include one of these lines
```
template<typename T>
templete<class T>
```

then in a function or class you write

```
int foo(const T &value1){
    ...
}

// using the function
foo<int>(7);
```

the compiler is also capable of inferring types not specified so you could just do `foo(7)`.


Templates are useful for classes as well
- `template <typename T> class pair { all class code }`
- T is replaced with the template argument when a class is intantiated `pair<std:string> ss`
- importantly only template methods that are actually called in your program are instantiated (but this is an implementation detail)


### Smart Pointers

An object that stores a pointer to a heap-allocated object
- pointers that we've turned into classes so they can do management for us
- looks and behaves like a regular C++ pointer
- can help you manage memory
- with correct use of smart pointers, you no longer have to remember when to `delete` `new`'d memory

- a `unique_ptr` takes ownership of a pointer
    - a template: template parameter is the type that the "owned" pointer references (i.e the T in pointer type T*)
    - `std::unique_ptr<int> x(new int[5])` wrapped and heap allocated
    - if you have many potential exits out of a function its easy to forget to call delete on all of them, and unique_ptr will delete its pointer when it falls out of scope so it makes everything safe for us
    - `unique_ptr` has disabled its copy constructor and assignment operator since if you copy it you no longer have uniqueness
    - to transfer owneship you use `reset` and `release`
        - release returns the pointer, sets wrapped pointer to `nullptr`
        - reset deletes the current ponter and stores a new one
        - `y(x.release())` x abdicates ownership to y
        - `z.reset(y.release)` is essentially doing `z = y` 

`unique_ptr`'s can be stored in STL containers
- seems wrong because copies cannot be made of these
- move semantics rescue us here as, when implemented STL containers will move rather than copy
- `z = std::move(y)` y abdicates ownership to z








