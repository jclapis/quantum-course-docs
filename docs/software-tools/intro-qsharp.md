# Intro to Q&#35;

## The Quantum Development Kit

There are a lot of software frameworks designed to help us write quantum code out there.
I've experimented with many of them, including [Qiskit](https://qiskit.org/), [Cirq](https://github.com/quantumlib/Cirq/), [Forest](https://www.rigetti.com/forest), [ProjectQ](https://github.com/ProjectQ-Framework/ProjectQ), and [XACC](https://github.com/eclipse/xacc).
All of them are frameworks built for classical languages, like Python or C++.
In our opinion, the easiest framework to use (both for learning quantum computing and for actual day-to-day development work) is Microsoft's [Quantum Development Kit](https://docs.microsoft.com/en-us/azure/quantum/install-overview-qdk).
That's what we're going to use in this class.

The Quantum Development Kit has a few important features to note.
First off, it introduces a new language called Q#  (Q-Sharp).
Q# is a programming language specifically designed for quantum computers; it gives us access to special operators and syntax that only make sense in the quantum domain and are hard to implement in conventional languages, but make our lives as developers a lot easier.
Q# is pretty easy to pick up if you're familiar with conventional programming languages, but we'll start with the basics and learn more as we introduce new quantum computing concepts throughout the course.

The second thing the QDK includes is a quantum simulator.
This tool can read our quantum programs and run them on the local, classical computer by simulating the qubits we use and the operations on them.
The local simulator can support up to 30 qubits (which would end up taking $16 \cdot 2^{30}$ bits, or 16 GB, of RAM).
This lets us test our algorithms without needing to have access to an actual quantum computer, all of which are prohibitively expensive and basically reserved for hardware research.

Third, the QDK includes full integration with the Visual Studio and VS Code IDEs.
This includes support for Intellisense (documentation and code completion), syntax highlighting, compiling, debugging, and unit testing.
Conveniently enough, we're going to use all of these things in this class!
A cursory glance through GitHub shows some projects that are building support modules to bring it into other IDEs as well.
QDK's tools are all command-line based, so if you prefer to develop in a different IDE without QDK support, you can still use it - it'll just be a little more manual effort.

Finally, Q# is actually a [.NET](https://dotnet.microsoft.com/learn/dotnet/what-is-dotnet) language.
.NET is an open-source, cross-platform runtime that many different languages can compile to and run on.
This means classical languages like C#, C++, and IronPython can invoke Q# code, and more importantly, Q# can invoke classical code from some (but not all) of .NET's base class libraries.
This is really helpful because the .NET BCL comes with a lot of useful utility functions that save time and effort during development.


## QDK's Reference Documentation

As with all good frameworks, QDK comes with comprehensive online documentation which you can find here:

