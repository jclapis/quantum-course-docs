# Endianness

## Objective

Practice working with both big- and little-endian bit and byte ordering.

## Big-Endian and Little-Endian Notation

In decimal (base-10) systems, each digit of a number can have 10 possible values: 0, 1, 2, 3, 4, 5, 6, 7, 8, or 9.
The placement of the digit corresponds to which power of 10 it represents.
The number 891, for example, is really just an easy way to represent this addition of powers of 10:

$$
\begin{aligned}
891 &= 800 + 90 + 1
\\~\\
&= 8 \cdot 10^2 + 9 \cdot 10^1 + 1 \cdot 10^0
\end{aligned}
$$

This particular notation, where the largest power of 10 is the left-most digit, is called **big-endian notation**.
This is the way that we think of numbers in everyday life.
The opposite convention, where the left-most digit is the smallest power of 10, is called **little-endian notation**.
In little-endian notation, the number eight-hundred ninety-one would be written as 198.
As a more general formula for little-endian numbers:

$$
x = x_0 \cdot 10^0 + x_1 \cdot 10^1 + x_2 \cdot 10^2 + ...
$$

where the coefficient $x_i$ means the $i$-th digit from the left (so $x_0$ is the first digit, $x_1$ is the second digit, and so on).
This may seem bizarre, but it's actually the way many computers keep track of values in memory.
Which one you use depends on what you're doing.
Knowing the difference between them, and recognizing numbers in either format, is going to be helpful when working with quantum algorithms.
Many algorithms are defined in academic papers, and some authors prefer one format over the other, so you'll end up working with both fairly often.

## Bitwise vs Bytewise Endianness

The above description of endianness can be applied directly to binary numbers and data. In bitwise big-endian notation, the leftmost bit is the **most significant bit**. In bitwise little-endian notation, the leftmost bit is the **least significant bit**.

However, conventional computers group data by bytes (8 bits). So if computer is said to have a *little-endian architecture*, that is usually referring to the byte ordering rather than the bit ordering. For bytewise little-endian data, the leftmost byte is the **least significant byte**. For example, the data `0x12345678` would be stored as `0x78563412` in little-endian byte ordering.

## Additional Materials

- [Computerphile video on endianness](https://youtu.be/NcaiHcBvDR4)

- [Jacob Schrum video on bit and byte ordering](https://youtu.be/rJf5qkwkMY4)

- [Wikipedia article on endianness](https://en.wikipedia.org/wiki/Endianness)

    - Focus on the "Byte addressing" and "Bit endianness" sections.

## Knowledge Check

### Q1

What is the little-endian bit ordering of the big-endian data, `10010111`?

??? check "Answer"
    `11101001`

### Q2

What is the decimal value of the bitwise little-endian data, `1010`?

??? check "Answer"
    $5$

### Q3

What is the little-endian byte ordering of the big-endian data, `0xBEEF`?

??? check "Answer"
    `0xEFBE`

### Q4

What is the decimal value of the bytewise little-endian data, `0x2800`?

??? check "Answer"
    $40$

### Q5

(Hard) Convert the big-endian data 0x1234 to little-endian byte ordering, with the bits in each byte ordered in little endian. Give your answer in hexadecimal.

??? check "Answer"
    `0x2C48`
