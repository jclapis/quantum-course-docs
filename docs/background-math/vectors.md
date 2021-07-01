# Vectors

## Objective

Get familiar with vectors and basic vector operations.

## Vector Notation

In software development, we use arrays all the time.
An array is simply a fixed-length collection of elements that have the same type, most often represented as one contiguous chunk of memory.
Arrays are usually written with square brackets, like this array of ints:

```csharp
int[] array = new int[4];
```

The notation varies between languages, but this syntax should look pretty familiar.

A **vector**, in the linear algebra sense, is like an array of numbers.
The numbers aren't integers, or floats, or doubles, they're just… numbers in the purest abstract sense.
They can be real, imaginary, or complex.
Like arrays, they're also written with square brackets.
Unlike arrays, vectors have one extra property: they have a direction.
More specifically, they can either be horizontal (called a **row vector**) or vertical (called a **column vector**).
The standard notation for vectors looks like this:

$$
\text{Column Vector:}\: \begin{bmatrix} 2 \\ 3 + 4i \\ 3.14159 \\ \sqrt{5} / 28 \end{bmatrix} \qquad \text{Row Vector:}\: \begin{bmatrix} 1 & -1 & 42 + 8i & 630.4 \end{bmatrix}
$$

Each of these vectors has length 4, because they have 4 elements.
When writing vectors, the kind of number you use doesn't matter (but generally, you want to represent them as exactly as you can instead of approximating).
We will be using **column vectors** about 99% of the time in our quantum software work.
We won't really need row vectors.

For convenience, in your code comments, you can usually just represent vectors in standard array notation.
For example, you could write:

```csharp
// This vector will be [0, 2, 3.14159, √5/28]
```

Everyone will assume you're talking about a column vector (in this case, the same as the one in the example above) unless you specifically say that it's a row vector.


## Magnitude and Unit Vectors

The **magnitude** of a vector is like the magnitude of a complex number: it's the square root of the sum of all of the terms' magnitudes squared.
Also like complex numbers, vector magnitude is represented with vertical bars:

$$
\left| \begin{bmatrix} x_0 \\ x_1 \\ \vdots \\ x_{n-1} \end{bmatrix} \right| = \sqrt{\lvert x_0 \rvert^2 + \lvert x_1 \rvert^2 + \dots + \lvert x_{n-1} \rvert^2}
$$

For real numbers, the magnitude of a number is just the absolute value of the number itself.
For complex numbers, recall from [the previous page on complex numbers](/background-math/complex-numbers) that the magnitude is the square root of the sum of the real and imaginary coefficients squared (go back and look at it if you need to see the formula).

If the magnitude of a vector is 1, then it is called a **unit vector**.
This will be important, because quantum computing *exclusively* uses unit vectors.


## Math Properties

### Addition

To add two vectors together, they have to be the same length and the same type (column and column, or row and row).
Just add each element to its partner:

$$
\begin{bmatrix} x_0 \\ x_1 \\ x_2 \\ x_3 \end{bmatrix} +
\begin{bmatrix} y_0 \\ y_1 \\ y_2 \\ y_3 \end{bmatrix} =
\begin{bmatrix} x_0 + y_0 \\ x_1 + y_1 \\ x_2 + y_2 \\ x_3 + y_3 \end{bmatrix}, \qquad
\begin{bmatrix} 1 \\ 2 \\ 3 \\ 4 \end{bmatrix} +
\begin{bmatrix} 5 \\ 6 \\ 7 \\ 8 \end{bmatrix} =
\begin{bmatrix} 6 \\ 8 \\ 10 \\ 12 \end{bmatrix}
$$


### Scalar Multiplication

To multiply a vector by a constant factor, just multiply each element by it.

$$
c \cdot \begin{bmatrix} x_0 \\ x_1 \\ x_2 \\ x_3 \end{bmatrix} =
\begin{bmatrix} c \cdot x_0 \\ c \cdot x_1 \\ c \cdot x_2 \\ c \cdot x_3 \end{bmatrix}, \qquad
3 \cdot \begin{bmatrix} 1 \\ 2 \\ 3 \\ 4 \end{bmatrix} =
\begin{bmatrix} 3 \\ 6 \\ 9 \\ 12 \end{bmatrix}
$$


## Additional Materials

- [Khan Academy lesson on vectors in the context of linear algebra](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/vectors/v/vector-introduction-linear-algebra)

    - All the videos and exercises are relevant except parametric representations of lines.

- [3Blue1Brown video on vectors](https://youtu.be/fNk_zzaMoSs)

## Knowledge Check

### Q1

$$
\begin{bmatrix} 3 \\ 2 \end{bmatrix} + \begin{bmatrix} -1 \\ 5 \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} 2 \\ 7 \end{bmatrix}$

### Q2

$$
\begin{bmatrix} 1 \\ 0 \\ a \\ 2+2i \end{bmatrix} + \begin{bmatrix} -1 \\ 4 \\ b \\ -2+i \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} 0 \\ 4 \\ a+b \\ 3i \end{bmatrix}$

### Q3

$$
5 \cdot \begin{bmatrix} 4 \\ 0 \\ 1 \end{bmatrix} = \; ?
$$

??? check "Answer"
    $\begin{bmatrix} 20 \\ 0 \\ 5 \end{bmatrix}$

### Q4

What is the speed of an object whose velocity vector is given as $\begin{bmatrix} v_x \\ v_y \end{bmatrix} = \begin{bmatrix} 12 \\ 5 \end{bmatrix}$

??? check "Answer"
    $13$

### Q5

$$
\left| \begin{bmatrix} 3 \\ -6 \\ 2 \end{bmatrix} \right| = \; ?
$$

??? check "Answer"
    $7$

### Q6

Which of the following is a unit vector? (Select all that apply.)

A: $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$

B: $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$

C: $\begin{bmatrix} \frac{\sqrt{3}}{2} \\ \frac{-1}{2} \end{bmatrix}$

D: $\begin{bmatrix} 0 \\ 0 \\ i \end{bmatrix}$

E: $\begin{bmatrix} \frac{1}{\sqrt{3}} \\ \frac{1}{\sqrt{3}} \\ \frac{1}{\sqrt{3}} \end{bmatrix}$

??? check "Answer"
    A, C, D, E

### Q7

What is the unit vector that points in the same direction as $\begin{bmatrix} -4 \\ 3 \end{bmatrix}$?

??? check "Answer"
    $\begin{bmatrix} -\frac{4}{5} \\ \frac{3}{5} \end{bmatrix}$
