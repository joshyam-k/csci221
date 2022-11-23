## Assembly Continued

Writing out procedures in the complicated way described in the slides allows us to restore everything to how it was before the procedure call (only changing the things we wanted to change). Thus we are able to create functions that behave appropriately in assembly.

Tail recursion
- functions that directly return the value of their recursive call
    - no work done after the recursive call
- we can convert them into loops

Making Factorial Tail recursive

```
int fact(int n){
    if (n <= 1){
        return(1);
    }
    else 
        return(n*fact(n-1));
}
```

split into two functions

```
int fact(int n){
    return fact_t(n, 1);
}

int fact_t(n, val){
    if (n <= 1){
        return val;
    }
    val = val*n;
    n = n-1;
    return fact_t(n, val);
}
```

now it is tail recursive!
- now how do we convert the code to only use loops?

pseudocode (fun blend of C and assembly lol)
```
int fact_t(n, val){
    start:
    if (n <= 1){
        return val;
    }
    val = val*n;
    n = n-1;
    goto start
}
```

By making this optimization we:
- turn recursive chain into single procedure
- eliminate procedure call overhead
- no stack frame needed (so no stackoverflow risk)
- constant space requirement

### Integer Multiplication

Multiplication takes two 32 bit numbers and returns a 64 bit number
- but integer registers are 32 bits...

So we store the result in a special product register
- composed of two 32 bit registrs (HI and LO) that hold the upper and lower 32 bits from the multiplication

```
mult $s0, $s1   # multiply the numbers in these registers
mfhi $t0        # loads the uper 32 bits from the product register
mflo $t1        # loads the lower 32 bits from the product register
```

### Integer Division

Again uses the HI and LO registers
- LO contains the quotient
- HI holds the remainder









