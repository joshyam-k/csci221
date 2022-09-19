## Using ints beyond numbers

An integer is really just a group of bits. So far we used the type int to represent integers, btu we can use an into to represent any data we can fit in the bits.
- then an int does not represent a number but a bit pattern
- C has a special set of operations to manipulate bit patterns

#### Pixels as 32-bit ints

A pixel is a dot of color in an image
- the color of a pixel can be described by specifying how much RGB it contains and how opaque it is
- pixels can be efficiently represented as bit patterns
- Bits 0-7 give the intensity of blue, bits 8-15 give the intensity of green, and 16-23 give the intensity of red
- this is a good place to use hexadecimal!

The bitwise operators manipulate the bits of a bit pattern independently of the other bits nearby.

The bitwise operations take ints as input and return an int. They apply the truth tables on each bit of their inputs:

Ex: 1100 and 1010 
- & would give us 1000 since it works digit by digit. 0 & 0 is 0, 1 & 0 is 0, 0 & 1 us 0, 1 & 1 is 1 so we get 1000
- | would give 1110

& and | are related to && and || but
- & and | take two ints and return an int
- && and || take two bools and return a bool

So what is 1010 && 0110?
- exact value is implementation dependent
- but it is guaranteed to be non-zero

So what is 1010 && 0000?
- answer is 0000

If we "and" any bit b with
- 0 we always get 0
- 1 we always get b back

If the int x is a bit pattern, then x & m is and int that
- has the same bits as x where m is 1
- has a zero where m is zero

Ex: We want to write a function that returns a pixel identical to p but with no red in it
- Zero out red component of p- bits 16-23
- preserve all the other bits
- We can use the mask 0xFF00FFFF

```
int clear_red(int p){
    return p & 0xFF00FFFF;
}
```

If we "or" any bit b with
- 0 we always get b back
- 1 we always get 1

Common uses of | are
- setting bits to 1
- constructing bit pattern from parts

Ex: We want to make a pixel fully opaque
- set the alpha bits to 1 - bits 24-31
- preserve the other component of p

```
int opacify(int p){
    return p | 0xFF000000;
}
```

Bitwise negation flips the bit

Ex: return the pixel with the same opacity but inverted colors
- preserve the alpha channel
- other channels should be 255 minus their original value
- this works because when we "or" the two bit patterns we keep the opacity and get the flipped colors too

```
int invert(int p){
    return (p & FF000000) | (~p & 0x00FFFFFF);
}
```

If we "xor" any bit b with
- 0 we always get b back
- b we always get 0
- 1 we always get the inverse

Switching variables with xor
- you want to swap two variables values without using a third

```
void swap(int p, int q){
    p = p ^ q;
    q = p ^ q;
    p = p ^ q;
}
```

this has to do with the commutativity and associativity of ^
- $p'' = p' ^ q'$
- $q'' = p'' ^ q' = p' ^ 0 = p'$
- $p''' = p'' ^ q'' = (p' ^ q') ^ p' = q' ^ 0 = q'$

so cool!

#### Moving bits' positions

The shift opperations enable us to move bits around
- left shift: `x << k` moves the bits of x left by k positions
    - the leftmost k bits of x are dropped
    - the rightmost k bits of the result are set to 0
    - undefined behavior if k is negative or k is greater than the number of bits of the number
    - `0101 << 1` evaluates to 1010
- right shift `x >> k` moves the bits of x right by k positions
    - the rightmost k bits of x are dropped
    - the leftmost k bits of the result are a copy of the leftmost bit of x
    - `0101 >> 1` results in 0010
    - `1010 >> 3` results in 1111

Ex: copying a pixels blue value
- return a pixel whose red and green components have the same intensity as p's blue component
- isolate the blue component of p
- put it in the red, green, and blue positions

```
int blue_everywhere(int p){
    int alpha = p & 0xFF000000;
    int blue = p & 000000FF;
    return alpha | (blue << 16) | (blue << 8) | blue
}
```

As a summary
- ints can represent integers (manipulated using the arithmetic operations)
- ints can encode bit patterns (manipulated using the bitwise operations and the shifts)

Beware of sizing issues!



