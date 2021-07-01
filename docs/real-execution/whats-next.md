# Closing Thoughts and Next Steps

As software engineers, you might think that our available work in the quantum computing landscape is fairly sparse.
After all, quantum hardware platforms are still heavily under research and development today and certainly can't perform better than classical computers yet.
Aside from assisting with the hardware development, is there anything for us to do until these platforms are ready?

The answer is **yes** - there are a lot of opportunities for software engineers to work on quantum computing in parallel with hardware development!
You've already played with resource estimation and practicality assessments; below are a few more promising activities to get involved in.
Each one could be the subject of its own class, but we've summarized them here.


## Software Framework Development

In this class, we've briefly touched on two prominent software frameworks for working with quantum algorithms - Microsoft's QDK, and IBM's Qiskit.
It turns out that there are many more available out there!

Google maintains one called [Cirq](https://quantumai.google/cirq) that offers similar functionality - build circuits, simulate them, study the results.
However, Cirq provides very fine-grained, low-level control of the machine instructions which makes it quite useful for studying the real execution of quantum circuits on hardware platforms.
It's mainly designed for compatibility with Google's own quantum computer architecture.

A company called Rigetti maintains a large quantum ecosystem called [Forest](https://www.rigetti.com/forest), which comes with a quantum circuit development system called [PyQuil](https://github.com/rigetti/pyquil).
It comes with a lot of the same functionality, including a cloud-based compiler service for situations where running it locally on large circuits is not feasible.
It's designed to run on a variety of backend systems including Rigetti's own machines.

[ProjectQ](https://projectq.ch/) is an interesting research project that came out of [ETH Zurich](https://ethz.ch/en.html), a University in Switzerland.
It actually follows Q#'s style of execute-at-each-statement rather than building up a circuit object and shipping it to a backend like the others do.
That being said, it *does* have a very robust and modular compiler and backend management system that lets it generate circuits for all kinds of quantum hardware.

There's a similar research project called [XACC](https://csmd.ornl.gov/index.php/highlight/xacc-system-level-software-infrastructure-heterogeneous-quantum-classical-computing) out of Oak Ridge National Laboratory.
It provides a more middleware-centric view of things, as it can ingest circuits built from many of the above frameworks, convert them to a common intermediate representation, compile them down to machine-specific instructions, and run them on a wide variety of backend systems (quantum computers).

There are many other projects and tools that we haven't listed here but offer useful functionality to quantum software engineers.
For example, the Quirk tool you've used through the class isn't technically a software framework, but it *is* an extremely useful tool.
The [Quantum Open Source Foundation](https://github.com/qosf/awesome-quantum-software) maintains an *exhaustive* list of such tools and projects if you're curious.

If your passion is tool development, then you may want to consider contributing to one or more of these projects!
Almost all of them are open source on Github, so there's nothing stopping you from diving right in.


## Compiler Research

Compilers (and their relatives *transpilers* and *optimizers*) are classical programs that transform quantum code from one form into another.

Q#'s compiler, as you've seen, turns Q# code into a sequence of instructions that Q#'s simulator can interpret and process.
Microsoft has made [the whole thing open source](https://github.com/microsoft/qsharp-compiler) on Github if you'd like to explore it; the project has over 30 contributors today.

Qiskit actually comes with both a compiler *and* a transpiler, which you can see [in the project's source code](https://github.com/Qiskit/qiskit-terra/tree/master/qiskit).
Together, these tools offer lots of functionality:

- They transform "high-level" quantum circuits (that use arbitrary gates and allow any qubit to interact with any other qubit) into "low-level" circuits that are compatible with a given specific quantum device.
- They handle scheduling to determine *when* to run certain gates, to maximize efficiency and minimize overlap / interference.
- They reorder qubits to minimize the number of SWAP gates required to simulate any-to-any qubit interactions.
- They can **optimize** a circuit by scanning for and removing useless gates and simplifying sequences.

Cirq hosts [a collection of optimizers](https://github.com/quantumlib/Cirq/tree/master/cirq-google/cirq_google/optimizers) that perform similar functionality to Qiskit's transpiler.

PyQuil [comes with a compiler](https://github.com/rigetti/pyquil/blob/master/pyquil/api/_compiler.py) that transcribes things down to the Quil quantum assembly language.

[QCOR](https://github.com/ORNL-QCI/qcor) and [tweedledum](https://github.com/boschmitt/tweedledum) are compiler systems that also transcode and optimize circuits.

If your passion is building tools to help run algorithms faster or bridge circuit-building applications with hardware systems, compiler development might be for you!


## Error Correction and Noise Reduction

As you can imagine, a *massive* amount of work is currently dedicated to minimizing the impact of quantum errors. 
Qiskit actually provides an entire library dedicated to this pursuit called [Ignis](https://github.com/Qiskit/qiskit-ignis).
If you're interested in profiling the noise of a quantum machine and testing an error filter or correction code, it's certainly something you're going to want to look at.

There are [several other projects](https://github.com/qosf/awesome-quantum-software#quantum-error-correction) dedicated to this as well, so if you'd like to work on combatting quantum errors then this field is definitely one that you can contribute to.


## Language Standards

Aside from the tooling and techniques, quantum software relies on standards to unify the software and hardware landscapes.
In particular, the software needs to be able to compile to **a well-known language** that the hardware can ingest and execute, much like the way classical programs are compiled down to machine code today.

There are a few layers of these languages - Q# and Qiskit, which you've played with during this class, are examples of **high-level languages** that can't actually be run by a quantum computer.

At the "middle" level are **intermediate representations**.
These are standards that can be used to describe quantum circuits in a general-purpose, platform-agnostic way.

Microsoft maintains one such standard, called the [Quantum Intermediate Representation (QIR)](https://devblogs.microsoft.com/qsharp/introducing-quantum-intermediate-representation-qir/).
QIR is designed to be compatible with any software framework; Qiskit, Q#, Cirq, or PyQuil could all compile down to QIR, which could then be compiled down to actual machine code for a specific quantum computer.

IBM maintains another, called [OpenQASM](https://en.wikipedia.org/wiki/OpenQASM).
Qiskit actually compiles its circuits to OpenQASM and ships that code to IBM's backend systems when you run on their computers.
It is a very well-established standard.

Rigetti maintains a third, called [Quil](https://en.wikipedia.org/wiki/Quil_(instruction_set_architecture)) which, unsurprisingly, PyQuil compiles down to in order to run on one of Rigetti's machines.
It's a hybrid design that includes support for classical computation as well, which can be helpful in certain situations (such as measure-in-the-middle circuits).
As with the others, it has a very assembly-like feel to it.

If working on universal standards for the entire quantum computing domain as a whole appeals to you, then you might fell right at home pulling down some of these repositories and working on the rules, descriptions, or examples that they provide.


## Closing Thoughts

At this point you have been exposed to a pretty wide spectrum of concepts, algorithms, technologies, and techniques surrounding the quantum computing landscape.

You've learned about the fundamentals - how qubits work, how quantum gates work, how superposition, entanglement, and interference combine to make powerful quantum algorithms, and how to represent quantum programs in Bra-Ket notation and in circuit diagrams.

You've learned about quantum programming using two different software frameworks - QDK and Qiskit.

You've implemented two of the most exciting general-purpose quantum algorithms we know of: Grover's and Shor's algorithms.

You've run code on a real quantum computer and learned about quantum errors and error correction.

You've even learned how to extract useful information about a quantum program and its practicality when run on a quantum computer.

In closing, we both want to thank you for having the courage and curiosity to take this class, and the determination to finish it.
At this point, you have built a firm foundation to pursue a career in quantum software engineering.
You can study ideas, build tools, bridge gaps, and ultimately solve problems that cannot be solved with modern computers today.
We can't wait to see where you go from here!
