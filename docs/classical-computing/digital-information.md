# Digital Information

## Objective

Understand how information is represented in a digital computer and practice working with binary numbers.

## Classical Computers

"Classical" computers refer to the conventional, electronic machines that we use in everyday life today.
Your laptop, your phone, and your smartwatch all qualify as classical computers.
These modern marvels are exceptional at solving problems of this nature:

> Given some function $f$, and some input value $x$, what is $f(x)$?

In other words, they are exceptional at *computing function outputs*.
This should come as no surprise, given the name "computer".
To accomplish this task, the function $f$ and the input value $x$ both need to be represented in some format that the computer can interpret and process.
There are a lot of different ways to accomplish this, but through our scientific experimentation and engineering, we as a society have collectively settled on the following general conventions for most classical computers:

- Values are represented in **binary (base-2)**, where the fundamental unit (each digit of a number) is referred to as a "bit".
- Functions are represented as sequences of binary arithmetic operations.

The exact implementations of these principles vary from device to device.
For example, bits can be represented as voltage levels in a cable, or electric charge polarity in a flash memory cell, or magnetic field orientation in a hard drive platter.
Similarly, the specific binary arithmetic operations that comprise a function can vary from processor to processor, based on its supported instruction set (like MIPS, ARM, or x64).
Whatever the particulars are, the important thing is that these two ideas are the fundamental concepts that classical computers are built upon.

To explain how quantum computers work and why they're so powerful, we want to spend a little more time talking about classical bits and machine instructions first.
This is a very brief refresher on the lowest level of how classical computers operate.
In the next page, we'll go over how this relates to modern software engineering tools and practices.

???+ note
    Diving deep into the weeds of computer science may seem like it is an unnecessarily low-level explanation, but we assure you, it's worth your time to refresh on these concepts.
    The reason we bring them up is because we, as classical software engineers, take a lot of this stuff for granted.
    Decades of research and iteration have given us high-level programming languages that completely abstract how classical computers work under the hood, but the quantum world doesn't have this legacy to build upon.
    There is no high-level language for quantum computers yet, at least not in the sense that the hardware details are abstracted away.
    In the quantum world we have to deal with individual bits, bit registers, logic gates, explicit memory management, and functions as sequences of explicit bitwise instructions.
    A good knowledge of how classical computers handle these things will go a long way to helping you understand quantum software development.

## Binary Numbers

In binary, there are only two valid values for a digit: 0 and 1.
We call each digit of a binary number a **bit**.
Just like how decimal numbers are simply strings of digits that can be any number from 0 to 9, binary numbers are just strings of 0s and 1s.
However, instead of each digit representing a power of 10, bits represent powers of 2.
Any whole number can be expressed as a sum of powers of 2, so we can write it in binary.
For example, consider the number 44:

$$
\begin{aligned}
44 &= 32 + 8 + 4
\\~\\
&= 2^5 + 2^3 + 2^2
\\~\\
&= 1 \cdot 2^5 + 0 \cdot 2^4 + 1 \cdot 2^3 + 1 \cdot 2^2 + 0 \cdot 2^1 + 0 \cdot 2^0
\end{aligned}
$$

Using the coefficients in front of each term, we can write the binary form of 44:

$$
44_d = 101100_b
$$

Here, the subscript $d$ means the number is in decimal, and the subscript $b$ means that it's in binary.
This kind of notation isn't really a standard convention - the base of the number you're looking at is usually defined by its context.
For this section, though, I'll use it so you can tell which base a number is in.

## Additional Materials

- [Khan Academy unit on digital information](https://www.khanacademy.org/computing/computers-and-internet/xcae6f4a7ff015e7d:digital-information)

    - Bits and bytes
    - Binary numbers
    - Hexadecimal numbers
    - Storing text in binary

- [Basics Explained video on binary](https://youtu.be/Xpk67YzOn5w)

- [TED-Ed video on binary](https://youtu.be/wgbV6DLVezo)

- [ASCII table](http://www.asciitable.com/)

    - This provides an example of how information is digitally encoded.

## Knowledge Check

### Q1

What is $6$ in binary (base two)?

??? check "Answer"
    $110_2$

### Q2

What is $10000_2$ in decimal (base ten)?

??? check "Answer"
    $16$

### Q3

$$
1010_2 + 111_2 = \; ?
$$

??? check "Answer"
    $10001_2$

### Q4

What is $18$ in hexadecimal (base sixteen)?

??? check "Answer"
    $12_{16}$

### Q5

What is $FF_{16}$ (a.k.a. 0xFF) in decimal?

??? check "Answer"
    $255$

### Q6

What is $1001 0110_2$ in hexadecimal?

??? check "Answer"
    $96_{16}$

### Q7

What word is ASCII encoded as 0x7175616E74756D ?

??? check "Answer"
    quantum
