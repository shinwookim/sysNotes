# Integer Encoding
A computer stores information as a stream of bits (e.g., `0xe29884`). But what do those bits actually mean? For that, we need to assign an **interpretation** to the bit stream.

## Unsigned Numbers
One possible interpretation of a stream of bits is as an unsigned number. This is the most simple interpretation of a bit stream, and we read the number (represented in hexadecimal )as follows:

\\[\begin{equation}
\begin{split}
\verb|0xe29884| & = \verb|e| \times 16^5 + 2 \times 16^4 + 9 \times 16^3 + 8 \times 16^2 + 8 \times 16^1 + 4 \times16^0 \\\\
                & = 14 \times 16^5 + 2 \times 16^4 + 9 \times 16^3 + 8 \times 16^2 + 8 \times 16^ 1 + 4 \times 16^0 \\\\
                & = 14680064 + 131072 + 36864 + 2048 + 128 + 4 \\\\
                & = 14850180
\end{split}
\end{equation}\\]

Similarly, if we want to convert a binary number (e.g., `0b1101`) to a decimal number, we’d apply the same process using powers of 2 instead of 16:


\\[\begin{equation}
\begin{split}
\verb|0b1101|   & = 1 \times 2^3 + 1 \times 2^2 + 0 \times 2^1 + 1 \times 2^0 \\\\
                & = 2^3 + 2^2 0 + 2^0 \\\\
                & = 8 + 4 + 0 + 1 \\\\
                & = 13
\end{split}
\end{equation}\\]

## Signed Numbers
Another possible interpretation of a hex digit is as an signed number. One of the most common way of representing signed numbers using ones and zeros is called **two's complement**. In two's complement, the most significant bit (MSb) denotes the sign of a number. For instance, given a 3-bit number:

| Binary Representation | Value |
| --------------------- | ----- |
| `100`                 | -4    |
| `101`                 | -3    |
| `110`                 | -2    |
| `111`                 | -1    |
| `000`                 | 0     |
| `001`                 | 1     |
| `010`                 | 2     |
| `011`                 | 3     |

we can see that numbers with a 1 in the left-most bit is negative, whereas numbers with a 0 in the left-most bit are positive. We can also see that there is one additional negative number than the positives. That is, \\(-4\\) does not have a positive counterpart. Two's complement is achieved by:
1. Starting with the equivalent positive number.
2. Inverting (or flip) all bits – changing every 0 to 1, and every 1 to 0;
3. Adding 1 to the entire inverted number, ignoring any overflow

For example, to write \\(-3 \\) using 4 bits:
1. We first write the bit pattern for positive \\(3 \implies \verb|0b0010|\\).
2. We then flips all the bits \\( \verb|0b0010| \implies \verb|0b1100|\\).
3. Finally, we add 1 to get \\( \verb|0b1100| + 1 \implies \verb|0b1101|\\).

Notice that if we apply the same process for the bit pattern of \\( -3 \\), we get \\(\verb|0b1101| \implies \verb|0b0010| \implies \verb|0b0011| \\) which is the bit pattern for positive \\( 3\\). That is, by applying the process above, we can negate any number in two's complement. Formally, this process can be written as:

\\[\begin{equation}
\text{Encode}(x)
    \begin{cases} 
      x & x\geq 0 \\\\
      x + 2^n & x < 0 
    \end{cases} \\\\
\text{Decode}(x)
    \begin{cases} 
      x & x < 2 ^{n-1} \\\\
      x - 2^n & x \geq 2 ^{n-1} 
    \end{cases}
\end{equation}\\]

Two's complement is useful since arithmetic can be done on numbers of either sign without having to do anything special.

### Integer Ranges
We saw that for \\(n \\)-bit unsigned numbers, the range of representable integers were \\(0\\) to \\(2^n-1\\). However, if we are using two's complement signed numbers, the range of representable integers become \\(-2^{n-1}\\) to \\(2^{n-1} -1\\) (since there is one more negative number than there are positive numbers). This also means that there is no positive counterpart to \\(-2^{n-1}\\). In fact, if we attempt to negate this number, we get:
\\[
-(-2^{n-1})=-(\verb|0b100|\ldots\verb|0|)=\verb|0b011|\ldots\verb|1|+1=\verb|0b100|\ldots\verb|0| = -2^{n-1}
\\]

### Overflow
We know that for \\(n \\)-bit signed numbers, the largest representable integer is \\(2^{n-1}-1\\). But, what happens when we try to add \\(1\\) to this number?

