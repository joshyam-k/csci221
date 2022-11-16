## Object-Oriented Programming in C++

C++ adds *objects* which is one of the main differences from C

Review of structs

```
struct point2d {
    int x;
    int y;
};

struct point2d p // initialization
p.x = 15;        // access
int new_var = p.x 
```

### Classes

Structs are types that contain:
- variables

Classes are types that contain:
- variables
- methods

Just like structs, you can create instances of classes (objects)
- each instance contains separate instances of the variables
- each instance can have the methods called upon it

Methods
- functions associated with a class
- you can call a function on a given instance of that class
- the object is the implicit argument to the method
- the method has access to the variables and methods inside of the class


### How to make a class in C++

two steps
- define the interface, typically create a header file describing what operations the class can perform and what internal state it needs
- define the implementation, a source file that contains the implementation of the class methods

```
class point2d {
public: 
    // methods for the class
    double displacement();
    void translate(int x, int y);
private:
    double x;
    double y;
protected:
}
```

members are grouped by accessibility 
- known as encapsulation

Encapsulation:
- different members of a class can have different levels of accessibility
- 3 levels:
    - private: accessible only to the class itself
    - public: accessible to all the code
    - protected: accessible to the class and any subclasses (see inheritance)

No inherit relationship between accesibility levels
- aka one member's status does not affect other members

encapsulation allows us to separate interface and implementation
- interface is used by external code
- implementation only affects internal code
- so what should be private?
    - functions that are used internally should be private (like helper functions)
    - most variables

Getters and Setters
- if variables are private how should external code be able to modify them?
- getter and setter functions
    - getter functions return the value of a variable
    - setter functions change the value of the variable

Class declaration
```
class point2d {
public:
    double displacement();
    void translate(int dx, int dy);
    int getX();
    int getY();
    void setX(int newX);
    void setY(int newY);
private:
    double x;
    double y;
protected:
}
```

Class declaration: source files
- make sure to include the declaration
- each method of the class must be defined
- denote the class using the syntax clasName::funcName
- methods know of all variables in the class
    - thats why we can just do `return x;` in the first function
    - this works because we're inside of the scope of the point2d class
    - in particular we're within a singular instance of the class
- methods know the other methods in the class

```
int point2d::getX(){
    return x;
}
void point2d::setX(int newX){
    x = newX;
}
double point2d::displacement(){

}
void point2d::translate(int dx, int dy) {
    setX(getX() + dx);
    setY(getY() + dy);
}
```

Constant methods
- some functions don't modify the object it's being called upon
- can be denoted as constant functions (both in declaration and implementation)
- compiler will enforce the fact that you aren't changing anything about the object
- why would you do this?
    - to avoid accidental modification
    - if you have a method not denoted as constant, you cannot call that function on an object that is constant
    - if the function doesn't change anything in the state of the system maybe it should be constant
    - constant refers to the state of the class object
```
class point2d {
public:
    double displacement() const;
    int getX() const;
    int getY() const;
    ...
}
...
int point2d::getX() const {
    return x;
}
```


Using classes
- recall that since `x` is private you can't run something like `myPoint.x = 1;`
- methods can be called like they are functions
- member variables are accessed just like a struct

```
point2d myPoint();
myPoint.publicVar = value;
myPoint.setX(3);
myPoint.setY(4);
cout << myPoint.displacement();
```

Constructors
- what are the default values of an object when created?
- for variables this is undefined
- for instances of classes, a constructor is called
- a constructor is a function that initializes a newly created object
    - has no return type
    - acts like a method otherwise

```
class point2d {
public:
    point2d(int x_, int y_);
    ...
}
point2d::point2d(int x_, int y_){
    setX(x_);
    setY(y_);
}
```

Default constructors:
- constructors that take no arguments
- are called when you make a new instance of the class
- if you don't define a default constructor it is defined implicitly by the compiler

```
class point2d {
public:
    point2d();
    ...
}

point2d::point2d(){
    setX(0);
    setY(0);
}
```

Copy Constructors
- used to initialize a newly created object based on an already existing object
- usually defined implicitly by the compiler (if you do not define one)
    - just sets each member variable equal to the same variable in the other object
    - beware! sometimes the implicit copy constructor is not going to work

```
class point2d{
public:
    point2d();
    point2d(const point2s other);
    ...
}
point2d::point2d(const point2d &other){
    setX(other.getX());
    setY(other.getY());
}
```

Destructors:
- just like we should initialize our objects when our objects are created, we should retired them when our objects are destroyed
- in charge of deallocating your member variables
- automatically called when the object goes out of scope
- make sure to define destructors for classes that allocate data
- implicit destructors simply do nothing

```
class sizedArray(){
public:
    sizedArray();
    ~sizedArray();
    ...
private:
    int* array;
    int size;
}
sizedArray::~sizedArray(){
    delete [] array;
}
```

Redefining operators
- ex: `+=` on two `point2d()`s
- need to redefine the operator

```
class point2d {
public:
    point2d();
    point2d operator+(point2d other);
    ...
}
point2d point2d::operator+(point2d other){
    setX(getX() + other.getX());
    setY(getY() + other.getY());
}
```





