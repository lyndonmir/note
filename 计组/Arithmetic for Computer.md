# 3.1 Introduction
## Words
- 4bytes or 8bytes
## Generic Implementation
- use PC to supply instruction address
- get instruction from memory
- read registers
- use instructino to decide what to do
## Number types
- Integer unsigned
- Signed: signed plus mode or complement
- Floating point numbers : structure
# 3.2 ALU-- add and substract
## Constitute ALU
### Composition
- Full adder
- substraction
- comparision
- overflow detection
- zero detector
### ways
- extended the adder
- parallel redundant selet
### Overflow
- Value 
- Sign: examine two carries
### Comparision
- by division and check sign
### Zero detector
- if all bits are 0, return 1
- else return 0
### Hardware Code
- always @(\*)
- Sensitive List
## Constitute adder
### Full adder
### Carry Lookahead Development
- associate with ways to calculate decimal add, evernote
- cause a large or gate
- group carry lookahead logic,
### Carry select adder(CSA)
- use more carry lookahead adder
# 3.3 Multiplication
## General Idea
- If multiplier is 1: add multiplicand
- else add 0
- shift multiplicand left by 1 bit
## V1
- Requires 64 iterations Addition/ Shift/Comparision
## V2
- Real addition is performed only with 64 bits
- Addition performed only on left half of product register
- shift of product register
- shift the multiplier
## V3
- based V2, use 128-bit product's lower 64 bits for the multiplier
## Signed multiplication
### General rule
- store the signs of the operands
- Convert signed numbers to unsigned
- perform multiplication
- xor stored sign
### Booth's Algorithm
- substract at first '1' in multiplier
- shift for the sequence of '1's
- add where prior step had last '1'
### Booth's Rule
- 10: subtract multiplicand from left(the left bit of 10, equals 1)
- 11 or 00: no arithmetic operation-shift
- 01: add multiplicand to left half
- $Bit_{-1}$ = '0'
### Example
## Faster Multiplication
- upside-down tree structure
- divide and conquer
- add adjoint two bits and so on
## RISC-V Multiplication
- In successor lesson
# 3.4 Division
## General Rule
- check for 0 divisor
- if divisor $\le$ dividend bits, 1 bit in quotient, subtract,Otherwise, 0 bit in quotient, bring down next dividend bit
- Do the subtract, and if remainder goes < 0, add divisor back
- If signed, divide using absolute values, adjust sign
## V1
- shift right divisor
- when subtract, use full bits not half
## V2
- Remainder contains dividend and quotient
- shift left Remainder
- when  subtract, use left half of remainder
- shift right finally to make "remainder" right
## signed division
## Faster division
## RISK-c Division
# 3.5 Floating point numbers
## Representation
- Sign
- Significand
- Exponent
## Types
- Single precision 31|31-23|22-0(8-bit exponent);
- Double precision 31|30-20|19-0;31-0(11-bit exponent);
## attribute
- Leading '1'bit of significand is implicit->save one bit
- Exponent is biased: 127 for single and 1023 for  double
- $(-1)^{sign}\times{(1+significand)\times{2^{exponent-bias}}}$
## Single-Precision Range
- Exponents 00000000 and 11111111 reserved
- Smallest : Fraction: all 0; Exponent 0...1;  $\approx\pm1.2\times{10^{-38}}$
- Largest : Fraction: all 1; Exponent 111..10 $\approx\pm3.4\times{10^{+38}}$
## Double-Precision Range
- Exponents 00000..000 and 111111..11 reserved
- Smallest : Fraction: all 0; Exponent 0...1 ;$\approx\pm2.2\times{10^{-308}}$
- Largest : Fraction: all 1; Exponent 111..10;$\approx\pm1.8\times{10^{+308}}$
## Floating-Point Precision
- Single: $23\times{log_{10}2}\approx6$ decimal digits
- Double:$52\times{log_{10}2}\approx$ 16
## Limitations
- Overflow
- Underflow
## Infinities and NaNs
- Exponent = 111.....1, Fraction = 000..0 : $\pm$Infinity
- Exponent = 111.....1, Fraction $\ne$ 000..0: NaN
## Addition
- Alignment
- Addition
- Normalisation
- Rounding
- Algorithm pics
## Multiplication
- Add exponents(bias)
- Multiply the significands
- Normalise
- Over-underflow
- Rounding
- Sign
## Division
- Subtraction of exponents
- Division of the significants
- Normalisation
- Runding
- Sign
# 3.6 Accurate Arithmetic
## Extra bits of precision(guard, round, sticky)
- guard: The first of two extra bits
- Round: method to make the immediate floating-point result fit  the floating-point format
- Units in the last place(ulp)
## Choice of rounding modes
