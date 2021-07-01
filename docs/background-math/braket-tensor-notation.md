# Bra-ket and Tensor Notation

## Objective

Get acquainted with some of the mathematical notation that arises in quantum information science.

## Ket (Dirac) Notation

In quantum computing, we're going to refer to column vectors with a special notation that makes it a lot easier to keep track of things.
I'll elaborate on how this notation works as we go in the actual class, but for now, here are the basics.

A column vector is written as what's called a **ket**, which has a straight line on the left, and an angle bracket on the right:

$$
\ket{x} = \begin{bmatrix} 1 \\ 2 \\ 3 \\ 4 \end{bmatrix}
$$

When talking about a vector $\ket{x}$, we usually refer to each individual element as $x_i$ where $i$ represents the index of the element.
$i$ can be zero-indexed or one-indexed, but you have to specify which one it is.
For example, here's how we would write the general form of a zero-indexed vector with length $n$:

$$
\ket{x} = \begin{bmatrix} x_0 \\ x_1 \\ ... \\ x_{n-1} \end{bmatrix}
$$

This looks just like the way we'd iterate through each element of an array with a for loop, so you should feel right at home with this notation.

## Tensor Product

### Vectors

Quantum mechanics uses a special kind of vector multiplication that you will see used all over the place.
This is called the **tensor product**.
It is symbolized by a circle with an X in the middle: $\otimes$.
When you tensor two vectors together, you take the entire right-hand vector and multiply it by each of the elements in the left-hand vector.
Those entire multiplied vectors then become the elements of the new output vector.
This is easiest to see with an example:

$$
\displaylines{
\ket{x} \otimes \ket{y} = \begin{bmatrix} x_0 \\ x_1 \end{bmatrix} \otimes \begin{bmatrix} y_0 \\ y_1 \end{bmatrix} =
\begin{bmatrix} x_0 \cdot \begin{bmatrix} y_0 \\ y_1 \end{bmatrix} \\ x_1 \cdot \begin{bmatrix} y_0 \\ y_1 \end{bmatrix} \end{bmatrix} =
\begin{bmatrix} x_0 \cdot y_0 \\ x_0 \cdot y_1 \\ x_1 \cdot y_0 \\ x_1 \cdot y_1 \end{bmatrix} \\~\\
\begin{bmatrix} 1 \\ 2 \end{bmatrix} \otimes \begin{bmatrix} 3 \\ 4 \\ 5 \end{bmatrix} =
\begin{bmatrix} 1 \cdot \begin{bmatrix} 3 \\ 4 \\ 5 \end{bmatrix} \\ 2 \cdot \begin{bmatrix} 3 \\ 4 \\ 5 \end{bmatrix} \end{bmatrix} =
\begin{bmatrix} 3 \\ 4 \\ 5 \\ 6 \\ 8 \\ 10 \end{bmatrix}
}
$$

Notice that the new vector isn't the same size as the original ones - it's the length of the first one times the length of the second one.
Also notice that the two original vectors don't have to be the same length, like they did in the other operations.

When there are multiple tensor products together, the order of operations doesn't matter as long as you follow the above pattern.
For example, if we had 3 kets tensored together, we could either evaluate the first pair or the second pair - the end result will be the same, which is this monstrosity:

$$
\displaylines{
\ket{x} \otimes \ket{y} \otimes \ket{z} = \begin{bmatrix} x_0 \\ x_1 \end{bmatrix} \otimes \begin{bmatrix} y_0 \\ y_1 \end{bmatrix} \otimes \begin{bmatrix} z_0 \\ z_1 \end{bmatrix} =
\begin{bmatrix} x_0 \\ x_1 \end{bmatrix} \otimes \begin{bmatrix} y_0 \cdot \begin{bmatrix} z_0 \\ z_1 \end{bmatrix} \\ y_1 \cdot \begin{bmatrix} z_0 \\ z_1 \end{bmatrix} \end{bmatrix} =
\begin{bmatrix} x_0 \\ x_1 \end{bmatrix} \otimes \begin{bmatrix} y_0 \cdot z_0 \\ y_0 \cdot z_1 \\ y_1 \cdot z_0 \\ y_1 \cdot z_1 \end{bmatrix}
\\~\\
= \begin{bmatrix} x_0 \cdot \begin{bmatrix} y_0 \cdot z_0 \\ y_0 \cdot z_1 \\ y_1 \cdot z_0 \\ y_1 \cdot z_1 \end{bmatrix} \\ x_1 \cdot \begin{bmatrix} y_0 \cdot z_0 \\ y_0 \cdot z_1 \\ y_1 \cdot z_0 \\ y_1 \cdot z_1 \end{bmatrix} \end{bmatrix}
= \begin{bmatrix} x_0 \cdot y_0 \cdot z_0 \\ x_0 \cdot y_0 \cdot z_1 \\ x_0 \cdot y_1 \cdot z_0 \\ x_0 \cdot y_1 \cdot z_1 \\ x_1 \cdot y_0 \cdot z_0 \\ x_1 \cdot y_0 \cdot z_1 \\ x_1 \cdot y_1 \cdot z_0 \\ x_1 \cdot y_1 \cdot z_1 \end{bmatrix}
}
$$

As you can imagine, this can become impossible to keep track of very quickly.
Luckily, ket notation is specifically built to deal with tensors.
There are four equivalent ways to write this tensor product:

$$
\ket{x} \otimes \ket{y} \otimes \ket{z} = \ket{x}\ket{y}\ket{z} = \ket{x,y,z} = \ket{xyz}
$$

The last form (with all of the variables contained in the ket) is by far the most common, and certainly the most convenient.
Occasionally you will also see the third form with commas appear - this is quite handy when the elements themselves are composites, but you want to semantically separate them.
For example:

