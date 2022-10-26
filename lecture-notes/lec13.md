## Intro to Assembly

By looking at what the computer is doing at the lowest level of software we can figure out what's going to be efficient when we write our own code.

- In C programming we perform abstract operations on a variable
- Hardware operates on bits, uses transistors and concrete operations
- assembly language is how we move from this abstract notion of variables and this concrete notion of bits (somewhere between these)

Terms
- ISA: interface for the machine architecture
- microarchitecture: implementation of the architecture (hardware) (we don't touch this)
- code forms:
    - machine code: the byte level programs that a processor executes
    - assembly code: a text representation of machine code

MIPS: an assembly language that we will focus on in this class
- using it because it is easier at a high level

### Assembly
There are 3 pieces of our CPU that talk to a memory
- PC: program counter (keeps track of what instruction we're going to run next)
- Condition Codes: stores status information about most recent logical or arithmetic operation (not really used in mips)
- Registers: heavily used program data (the data that we have easy access to)

Memory (data we don't have easy access to)
- byte addressable array
- code and user data
- stack to support procedures
- but for our purposes treat it as a black box

The CPU makes requests to data by sending addresses and it will read instructions from memory

Data Types in Assembly
- Byte (8 bits)
- Word (32 bits)
- Half-Word (16 bits)
- Single FP (32 bits)
- Double FP (64 bits)
- Code: Byte sequences encoding series of instructions (we'll do this implicitly)
- no aggregate types like arrays or structs (just contiguously allocated bytes in memory)
- MIPS is big Endian (the most significant byte is at the lowest address) this is one of those nice things we don't have to deal with in a high level language


### MIPS Registers
Just a piece of program to hold the data that we're using right now

32 Integer registers in MIPS
- Store 32 bits each
- R0 always stores value 0

32 Single FP registers
- store 32 bits each

16 Double FP registers
- store 64 bits each

These are just chunks of hardware that store a certain number of bits.

Register Naming
- Integer registers are identified by a `$<num>`
- Single Precision Floating Point registers are identified by a `$f<num>`
- By convention, we also give them names based on the job they're doing at the moment
    - `$zero` contains the hardwired value 0 (cannot be overwritten)
    - `$v0` and `$v1` are for results and expression evaluation
    - `$a0-$a3` are for arguments
    - `$s0-$s7` are for save values (values we're saving for something)
    - `$t0-$t9` are for temporary values
- compilers use these conventions to simplify linking

Why do we have registers?
- aren't they just memory that we've singled out as being special in some way?
- if we didn't have registers:
    - memory-memory ISA
    - all variables stored in memory
    - these are much much slower
- benefits of registers
    - smaller is faster
    - multiple concurrent accesses
    - shorter names
- Load store ISA:
    - arithmetic operations only use register operands
    - when you want to operate on some data you load it into a register, do the operations, then send it back to memory

Using Registers
- registers are a finite resource that needs to be managed
- goals:
    - keep data in registers as much as possible
    - always use data still in registers if possible
- issues:
    - finite number of registers available
    - spill registers to memory when all registers in use (ex arrays are often quickly too large)

Assembly Instructions
- The basic type of instruction has four components:
    - operation name
    - 1st source operand
    - 2nd source operand
    - destination operand
- ex: `add dst, src1, src2` equivalent to this in C: ` # dst = src1 + src2` 
    - dst, src1, src2 are register names `$()`
- ex: `add $1, $1, $1` doubles whatever value is in register 1
- ex: `add $2, $1, $3` adding the new value of register 1 and the value of register 3 and putting that result into register 2

Perform arithmetic function on register or memory data
- `a = b + b`
    - first need to assume values are in registers `$1-$3` respectively
    - `add $1, $2, $3`
- use `sub` to perform subtraction
- recognize that variables may move (around the registers, or to memory)
- `a = b + c + d - e` how do we do this in assembly?
    - recall that t is for temporary and s is for values
```
add $t0, $s1, $s2
add $t1, $t0, $s3
sub $s0, $t1, $s4
```

Constants
- We often want to specify an operand in code (want to add 8 to something). known as an immediate or literal value
    - use the `addi` instruction: `addi dst, src1, immediate`
    - values is between $-2^{15}$ and $2^{15}-1$ (ranged of a 16 bit signed integer)
        - sign extended to 32 bits
    - how would you use a larger constant? (this is going to be important in an assignment)
- Consider the C code `a++`
- In assembly we use: `addi, $s0, $s0, 1`
- there is no immediate subtract because you can just immediate add a negative number


Memory access
- what if we want data not in a register?
- all memory access happens through loads and stores
    - loads: move from memory -> registers
    - stores: move from registers -> memory
- using aligned words, half words, and bytes
- floating point loads and stores for accessing FP registers
- displacement based addressing mode

Importantly if you load half-words or bytes you store lowest 16 bits and 8 bits respectively of whatever is at that register
Data Transfer Instructions
- Data transfer instructions have three parts
    - operator name (transfer size)
    - destination register
    - base register address and constant offset (offset value is a signed constant)
- Load format of a word: `lw dst, offset(base)` the units of the offset are bytes
- ex: consider `a = b + *c;` (c is a pointer)
    - use `lw` instruction to load
    - assume `s0` stores a `s1` stores b and `s2` stores c
    - we start by loading into a temporary register the value that c points to
    - the offset is zero in this case (says that you're loading the value at base + 0)

```
lw $t0, 0($s2)
add $s0, $s1, $t0
```

- storing data is just the reverse and the instruction is nearly identical
- `sw src, offset(base)`
- ex: consider `*a = b + c;`

```
add $t0, $s1, $s2
sw $t0, 0($s0)
```

- note that `0($s0)` just means that you want to store it into the address of `$s0` thus the offset is 0

Arrays
- arrays are really pointers to the base address in memory
- address of element `A[0]`
- so use offset value to indicate which index
    - remember that addresses are in bytes, so multiply by the size of the element
    - so `array[5]` is at address `array + 5*4` in an integer array where each integer requires 4 bytes
    - unlike C, assembly does not do pointer arithmetic for you
- ex: consider `a = b + array[7]`
    - offset will be `7*4` 

```
lw $t0, 28($s3) // assume that $s3 holds the address for array
add $s0, $s1, $t0
```

Alignment
- in MIPS data is required to fall on addresses that are multiples of data size
- MIPS lays things out in memory in such a way that this alignmnet happens

Control Flow
- Conditional branch instructions are known as branches
- Basic block:
    - maximal sequence of instructions without branches or branch targets
- unconditional changes in the control flow are called jumps
- the target of the branch/jump is a label

Test for equality
- `beq reg1, reg2, label`
- ex: consider `if (a == b) goto L1`
    - `beq $s0, $s1, L1`

Inequality:
- `bne`

The j instruction jumps to a label `j label`
- ex: consider `if (i = j) f = g + h else f = g - h`

```
    beq $s3, $s4, True // if these two things are equal go to True
    sub $s0, $s1, $s2 
    j Exit // jump to exit
True: add $s0, $s1, $s2
Exit:
```

- If the equality holds we jump to True and add, otherwise we subtract and then jump to Exit

Other comparisons (see slides)
- register is "set" to 1 if a condition is met (`slt`, etc)
- can do with immediate values as well as unsigned values

## Assembly Continued

Reminder: Assembly connects your C programming to your hardware!

consider this C code:

```
int sum_pow2(int b, int c){
    int pow2[8] = {1,2,4,8,16,32,64,128};
    int a, ret;
    a = b + c;
    if (a < 8){
        ret = pow2[a];
    } else {
        ret = 0;        
    }
    return(ret);
}
```

We can write this in assembly as

```
sum pow2:
        addu $a0, $a0, $a1  \\ $a0 = b, $a1 = c and a = b + c, $a0 = a
        slti $v0, $a0, 8    \\ $v0 = a < 8
        beq $v0, $zero, Exceed  \\ go to exceed if $v0 == 0
        addiu $v1, $sp, 8   \\ $v1 is the address of pow2
        sll $v0, $a0, 2 \\ shift left the value at a0 by 2 which multiplies by powers of 2. so $v0 = a*4
        addu $v0, $v0, $v1 \\ $v0 = pow2 + a*4
        lw $v0, 0($v0)  \\ $v0 is pow2[a]
        j Return
Exceed: addu $v0, $zero, $zero  \\ $v0 = 0
Return: jr ra   \\ jr is jump to register 
```

Why dont we have a branch "less than" instruction for comparing two registers?
- such an instruction would be much more complicated
- assembly wants to do everyhing "in once cycle of a clock"

Loop Efficiency
- control transfer insturctions are very expensive
- how man control transfer instructions does this code need?

