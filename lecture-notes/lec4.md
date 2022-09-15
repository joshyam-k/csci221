## Hexadecimal

Consists of numbers 0-9 and letters A-F

The position i of a digit d indicates its importance. It contributes $d\times 16^i$ to the value of the number




$DEAD_{16} = D\times 16^3 + E\times 16^3 + A\times 16^1 + D\times 16^0$ 

## Machine Words

Computers store and manipulate binary data. Computer hardware processes baches of k bits in parallel
- a batch of k bits is called a machine word
- today a typical value of k is 32
- computation is very efficient on whole words
- most programming languages use a word to represent an int

A k-bit computer uses exactly k bits to represent an int (for this example let's assume $k=4$)


## Numbers in C

How many bits is an int in C?
- depends on the implementation
- you can use `sizeof()` but this is a huge plan
- or you can use specifically sized integer types (`int8_t`, int16_t`)
  - you can get these by using `#include <stdint.h>`
  - additional types are also defined in this file
  - highly recommend using these as standard practice

## Numbers: Math vs Computers

In math there are infinitely many numbers, in a k-bit computer there are finitely many numbers ($2^k$ to be exact), the line is finite.

This means we can't represent numbers larger than what fits in k bits. Even if we avoid writing larger numbers in a program, they may emerge during computation.

### Overflow

The result of adding two int's may not fit into a k bits word. We have an overflow when the result of an operation doesn't fit a machine word..

How do we deal with this?
- Raise an error or an exception
- continue execution in some meaningful way

Treating overflows as errors makes it hard to write correct code involving ints
- hard to debug
- hard to reason about

example:
- $n + (n-n)$ is always equal to $n$ on a computer
- $(n + n) - n$ is not always equal to $n$ on a computer due to overflows

People instinctively use math when writing code so this is bad.

### Handling overflows by continuing

Instead of aborting execution, just ignore the overflow bits, the result of the operation is what fits in the word.

Throwing out the overflow bit amounts to subtracting some multiple from the result

In the example of $k = 4$ we subtract as many multiples of 16 $(2^4)$ as we had to remove. This is just modular arithmetic.

#### Modular arithmetic

ex when $k=4$, i.e we can count up to 16:

$12 + 9 = 5$, $9 * 6 = 6$

C uses modular arithmetic. Rather than viewing numbers as lying on an infinite line, we think of them as wrapping around a circle with n positions. We carry out computations normally but return the position of the remainder. 

Usually this modular arithmetic saves us from experiencing math failures in our code. This is because of all the nice properties of modular arithmetic like associativity and what not. 

### Two's complement number system

Any number is represented as a sequence of digits. The position i of digit d indicates its importance

It contributes $d\times 2^i$ to the value of the number, except the last which contributes $-d\times 2^i$.

100 ... 000 is the smallest number, -1 is represnted by 111 ... 111

For example:

```
int foo(signed int x) {
  if (x + 1 > x) 
    return 1;
  else
    return 0;
}
```

This function does not always return 1 (if x is int_max, it returns 0) 


### How does division work?

We are used to division on real numbers, but with integers it doesn't always work. We introduce a new operation, the modulus, to pick up the slack. We want to define the operations $x/y$ and $x % y$ such that 

$(x/y) * y + (x \\% y) = x$ but this actually still isnt enough















