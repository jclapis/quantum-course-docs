---
hide:
  - toc
---

# Getting Started

## Course Modules

Use the table below to find a course module. If you are not sure whether you have all the needed background knowledge, start with [Complex Numbers](./background-math/complex-numbers.md). To jump right into quantum computing fundamentals, go to [Qubits](./quantum-concepts/qubits.md).

| Background Math | Classical Computing | Qubits and Quantum Gates | Multi-Qubit Systems | Quantum Circuits | Quantum Protocols | Quantum Algorithms | Quantum Error Correction | Execution on Quantum Computers | 
| - | - | - | - | - | - | - | - | - |
| [Complex Numbers](./background-math/complex-numbers.md) | [Digital Information](./classical-computing/digital-information.md) | [Qubits](./quantum-concepts/qubits.md) | [Qubit Registers](./quantum-concepts/qubit-registers.md) | [Complex Superpositions](./quantum-concepts/complex-superpositions.md) | [Quantum Interference](./quantum-concepts/quantum-interference.md) | [Deutsch-Jozsa Algorithm](./quantum-algorithms/deutsch-jozsa-algorithm.md) | [Bit-Flip Error Correction](./error-correction-codes/bit-flip-error-correction.md) | [Intro to Qiskit](./software-tools/intro-qiskit.md) |
| [Vectors](./background-math/vectors.md) | [Endianness](./classical-computing/endianness.md) | [The Bloch Sphere](./quantum-concepts/bloch-sphere.md) | [Multi-Qubit Gates](./quantum-concepts/multi-qubit-gates.md) | [Quantum Circuit Diagrams](./quantum-concepts/quantum-circuit-diagrams.md) | [Superdense Coding](./quantum-algorithms/superdense-coding.md) | [Grover's Algorithm](./quantum-algorithms/grovers-algorithm.md) | [Steane ECC](./error-correction-codes/steane-ecc.md) | [Cloud-Based Machines](./real-execution/cloud-based-machines.md) |
| [Matrices](./background-math/matrices.md) | [Digital Logic](./classical-computing/digital-logic.md) | [Single-Qubit Gates](./quantum-concepts/single-qubit-gates.md) | | [The Quirk Tool](./software-tools/quirk-tool.md) |  | [Simon's Algorithm](./quantum-algorithms/simons-algorithm.md) | | [Resource Estimation and Practicality Assessment](./real-execution/resource-estimation.md) | 
| [Bra-ket and Tensor Notation](./background-math/braket-tensor-notation.md) | [Low-level Programming](./software-development/low-level-programming.md) | [Intro to Q#](./software-tools/intro-qsharp.md) |  | |  | [Quantum Fourier Transform](./quantum-algorithms/qft.md) |  | [Closing Thoughts and Next Steps](./real-execution/whats-next.md) |
| | [High-level Programming](./software-development/high-level-programming.md) | [Lab Tutorial: Single-Qubit Gates](./labs/lab1.md) |  | |  | [Shor's Algorithm](./quantum-algorithms/shors-algorithm.md) |  |
| | [Visual Studio](./software-development/visual-studio.md) | | | | |  |

## Lab Exercises

[Download :material-download:](./exercises.zip){: .md-button .md-button--primary }

## Installation

- Install [Visual Studio Community](https://visualstudio.microsoft.com/vs/community/) with the .NET Core cross-platform development workload enabled

- Install the [Microsoft Quantum Development Kit extension](https://marketplace.visualstudio.com/items?itemName=quantum.DevKit) for Visual Studio

- Click the button above to download the lab exercises and extract the contents of the .zip file

- Open `Intro to Quantum Software Development.sln` in Visual Studio

## Use

Each exercise consists of functions or operations that have not been implemented. The project includes unit tests that validate whether the implementation is correct. Use the [Test Explorer](https://docs.microsoft.com/en-us/visualstudio/test/run-unit-tests-with-test-explorer?view=vs-2019) to see which exercises have been completed successfully. The first time you open the solution, pull up the Test Explorer pane using the toolbar option `Test` > `Test Explorer`, and then click the green `Run All Tests In View` button. After that, you can expand the tree and run tests individually. You can see the output of a selected test by clicking the `Open additional output for this result` link.

See the [Visual Studio](/software-development/visual-studio) module for info on debugging.
