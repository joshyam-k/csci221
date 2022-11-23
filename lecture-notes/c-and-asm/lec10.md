## Debugging and Design

### Debugging
Defects and Infections
- the programmer creates a defect
- the defect causes an infection
- the infection propogates
- the infection causes a failure

So the goal of debugging is tracing failures back to the defects

Challenges
- not every defect causes a failure
- testing can only show the presence of errors -not their absence

Explicit Debugging
- stating the problem
- describe the problem aloud or in writing (rubber duck or teddy bear method)

Scientific Debugging
- first construct a hypothesis as to the defect
    - propose a possible defect and why it explains the failure conditons
- Ockham's Razor- given several hypotheses, pick the simplest
- make predictions based on your hypothesis
    - what do you expect to happen under new conditions
    - what data would confirm or refute your hypothesis
    - how can I collect that data?
- a set of experiments can confirm the hypothesis
    - this is the diagnosis of the defect
- develop a fix for the defect
- run experiments to confirm the fix

Not every problem needs scientific debugging

Common Defect Causes
- use of uninitialized variables
- unused values
- unreachable code
- memory leaks
- interface misuse
- Null pointers


### Design
a good design needs to achieve many things:
- performance
- availability
- modifiability, portability
- scalability
- security
- testability
- usability
- cost to build, cost to operate
- readability

Two high level ideas:
- complexity management
- communication

Complexity Management
- there are well known limits to how much complexity a human can manage easily
- patterns help increase this amount
- techniques to help manage complexity: separation of concerns, modularity, reusability, extensibility, abstraction, information hiding
- design code to be testable, try to reuse testable chunks

Testable design is modular
- separation of concerns
    - create helper functions so each function does "one thing"
    - functions should neither do too much nor too little
    - avoid duplicated code
- encapsulation, abstraction, and respecting the interface
    - no outside code intrudes on the innter workings of another module

Trust the compiler
- use plenty of temporary variables
- use plenty of functions
- let the compiler do the math

Communication
when writing code the author is communicating with:
- the machine
- other developers of the system

Techniques
- tests
- naming
- comments

Avoid using deliberately meaningless names
- use words with precise meanings
- prefer fewer words in names
- avoid abbreviations in names
- read the code out loud to check that it sounds okay









