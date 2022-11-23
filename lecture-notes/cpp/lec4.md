## The C++ Standard Template Library

The STL contains many class and function templates that may be used to store, search, and perform algorithms on data structures
- you should implement your own data structures and algorithms only if the ones provided in the STL do not suffice
- STL consists of:
    - container classes (data structures)
        - an object that stores a collection of other objects
        - 3 typs of containers: sequence containers (store sequences of values), associative containers (use keys to access data), container adapters (specialized interfaces for general containers)
        - STL containers store by value, not by reference
        - when you insert an object, the container makes a copy and if the container needs to rearrange objects, it makes copies
        - if you dont want this, you can insert a wrapper object with a pointer to the object (smart pointers, see lec5)
        - **sequence containers**:
            - arrays, vectors (like arrays but with nicer features), deque, list (like a linked list).
        - **associative containers**:
            - sets, multiset, map, multimap
        - **container adapters**:
            - stacks, queue, priority_queue
    - iterators
    - algorithms

#### C++ arrays

- fixed size, fast random acces, slow to insert or delete in the middle, size cannot be changed at runtime, accessed using operator `[]`

#### vector

- resizeable array `#include <vector>` `vector<string> vec;`
- fast random access
- slow to insert or delete in the middle
- fast to insert or delete at the end
- other operations (size, empty, clear)
- vectors are allocated with too much space so that it's easier to add on to the end

#### deque

- like a vector but with fast insertion and deletion at both ends
- `#include <deque>` `deque<string> dq;`
- everything else the same
- allocates extra space both at the front and at the back to enable this fast insertion or deletion on both ends

#### list

- doubly-linked list `#include <list>` `list<string> lst;`
- slow random access (need to traverse using iterator)

#### set

- `#include <set>` `set<string> s;`
- stores a set of values (i.e keys)
- values are unique
- implemented as a balanced binary search tree
- fast insert and delete
- fast search

#### multiset

- stores a set of values
- like a set, but values need not be unique

#### map

- stores a set of (key, value) pairs; each key has one value
- implemented as a balanced binary search tree
- `#include <map>` `map <string, int> m;`
- ex: `m["fred"] = 99;`
- fast insert and delete and search

#### multimap

- like a map, but each key can have multiple values
- need to be more explicit with pairings and implementations

### sorting

- STL associative containers are implemented internally using a balanced BST
- thus the key class must support the operator `<` on another instance of its type
- if they don't you can alternatively pass a comparator class to the template that it should use to order elements

ex:
```
set<employee* > employees;

class employeeComparator {
public:
    bool operator() (const employee* a, const employee* b){
        return (a -> getID() < b -> getID());
    }
}

set<employee*, employeeComparator> employees;
```

#### container adapters: stack

- `#include <stack>` `stack<string> st;`
- can be used with a vector, deque, or list (uses a deque by default)
- spacing ex: `stack < string, vector<string> > st;` needs this space to avoid having the compiler think we are using the `>>` operator
- hides, rather than adds functionality

#### queue

- last in last out, first in first out (which is what makes them different from stacks which are last in first out)
- `queue<string> q; // uses deque by default`

#### priority_queue

- elements put into the queue have to have a priority
- `priority_queue<int> pq;`

### Scanning through containers

How do we iterate over the values stored in a container?
- for vectors, deques, and arrays you can just use a loop and `[]`
- this style doesnt work for other container types though

#### Iterators

Iterators are pointer-like objects that can be used to access the values in a container
- all can be incremented, copied, copy-constructed, some can be dereferenced on either side of the expression and decremented

Iterator ranges
- containers `begin` method returns an iterator pointing to the first value in the container
- containers `end` method returns an iterator pointing to one beyond the last element in the container

Iterator order
- for sequences there is a natural first to last order
- for sets and maps the values are returned by doing an in order traversal of the BST
- you can also iterate in reverse using `rbegin` and `rend`

Type Inference
- the `auto` keyword can be used to infer types
- part of the C++ 11 standard
- requires the expression using `auto` to contain explicity initialization

- `std::vector<int> facts1 = Factors(2232131)`
- since Factors returns a vector of ints, then auto is smart enough to set facts2 to be this as well
    - `auto facts2 = Factors(4346436);`
- works well with iterators

### For Each

- Syntactic sugar

```
for (declaration : expression){
    statements;
}
```

- `declaration` defines a loop variable
- `expression` is an object representing a sequence
    - strings, initializer lists, arrays with explicit length defined, STL containers that support iterators

### Writing classes that work with the STL

- classes that will be stored in STL containers should explicitly define the following
    - default constructor
    - copy constructor
    - destructor
    - assignment operator (`=`)
    - comparison operator
- not all of these are always necessary, sometimes you can get away with not using all of them, but its often easier to just implement all of these things
- this will really help you avoid errors

















