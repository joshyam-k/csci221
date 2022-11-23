## Assembly Wrap-Up

MIPS instructions are encoded in different forms depending on the arguments
- R format: modifying two different pieces of data 
- I format: immediate instruction format
- J format: jump format

Pseudo-instructions
- assembler allows use of shortcut instructions that don't exist in the ISA
```
move %t0, $t1           # this instruction
addu $t0, $zero, $t1    # just does this behind the scenes
```

The `$at` register is reserved for the assembler

so when you run something like 
```
blt $t0, $t1, L1    # this instruction
slt $at, $t0, $t1   # just does these two behind the scenes
bne $at, $zero, L1
```

### Procedures

Procedures are required for structured programming (functions, methods, subroutines)

Implementing procedures in assembly requres
- memory space must be set aside for local variables
- arguments must be passed in and return values passed out
- execution must continue after the call

Steps
- place parameters in a place where the procedure can access them
- transfer control to the procedure
- acquire the storage resources needed for the procedure
- perform the desired task
- place the result value in a place where the calling program can access it

#### Returning from calls
- to jump to a procedure use either of the followng instructions
```
jal target  # jump and link to label
jalr $dest  # jump and link to $dest
```

'Jump and link' instructions stores the next instruction address in `$ra` before transferring control to the target/destination

To return, use the `jr` instruction

#### Stack-Based Languages
- languages that support recursion
    - need some place to store state of each instantiation
- Stack Discipline (last in first out)
- Stack allocated in frames


#### Stacks

Data is pushed onto the stack to store it and popped from the stack when no longer needed
- MIPS does not support in hardware
- we must do this using loads and stores

Calling convention
- common rules across procedures required

Using Stacks
- stacks can grow up or down (stack grows down in MIPS (as you call more instructions the stack pointer decreases))
- entire stack from is pushed and popped rather than a single element


#### Handing data in procedure calls
What happens to data in registers on a procedure call?
- preserved registers (callee save)
    - save register values on stack prior to use
    - restore registers before return
    - includes `$s0-$s7`, and others
- not preserved registers (caller save)
    - should be saved by caller if needed after procedure call
    - `$v0, $v1, $a0-$a3, $t0-$t9`

#### Call and Return
- caller
    - save caller-saved registers `$a0-$a3` and `$t0-$t9`
    - load arguments in `$a0-$a3`, rest passed on stack
    - execute jal instruction (will store a pointer for where to return to)
- callee setup
    - allocate memory for new frame `$sp = $sp - frame`
    - save callee saved registers `$s0-$s7`, `$fp`, `$ra`
    - set frame pointer `$fp = $sp + frame size - 4`
- callee return
    - place return value in `$v0` and `$v1`
    - restore any callee-saved registers
    - pop stack
    - return by `jr $ra`









