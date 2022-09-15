## Hexadecimal

Consists of numbers 0-9 and letters A-F


The position i of a digit d indicates its importance. It contributes $d\times 16^i$ to the value of the number.

One hex corresponds to 4 bits. This makes it very easy to convert between binary and hex as you simply replace every group of 4 bits with the corresponding hex digit.

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

Most programming languages use a machine word to represent an int
- Internally 37 is not represented as 100101
- It is represented as 00000000000000000000000000100101

Thus a k-bit computer uses exactly k-bits to represent an int. We say that numbers have a fixed size in a computer

## Numbers: Math vs Computers

In math there are infinitely many numbers, in a k-bit computer there are finitely many numbers ($2^k$ to be exact), the line is finite. 

On a k-bit computer we can represent only $2^k$ distinct numbers.

This means we can't represent numbers larger than what fits in k bits. Even if we avoid writing larger numbers in a program, they may emerge during computation.

### Overflow

The result of adding two int's may not fit into a k bits word. We have an overflow when the result of an operation doesn't fit in a machine word.

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

Throwing out the overflow bit amounts to subtracting some multiple from the result. In general we subtract as many multiples of $2^k$ as necessary so that the result fits in k-bits.

In the example of $k = 4$ we subtract as many multiples of 16 $(2^4)$ as needed to make our number fit into k-bits. This just modular arithmetic. In fact, ignoring the overflow bits simply computes the result modulo $2^k$.

#### Modular arithmetic

Evaluate an expression normally, but return the remainder of dividing it by $n$. 5 modulo 3 is equal to 1. Results in numbers between 0 and $n-1$.

ex when $k=4$, i.e we can count up to 16:

$12 + 9 = 5$, $9 * 6 = 6$

C uses modular arithmetic. Rather than viewing numbers as lying on an infinite line, we think of them as wrapping around a circle with n positions. We carry out computations normally but return the position of the result on a modular arthmetic circle. 

Usually this modular arithmetic saves us from experiencing math failures in our code. This is because of all the nice properties of modular arithmetic like associativity and what not. Here's an example

```
int foo(int x) {
    int z = 1 + x
    if (x + 1 = z)
	return 1;
    else
	return 0;
}
```

Although we might be suspicious of this function failing to always return 1 because of potential overflow issues, this function will actually always return 1 due to the fact that the properties of modular arithmetic guarantee that $x + 1 = 1 + x$ no matter what.

Modular arithmetic tells us that many numbers correspond to the same bit sequence

### Two's complement number system

Any number is represented as a sequence of digits. The position i of digit d indicates its importance

It contributes $d\times 2^i$ to the value of the number, except the last which contributes $-d\times 2^i$.

Each k-bit machine word corresponds to a number between $-2^{k-1}$ and $2^{k-1} - 1$. So the leftmost bit tells the sign. 1 makes a number negative, 0 keeps it non-negative. It is commonly called the sign bit.

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

This function does not always return 1 due to the fact that x is a signed int. If x is the largest machine word on a machine then $x + 1$ loops the number back to the smallest machine word and so the function returns 0. i.e 011...111 + 000...001 returns 100...000 which is the smallest signed int because the first bit is the sign bit and makes the number negative.


### How does division work?

We are used to division on real numbers, but with integers it doesn't always work. We introduce a new operation, the modulus, to pick up the slack. We want to define the operations $x/y$ and $x % y$ such that 

$(x/y) * y + (x \\% y) = x$ but this actually still isnt enough