$$
\displaylines{
\ket{a} = \ket{xyz}
\\~\\
\ket{b} = \ket{uvw}
\\~\\
\ket{a} \otimes \ket{b} = \ket{xyz,uvw}
}
$$

The comma form lets you present the fact that you want to keep the terms split apart (perhaps because in your program, they represent different arrays even though the tensor will produce a new array that's a combination of them all).
Whatever form you choose, all of them mean the same thing.

### Matrices

Like vectors, matrices can also use the tensor product.
The rules for matrix tensoring are the same as vector tensoring: take the entire right-hand matrix and multiply it by each element of the left-hand matrix.
The result will be a new matrix with a width of the left-hand matrix's width times the right-hand width, and a height of the left-hand's height times the right-hand's height:

$$
\displaylines{
A \otimes B = \begin{bmatrix} A_{00} & A_{01} \\ A_{10} & A_{11} \end{bmatrix} \otimes \begin{bmatrix} B_{00} & B_{01} \\ B_{10} & B_{11} \end{bmatrix} =
\begin{bmatrix} A_{00} \cdot \begin{bmatrix} B_{00} & B_{01} \\ B_{10} & B_{11} \end{bmatrix} & A_{01} \cdot \begin{bmatrix} B_{00} & B_{01} \\ B_{10} & B_{11} \end{bmatrix} \\ A_{10} \cdot \begin{bmatrix} B_{00} & B_{01} \\ B_{10} & B_{11} \end{bmatrix} & A_{11} \cdot \begin{bmatrix} B_{00} & B_{01} \\ B_{10} & B_{11} \end{bmatrix} \end{bmatrix}
\\~\\
= \begin{bmatrix}
A_{00} \cdot B_{00} & A_{00} \cdot B_{01} & A_{01} \cdot B_{00} & A_{01} \cdot B_{01} \\
A_{00} \cdot B_{10} & A_{00} \cdot B_{11} & A_{01} \cdot B_{10} & A_{01} \cdot B_{11} \\
A_{10} \cdot B_{00} & A_{10} \cdot B_{01} & A_{11} \cdot B_{00} & A_{11} \cdot B_{01} \\
A_{10} \cdot B_{10} & A_{10} \cdot B_{11} & A_{11} \cdot B_{10} & A_{11} \cdot B_{11}
\end{bmatrix}
}
$$

Matrix tensors can get very complicated very quickly, so we usually just represent them by combining the names of their components, like we do with vectors:

$$
A \otimes B \otimes C = ABC
$$

## Additional Materials

- [Math is Fun page on Bra-Ket notation](https://www.mathsisfun.com/physics/bra-ket-notation.html)

    - This page includes a preview into some concepts of quantum mechanics.

- [Dan Fleisch video on tensors](https://youtu.be/f5liqUk0ZTw)

    - This video does not go into the math, but it offers a great explanation of tensors.

- [Wikipedia article on Kronecker product](https://en.wikipedia.org/wiki/Kronecker_product)

    - In the context of quantum information science, the $\otimes$ symbol or "tensor product" is computed with the Kronecker product.

## Knowledge Check

### Q1

Let $\ket{x} = \begin{bmatrix} x_0 \\ x_1 \end{bmatrix}, \: \ket{y} = \begin{bmatrix} y_0 \\ y_1 \end{bmatrix}$. Which of the following expressions represent the tensor product of $\ket{x}$ and $\ket{y}$? (Select all that apply.)

A: $\ket{x} \otimes \ket{y}$

B: $\ket{y} \otimes \ket{x}$

C: $\ket{x, y}$

D: $\begin{bmatrix} x_0 \\ x_1 \end{bmatrix} \otimes \begin{bmatrix} y_0 \\ y_1 \end{bmatrix}$

E: $\begin{bmatrix} x_0 \cdot y_0 \\ x_0 \cdot y_1 \\ x_1 \cdot y_0 \\ x_1 \cdot y_1 \end{bmatrix}$

??? check "Answer"
    A, C, D, E

### Q2

$$
\begin{bmatrix} 1 \\ 0 \end{bmatrix} \otimes \begin{bmatrix} 0 \\ 1 \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} 0 \\ 1 \\ 0 \\ 0 \end{bmatrix}$

### Q3

$$
\begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} \otimes \begin{bmatrix} \frac{1}{\sqrt{2}} \\ \frac{1}{\sqrt{2}} \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} \frac{1}{2} \\ \frac{1}{2} \\ \frac{1}{2} \\ \frac{1}{2} \end{bmatrix}$

### Q4

If $\ket{x} \otimes \begin{bmatrix} \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ \frac{1}{\sqrt{2}} \\ -\frac{1}{\sqrt{2}} \end{bmatrix}$, what is $\ket{x}$?

??? check "Answer"
    $\begin{bmatrix} 0 \\ 1 \end{bmatrix}$

### Q5

$$
\begin{bmatrix} 1 & 2 \\ 0 & -1 \end{bmatrix} \otimes \begin{bmatrix} i & 10 \\ 5 & 4 \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} i & 10 & 2i & 20 \\ 5 & 4 & 10 & 8 \\ 0 & 0 & -i & -10 \\ 0 & 0 & -5 & -4 \end{bmatrix}$

### Q6

What is the element at the 3^rd row and 6^th column of the resultant matrix of the following tensor product?

$$
\begin{bmatrix} a & b \\ c & d \\ e & f \end{bmatrix} \otimes \begin{bmatrix} 1 & 2 & 3 \\ 4 & 5 & 6 \\ 7 & 8 & 9 \end{bmatrix}
$$

??? check "Answer"
    $9b$
