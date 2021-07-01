# High-level Programming

## Objective

Appreciate how conventional computers are used to solve problems, and understand the difference between statically and dynamically typed languages.

## High-Level Programming Languages

The label "high-level" when applied to programming languages is somewhat vague, but the general idea is that the language abstracts the nuances of the physical machine and its architecture away from developers.
There are varying levels of high-levelness, depending on the language's features.
Languages like C live on the low-to-medium-level end of the spectrum, because they offer more functionality than assembly but are still very closely tied to the hardware.
On the other hand, languages like Java, Python, C#, and JavaScript live on the high-level end because they operate in completely different paradigms that no longer even resemble the stack-based computation that they perform under the hood.

High-level languages can include features such as:

- Automated memory management with the aid of garbage collection systems
- The concept of "objects" or other entities that contain structured information
- Type systems (static, dynamic, or duck typing) that know what functionality an entity provides and the structure of the data it supports
- Support for defining custom syntax extensions (such as custom operators)
- Abstract data types, such as arrays, maps, lists, and sets that each come with their own rules and capabilities
- Boundary-checking to prevent the system from executing code in memory locations that go beyond an entity's assigned limits
- Support for multiple threads, to run different functionality on different parts of the processor simultaneously
- Interpreted or just-in-time (JIT) execution, which transforms the code into processor-specific machine instructions in real-time, allowing one codebase to be run on any processor and operating system that has a runtime environment built for it

As software engineers, we use languages with these features daily.
Though the tools have changed, our job is still fundamentally the same as it was at the dawn of the classical computer: we write code that expresses some desired functionality in terms that the system can interpret and execute, and all of our data is ultimately represented as binary numbers.
The form of those instructions and data may have changed as computer science has matured, but these underlying truths are still valid.
We can go from object-oriented to aspect-oriented paradigms, from functional to imperative styles, or from strongly-typed languages to duck-typed languages.
At the end of the day, we know that we'll have variables, arrays, functions, comments, and 1 + 1 will always equal 2.
The foundational pillars of classical computers will always be the same, regardless of language.
We want you to appreciate what you take for granted in your daily life as a software engineer.

If you don't have a lot of software experience, it's a good idea to browse the materials below until you feel comfortable answering the knowledge check questions. Basic exposure to Python and C# will be very helpful when exploring some of the quantum software frameworks.

## Additional Materials

- [CrashCourse video on statements & functions](https://youtu.be/l26oaHV7D40)

- [CrashCourse video on algorithms](https://youtu.be/rL8X2mlNHPM)

- [Python Like You Mean It](https://www.pythonlikeyoumeanit.com/)

- [Stack Overflow answer by Prof. Norman Ramsey on what it means for a language to be statically typed](https://stackoverflow.com/a/2696369)

    - This provides a precise definition of "statically typed", and it clears up confusion around some related terms. It is also a great example of how the computer science community deals with messy topics.

- [C# Tutorials by Microsoft](https://docs.microsoft.com/en-us/dotnet/csharp/tutorials/)

    - This page includes links to videos and interactive tutorials. Focus on the “Hello world” tutorial to understand the basic syntax.

- [Doc page on the C# type system](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/)

    - Note the difference between value and reference types.

## Knowledge Check

### Q1

What is the output of the following Python program?

```python linenums="1"
def fibonacci(n):
    if n < 2:
        return n
    else:
        return fibonacci(n-1) + fibonacci(n-2)
print(fibonacci(6))
```

A: `6`

B: `8`

C: Nothing; the program runs in an infinite loop

D: Error due to bad syntax/indentation

E: Error due to no `if __name__ == '__main__'` statement

??? check "Answer"
    B

### Q2

Fill in the missing line of Python code so that the function below computes the mean of a list of numbers.

```python linenums="1"
def mean(num_list):
    total = 0
    for num in num_list:
        # ???
    return total / len(num_list)
```

??? check "Answer"
    `total += num`

### Q3

What is the time complexity of the algorithm implemented in Q2 that computes the mean of a list of numbers? Give your answer in “big O” notation.

??? check "Answer"
    $Ο(n)$

### Q4

Suppose you are asked to guess a number between 1 and 15 (inclusive), and after each guess you are told whether it is higher or lower. How many guesses are required before you are guaranteed to know what the number is?

??? check "Answer"
    3

### Q5

Which of the following is an advantage of *all* statically typed languages? (Select all that apply.)

A: Compiled programs provide some guarantees on type safety

B: Programs produce a runtime error when some type restrictions are violated

C: Any type is easily convertible to any other type

D: A consistent style is enforced, making the code more readable

E: If the program compiles, no logic errors are possible

??? check "Answer"
    A

### Q6

What is the output of the following C# snippet, assuming it is part of an executable program?

```c# linenums="1"
char c = 'c';
int i;
i = (int)c; // cast c to int
System.Console.WriteLine(i);
```

??? check "Answer"
    `99`

### Q7

What is the classification of the type `Employee` as defined below in C#? (Select all that apply.)

```c# linenums="1"
public struct Employee
{
    public string name;
    public int id;

    public Employee(string n, int i)
    {
        name = n;
        id = i;
    }
}
```

A: Value type

B: Reference type

C: Literal value

D: Generic type

E: Anonymous type

??? check "Answer"
    A