Consider \\(\verb|0b0111| \\), a 4-bit signed number, whose value is 7. If we try adding 1 to this number, we get:
\\[
7+1=\verb|0b0111| + 1 = \verb|0b1000|=-8
\\] 
This is an example of an **integer overflow** which occurs when an arithmetic operation attempts to create a numeric value that is outside of the range that can be represented with a given number of digits. Integer overflows can occur in either direction:
- When an addition produces a value that is higher than the maximum representable value.
- When a subtraction produces a value that is lower than the minimum representable value.

Integer overflows are a common source of *undefined behavior* and can often lead to bugs in programs. Hence, detecting overflow is a crucial task for programmers.

An overflow occurs when the value affects the sign:
- If adding two positive numbers yields a negative result, an overflow occurred.
- If subtracting two negative number yields a positive result, an overflow occurred.
- If subtracting a negative number from a positive number yields a negative result, an overflow occurred.
- If subtracting a positive number from a negative number yields a positive result, an overflow occurred.
- An overflow cannot occur when subtracting two numbers of the same sign.
- An overflow cannot occur when adding two numbers of opposing signs.

## Integers in C
In Java, integers were signed variables which used the two's complement interpretation. This meant that variables could hold values from \\(-2^{n-1} \\) to \\(2^{n-1} -1\\) where \\(n\\) is given by the variable type.

| Integer Types | size    |
| ------------- | ------- |
| byte          | 8 bits  |
| short         | 16 bits |
| int           | 32 bits |
| long          | 64 bits |

In C, variables can be declared as either signed or unsigned. This means that any variable declared as unsigned can hold values from \\(0\\) to \\(2^n -1\\) and variables declared as signed can hold values from \\(-2^{n-1}\\) to \\(2^{n -1}-1\\).[^c-tc]

The \\(n\\), like in Java, is given by the variable type. A typical 64-bit machine will have variable sizes as such:

| Integer Types | size    |
| ------------- | ------- |
| char          | 8 bits  |
| short int     | 16 bits |
| int           | 32 bits |
| long     int  | 64 bits |

However, these sizes are *architecture-dependent* and can vary from machine to machine. As such, the [C standard library](https://pubs.opengroup.org/onlinepubs/009695399/basedefs/limits.h.html) provides constants which can help define the ranges of each variables.

```c
#include <limits.h> // for INT_MAX, UNIT_MAX
#include <stdio.h>  // for printf()
int main()
{
  printf("%d", INT_MAX); // prints 2147483647
  printf("%d", UINT_MAX); // prints 4294967295
  return 0;
}
```
Additionally, the `sizeof` operator (built in to C) allows us the ability to programmatically obtain the byte size of data.
```c
#include <stdio.h>  // for printf()
int main()
{
  printf("%d", sizeof(int));       // prints 4 (= 32b) on a typical 64-bit machine
  long long_var = 0;
  printf("%d", sizeof(long_var));  // prints 8 (= 64b) on a typical 64-bit machine
  return 0;
}
```

### Integer Casting
In C, like in many other programming languages, we can cast[^cast] variables to another type. In addition, C lets us move a value from an unsigned integer variable to a signed integer variable (and vice versa).
```c
int sx, sy;
unsigned ux, uy;
sx = (int) ux;
uy = (unsigned) sy;
```
When we cast a variable from signed to unsigned (or unsigned to signed), the underlying bit pattern is not changed, but the interpretation of the bit pattern is. This becomes troublesome when a cast results in a interpretation that is not valid. Even if the resulting interpretation is invalid, your program will still cast anyway. This is called **coercion**.
```c
#include <stdio.h>
#include <limits.h>
int main()
{
    int i = -1;
    unsigned u = (unsigned) i;
    printf("i=%d, u=%u\n", i, u);
    return 0;
} // Output: i=-1, u=4294967295
```
Since C ignore the obvious invalid operations this is sometimes referred to as "weak" typing.[^weak-typing]

In addition to the explicit casts (like the one above), we can also *implicitly* cast between variables through assignments and procedure calls:
```c
sx = ux;
uy= sy;
int (fun unsigned u);
uy = fun(sx);
```
By default, integer literals (constants) are considered to be *signed integers*. If we were to explicitly force them to be unsigned, we can suffix a "`U`" or "`u`" to the literal like: `0U`, `4294967259u`.

Lastly, when we mix an unsigned and signed variable in a single expression (including comparison operators), signed values are implicitly cast to unsigned values.












---

[^c-tc] Two's complement is not strictly mandated by the C language. However, most machines use it to store and represent signed integers.

[^cast] Moving values between different type is called **casting**.

[^weak-typing] The strong/weak terminology has had very fragile definitions over the years and are arguably useless in our context. Hence, we will ignore them.