[https://docs.microsoft.com/en-us/azure/quantum/user-guide/?view=qsharp-preview](https://docs.microsoft.com/en-us/azure/quantum/user-guide/?view=qsharp-preview)

This site contains a complete explanation of all of Q#'s language features, a tutorial of how to use them, and a full set of API references for all of QDK's functions and types.
If you ever forget how a particular feature works or need to find a function for something, this site will be your best friend.
We're going to explain most of the simple things about Q# in this class, but there's way more stuff to Q# and the QDK than we can fit into a two-day course.
If you want to continue exploring the world of quantum computing after we're done here, you can use this site as a good place to start.
I'll also link to some more advanced training and exploration material at the end of the class.


## Opening the Course Solution in Visual Studio

In the class package, there is a file named **Intro to Quantum Software Development.sln**.
Open this, and it should bring up Visual Studio.
If you need a refresher on how to use Visual Studio, take a look at the section in the [Background Refresher](/software-development/visual-studio.md) section.

There are 3 projects in the solution:

- **ConsoleSandbox** is a project you can use for interacting and experimenting with your own quantum code through a terminal / command prompt.
  It's set up to let you add and run whatever classical or quantum code you want.
  You can use this for testing an idea, trying an algorithm on custom inputs, or anything else you'd like to do.
  Anything goes in this project!
- **CSharpExercises** is filled with exercises from the prerequisite sections that test your knowledge of statically-typed languages.
  You can ignore them at this stage of the class.
- **QSharpExercises** is filled with the hands-on labs that we will explore throughout the course.
  Each `.qs` file contains a set of exercises to help you understand an aspect of quantum computing, and give you practice working with it from a software engineering perspective.
  Some of the modules in the class will ask you to complete one of these labs once you've finished reading it.

Once you have the solution open, take a look at the **QSharpReference.qs** file in the **QSharpExercises** project.
The .qs extension is used for Q# files.
This file contains a brief example of the most common things that you'll tend to do in Q#.
You can rely on it for a quick syntax lookup or for the name of some function you forgot; for a more thorough explanation of Q#, you'll want to look at the official reference documentation on the Microsoft website.
For this class, though, this reference will cover everything we need.


## Q# Overview

### Code Structure

Q# is a simple language.
It isn't really object-oriented, at least not in the conventional sense of classical OOP languages.
It leans closer to the functional programming paradigm, though it does blur the lines between the two a bit.
From a classical language perspective, I'd say that Q# is roughly analogous to plain old C.

Q# has the notion of an "object", in the sense that it has variables and a type system.
It is strongly typed, meaning a variable has a well-defined type at the time of its declaration and it can only ever be that type.
Functions expecting arguments of specific types can only be given those specific types.
However, it doesn't have the notion of classes.
Objects in Q# do not have their own properties or instance methods; objects are simply instances of a particular type, and that's all they are.

Everything (and we mean *everything*) in Q# is done through static methods (called **operations** in Q#).
Essentially, when we write Q# code, we're just constructing a bunch of these static operations.
Operations can have as many parameters as you want, and they can be of any type.
They can also return one variable, like in most classical languages.
Operations can contain quantum code, classical code, or both - they're totally interchangeable in Q#.
It doesn't care which paradigm you're using, it lets you construct whatever you want on a line-by-line basis.
You can intersperse quantum and classical code however you see fit.

Q# is a *compiled* language, like other C-style languages.
It's not a scripting language like Python.
The compiler will check syntax and semantic correctness and identify any problems with either one prior to running.
Of course, it can't catch everything - Q# still has runtime errors (like trying to access an invalid index of an array), but the compiler catches a lot of simple mistakes.

This is a simple example of a Q# file:

```
namespace MyQuantumProgram
{
	open Microsoft.Quantum.Intrinsic;
	 
	/// # Summary
	/// Prints a greeting message to the console.
	operation HelloWorld() : Unit
	{
		// Say hello!
		Message("Hello World!");
	}
}
```

There are a few things to note here:

- Everything in Q# is wrapped in a **namespace**.
  This is identical to namespaces in C# and C++, and it's essentially the same thing as a package in Java.
  Python doesn't really have an analog to this, because you can define things in the same namespace across multiple files.
  Namespaces are essentially named scopes; anything defined in a namespace is accessible by anything that references (imports / uses) the namespace.
- Referencing a namespace is done with the **open** keyword, as shown in the "open Microsoft.Quantum.Intrinsic" line.
  This is effectively the same as a "using" statement in C# or C++, or an "import" statement in Java or Python.
  It lets you reference things in other namespaces without having to type the entire namespace in front of the thing.
- Statements are all ended with **semicolons**.
  Sorry Python folks, this is just one of those things you have to get used to in Q#.
- This code defines an **operation** called "HelloWorld".
  It doesn't take any parameters (empty parentheses after the name of the operation), and it doesn't return anything.
  The colon is used to separate the parameters from the return type; whatever comes to the right is the return type.
  In this case, it returns **Unit**.
  Unit in Q# is the same as **void** in C#, C++, and Java, or basically the same as **None** in Python.
- Operation (and namespace) scope is defined by a pair of curly braces, as in other C-style languages.
  Whitespace and indentation doesn't matter.
- Documentation comments (docstrings) are attached to operations, types, variables, and everything else using blocks of comments that start with three forward slashes.
  The official format for doc strings is **Markdown**.
- In-code comments are done with two forward slashes, like most C-style languages.
- The **Message** function is essentially the "print something" function.
  It's analogous to `Console.WriteLine()` in C#, `std::cout << something << std::endl` in C++, `system.out.println()` in Java, and `print()` in Python.

Running this function will simply print "Hello World!" to the program's output, whether that's the console, Visual Studio's debug terminal, or something else.


### Basic Types

[The Q# documentation](https://docs.microsoft.com/en-us/azure/quantum/user-guide/language/typesystem/) covers the included types, but I've summarized the important ones here:

- **Unit** is essentially void, or None. It represents an empty value / lack of a value.
- **Int** is a 64-bit signed integer. Note that this is 64-bit instead of 32-bit; most classical languages would call this a "long".
- **Double** is a 64-bit floating-point number. This is the same as "double" in C-style languages, or "float" in Python.
- **Bool** is a Boolean value, either **true** or **false**.
- **String** is a sequence of Unicode characters. This is like a C# / Java string, or a str in Python.
- **Qubit** is a qubit.
  It doesn't expose any information (it's opaque), but you can act on qubits with quantum gates (defined as operations, like everything else).
- **Result** represents the result of a qubit measurement.
  It's effectively an enum with two possible values: **Zero** which corresponds to the $\ket{0}$ state, and **One** which corresponds to the $\ket{1}$ state. 
- **Range** is analogous to ranges in Python - a range is a sequence of integers with a discrete start, step size, and stop.


### Working with Variables

Q# separates mutable variables (ones you can change after they've been defined) from immutable variables.
You can define a new immutable variable with the **let** keyword:

```
let var1 = 0;
```

The type of the variable will automatically be inferred by the compiler.
In this case, it will be set to an Int.
Since var1 is immutable, it will always have the value 0.
It can't be changed later on.

Mutable variables can be declared with the **mutable** keyword:

```
mutable var2 = "hello world";
```

In this case, `var2` is a String.
It can be changed later on by using the **set** keyword:

```
set var2 = $"var1 = {IntAsString(var1)}";
```

This also shows **string interpolation**, where you can insert code in the middle of a string to get the string value of something.
The **IntAsString** function will convert an Int to a string.
String interpolation is done by putting a$in front of the opening quote.
You can put any code you want to run in a pair of curly braces.
This is the same as string interpolation in C#, or putting an "f" in front of a string in Python. 


### Tuples

Q# has pretty extensive support for tuples (anonymous types that contain multiple different objects).
They get used a lot, especially for pairing values into a single variable or returning multiple things from an operation.
A tuple is defined like this:

```
let someTuple = (1, 2, 3.0);
```

This will create a new tuple of type (Int, Int, Double).
The type is automatically figured out by the compiler.
The tuple can be passed around as this single variable, which can be convenient if you want to pack related things together semantically.

Getting the values out of a tuple can be done by "unpacking" the tuple into individual variables:

```
let (tuple0, tuple1, tuple2) = someTuple;
```

As before, the types of these variables will be figured out automatically.

If you only care about one value, you can ignore the rest by putting an underscore in their place:

```
let (tuple3, _, _) = someTuple;
```

This will pull out the first value and leave the other ones alone.


### Ranges

Ranges are used a lot in Q# for things like picking specific indices of arrays or iterating with for loops.
They are defined like this:

```
let range = 0..3;
```

This can be read as "from 0 to 3".
This will create a range that has the values 0, 1, 2, and 3.
Note that the last element in Q# ranges is *included* in the collection; this is different from ranges in Python, where the last element is excluded.

If not specified, the range will use the default step size of 1.
However, ranges can also be defined with an explicit step size:

```
let rangeWithStep = 0..2..10;
```

In this syntax, the step is the middle term.
This represents a range that has the values 0, 2, 4, 6, 8, and 10.

Ranges can also decrement by specifying a negative number as the step size:

```
let negativeRange = 10..-1..1;
```

This will go from 10 to 1, with a decreasing increment of 1.


### Arrays

Arrays in Q# work (mostly) the same as they do in other languages.
They're defined and indexed with square brackets:

```
mutable intArray = new Int[10];
```

This will define a new mutable array that stores 10 Ints.
Note that arrays in Q# are fixed-length, and they have the same data type for all of the elements; they aren't like Python lists.

Getting the length (size) of an array is done with the **Length** function:

```
let arrayLength = Length(intArray);
```

Getting an element from an array is done with square brackets, as it is in most classical languages:

```
let array3 = intArray[3];
```

This will get the fourth element in the array (arrays are zero-indexed in Q#).

Unfortunately, it's a little weird to *modify* the elements of an array in Q#.
This is because arrays themselves are immutable (even if their elements aren't), so modifying an array means creating a new array, copying the contents over, and modifying the relevant indices during the copy operation.
Modifying elements is done with this syntax:

```
set intArray w/= 3 <- 22;
```

This unusual syntax is called an "apply-and-replace" operator.
It essentially copies the values of intArray into a new array of the same size and type but replaces the element at index 3 with the value 22, then assigns the variable intArray to the new array.
It effectively does the same thing as a statement like `intArray[3] = 22;`, just with a bunch of copying under the hood.
In fact, that more traditional syntax used to be included in an earlier version of Q#, but they got rid of it to enforce the fact that arrays are immutable.

Instead of creating a new array with a specific length and updating it like this during a for loop, it's often easier to just append elements to the list.
Appending elements to an array can be done like this:

```
set intArray += [8];
```

This will grow the array by 1 element, and "8" as the element at the end.
Arrays of any size can be concatenated together like this, they don't have to be done element-by-element.

There are a few other things you can do with arrays in Q# (like getting subsets).
All of these are shown in the QSharpReference file.


### Control Flow

Q# supports three main ways of controlling code: if statements, for loops, and repeat-until loops (which is kind of like the inverse of a do-while loop).
Let's go over the first two, since they're the most common.

If statements are done the same way that they are in the other C-style languages:

```
if someBool
{
	// Do something
}
elif someOtherBool
{
	// Do something else
}
else
{
	// Do a third thing
}
```

`elif` is the same as `else if` in other languages. 

For loops are a bit different.
Q# doesn't have a C-style for loop; instead, it has what we would consider a "for each" loop, or an enumerate loop.
It can iterate over all of the items in a collection like this:

```
for i in intArray
{
	// Do something with i
}
```
	
This can be done with ranges as well, which emulate the behavior of a traditional C-style for loop:

```
let length = Length(intArray);
for i in 0..length - 1
{
	// Do something with i
}
```
	
Remember that the end value of a range is included in the range, so if you're going to iterate over each index of an array, you have to end it at the length minus 1 or it will go out of bounds.


### Single Qubit Gates

Quantum gates in Q# are implemented as operations that take in one qubit as an argument (and potentially some other arguments, depending on the gate).
For example, if you have a qubit named "qubit", the X operation will apply the X gate to the qubit:

```
X(qubit);
```

The $R_x$ gate, which does an arbitrary rotation around the X axis, is defined as the `Rx` function which also takes an angle of rotation:

```
Rx(PI(), qubit);
```

(Note that the PI() function is just used to get the value of $\pi$.)

Measuring a qubit is done with the `M` operation:

```
let measurement = M(qubit);
```

This will return a `Result` object, which will either have the value **Zero** or **One**.


### Allocating Qubits

Q# has a really nice qubit allocation system.
You don't have to figure out which qubits are reserved for which use cases or keep track of how many you've used so far; it does all of that for you.
If you want a qubit, use the **use** statement:

```
use(qubit = Qubit())
{
	// Do something with the qubit
	 
	Reset(qubit);
}
```

The qubit will exist as long as it's in the using statement's scope.
This means you can call operations in the middle of the using block, and pass the qubit to those operations without it being destroyed.
Qubits are always in the $\ket{0}$ state when they're allocated, and they **must be put back in the $\ket{0}$ state before they go out of scope**.
This is very important!
You can put them back in the $\ket{0}$ state by reversing all of the operations you've done to it, or by calling the `Reset` function (which will measure the qubit, and if it's $\ket{1}$, apply the X gate to it). 


## Lab 1
That's a pretty quick summary of Q#, but as you can see, it's fairly similar to most classical languages.
We'll get into some of the more advanced stuff as we go throughout the course, but you know enough to tackle a few simple tasks.
Go onto the next page and you'll start writing Q# code in the first hands-on exercise lab!