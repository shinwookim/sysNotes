# Binary Number System
A binary number system works just like the familiar base-10 number system (which uses the symbols 0 thru 9)  The numbers are written positionally (each position of a digit within the number has meaning) with the most significant digit being written on the left-most side.

For instance, in a base-10 number system, a four digit number \\( 2023 \\) has the value: 
\\[ 2 \times 10^3 + 0 \times 10^2 + 2 \times 10^1 + 3 \times 10^0 \\]

The only difference in the base-2 number system is that the only allowable symbols are 0 and 1. With this requirement, each position of a digit now represents a power of 2. For instance, a four digit number \\( 1011 \\) has the value:
\\[1 \times 2^3 + 0 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 \\]

## Representable Numbers
Notice that, when we had four digits in the traditional base-10 number system, we could represent at most \\(10^4 = 10000\\) unique numbers. The smallest non-negative number would be \\[0000 = 0 \times 10^3 + 0 \times 10^2 + 0 \times 10^1 + 0 \times 10^0 =0 \\] and the largest representable number is \\[ 9999 = 9 \times 10^3 + 9 \times 10^2 + 9 \times 10^1 + 9 \times 10^0 = 10^4 -1 \\]

However, with the binary number system, we can represent at most \\(2^4 = 16_{10}\\) unique numbers with the smallest non-negative representable number being \\[0000 = 0 \times 2^3 + 0 \times 2^2 + 0 \times 2^1 + 0 \times 2^0 =0 \\] and the largest representable number being \\[1111= 1 \times 2^3 + 1 \times 2^2 + 1 \times 2^1 + 1 \times 2^0 = 2^4 -1 = 15_{10} \\]

Generalizing, a \\( n \\) digit binary number \\(d_{n-1} \ldots d_1 d_0 \\) has the value: 
\\[d_{n-1} \times 2^{n-1} + \cdots + d_1 \times 2^1 + d_0 \times 2^0 \\]
Furthermore, with \\( n \\) binary digits (bits), we can represent \\(2^n -1 \\) unique digits where the smallest non-negative representable number is \\(0 \\) and the largest representable number is \\(2^n -1\\).

| Min     | Max         |
| ------- | ----------- |
| \\(0\\) | \\(2^n-1\\) |

## Base-16 Number System
Because we can only use two symbols in the base-2 numbering system, our *bit sequences* can easily become too long to write by hand. Hence, we often use a shorthanded base-16 (also called **hexadecimal**) notation to condense the representation of bits. In this shorthand, we use 16 symbols \\( \\{1 \ldots 9, A, B, C, D, E, F \\} \\) where \\(0 \\) through \\(9 \\) represent their base-10 counterparts and \\(A \\) through \\(F \\) represent 10 through 15.

Notably, this shorthand is very easy to convert to binary and vice versa. All we have to do is, block groups of 4 bits and convert each block to a corresponding hex digit. For example, we can do the following conversion in both directions:
![Binary to Hexadecimal](./bin-to-hex.svg)
Here, the line at the top (`0xFACE`) is the hexadecimal representation and the line at the bottom (`0b1111 1010 1100 1110`) is the binary representation.