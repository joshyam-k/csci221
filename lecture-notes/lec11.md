## Communication & Naming (con't)

Words are better than abbreviations

Comments
- don't explain awkward logic, just improve the code to make it clearer
- answer the question: why does this code exist?
- write short comments of what the code will do (helps you think about the modular components of your code)
- revise comments when you revise code


## Testing

Debugging and testing are inevitable when writing software
- goal: try as many critical input combinations as possible given the time and resource constraints
- want to achieve "good coverage" of the code

Test Coverage
- measures the degree to which the specification or code of a program is being tested
- "big picture" specification testing focus on the coverage of the input space without necessarily testing each part of the software
- "implementation details" measures the degree to which elements of the program source code have been tested

Terminology
- test case: one choice of input and the expected output or behavior
- test: a finite collection of test cases
- extreme: test-driven development (don't do anything unless you develop a test plan for it)

Ideally every test case will expose a different fault, but we do not live in an ideal world and so this is hardly ever perfectly true

Test Priority
- test cases should be prioritized
- test are about finding developer errors and people are prone to make certain kinds of errors

Methodology
- static analysis:
    - hand execution: read the source code
    - walk through: informal presentation to others
    - code inspection: formal presentation to others
    - automated tools to check for syntacic and semantic errors
- dynamic analysis:
    - black box testing
    - white box testing

Testing Types
- black box testing explores input space of functionality defined by interface specification (does not requre access to code)
    - equivalence testing
    - boundary testing
- white box testing exploits structure within program
    - control flow testing
    - state based testing

Equivalence testing
- divides the possible inputs into equivalence groups
    - the program is expected to "behave the same" within a group
    - developers probably handle inputs from the same group in the same manner
- equivalence classes: how do you partition your input space?
    - for input parameters specified over a range of values. partition the space into one valid and two invalid classes
    - for input parameter specified by a set of values. partition the space into one valid and one invalid class

Boundary Testing
- a special case of equivalence testing that focuses on the boundary values of input parameters
- select "edges" or "outliers" of each equivalence class
    - min/max values
    - empty set
    - empty strings
    - null pointers

Control Flow testing
- Represent program with control graph
- nodes represent instructions
- often instructions without branches are grouped into a single node
- edges represent possible execution paths

Maximizing coverage in control-flow testing
- each statement is executed at least once by some test case
- every branch of the control flow is traversed at least once by some test case
    - when you have an if statement make it so the conditional takes on true and false at least once each
- loops should be tested with varying iterations (0: skipped entirely, 1: no return, many)

State Based testing
- defines a set of abstract states taht a software unit can take and tests the units behavior by comparing its actual states to the expected states
- populat with object-oriented systems
- finite state machine (FSM): the state of an object is defined as a constraint on the values of its attributes

FSM example: keypad with 4 numbers
- locked state: armed and no attempts made
- accepting inputs: locked and attempts have been made
- unlocked, blocked, undefined, etc


Unit testing
- a test driver simulates the part of the system that invokes operations on the tested environment
- a test stub simulates the components that are being called by the tested component
- follows this cycle:
    - creates the thing to be tested
    - have the test driver invoke the operation
    - evaluate the actual states
















