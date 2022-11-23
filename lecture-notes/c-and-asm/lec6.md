## Floating Point Numbers

How should we represent 0.625 in binary?

Any number is represented as a sequence of digits
- $100.101_2 = 1\times 2^2 + 0\times 2^1 + 0\times 2^0 + 1\times 2^{-1} + 0\times 2^{-2} + 1\times 2^{-3}$

Observations
- divide by 2 by shifting right (unsigned)
- multiply by 2 by shifting left
- numbers of the form 0.1111.. are just below 1.0

Converting decimal to binary
- multiply the number by 2
- record the 1s place as the next most significant bit
- multiply the remainder by 2 and continue
- $0.625 = 0.101$ 

Note that we can only represent numbers that are powers of two (numbers that are not need an infinite number of digits), so other numbers must be rounded.

Despite these limitations we still primarily use this system.

How do we allocate digits between integers and fractions? 
- more integer digits let us represent larger numbers
- more fraction digits let us represent more precise numbers

### Scientific notation (aka floating point numbers)

We typically allow significand values in the range $[1.0, 2.0)$
- $160 = 10100000_2 = 1.01 \times 2^7$
- (not $10.1 \times 2^6$)

#### IEEE Floating Point Standard

- single precision: 32 bits
    - ~7 decimal digits, $10^{\pm 38}$
- double precision: 64 bits
    - ~16 decimal digits, $10^{\pm 308}$

First bit is used as a sign bit

Three types of encodings, dependent what the exponent is. If the exponent is...
- all zeroes (denormalized encoding, used for numbers close to zero)
- all ones (special encoding, used for infinity, NaN, etc)
- anything else (normalized encoding, used for most numbers)

Normalized encoding
- occurs when the exponent is no 00...00 or 11...11
- exponent coded as a biased value: $E = exp - Bias$
    - exp: unsigned value of the exponent field
    - bias: $2^{k-1}-1$, where k is the number of exponent bits
- single precision: Bias = 127
- significand coded with implied leading 1: $1.xxx...x2$
    - so you get the leading bit for "free"

#### Ex

value: float $F = 15213.0$
- $15213 = 1.1101101101101 \times 2^{13}$
- check course slides "Floating Point" slide titled "Normalized Encoding Example"
- Decoding examples in slides are also super super helpful!!


### Floating point operations

Basic idea
- compute exact result first
- then make it fit into the desired precision
- but how to round?

Round to nearest even: rounds to nearest number, but breaks ties towards even numbers
- this is the default rounding mode
- why is it default?
- the reason is that the common alternatives are statistically biased
    - sum of set of positive numbers will consistently be biased








