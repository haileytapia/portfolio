---
layout: default
title: Create your first Q# program
parent: Microsoft
nav_order: 3
permalink: /microsoft/qsharp-quickstart
---

# Quickstart: Create your first Q# program
{: .no_toc }

August 5, 2024 ∙ [Original document](https://learn.microsoft.com/en-us/azure/quantum/qsharp-quickstart)
{: .fs-5 : .fw-300 }

Learn how to write a basic Q# program that demonstrates entanglement, a key concept of quantum computing.

When two or more [qubits](https://learn.microsoft.com/en-us/azure/quantum/concepts-the-qubit) are entangled, they share quantum information, meaning whatever happens to one qubit also happens to the other. This quickstart focuses on a two-qubit entangled state called a Bell pair. In a Bell pair, if you measure one qubit in the ∣0⟩ state, you know the other qubit is also in the ∣0⟩ state without measuring it. For more information, see [Quantum entanglement](https://learn.microsoft.com/en-us/azure/quantum/concepts-entanglement).

In this quickstart, you:

✔ Create a Q# file. <br>
✔ Allocate a pair of qubits. <br>
✔ Entangle the qubits.

## Prerequisites

- The latest version of [Visual Studio Code](https://code.visualstudio.com/download).
- The [Azure Quantum Development Kit (QDK) extension](https://marketplace.visualstudio.com/items?itemName=quantum.qsharp-lang-vscode). For installation details, see [Set up the QDK](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk).

## Create a Q# file

1. Open Visual Studio Code.
2. Select **File** > **New Text File**.
3. Save the file as `Entanglement.qs`. The .qs extension denotes a Q# program.

## Write your Q# code

In your `Entanglement.qs` file, follow these steps to entangle and measure a pair of qubits.

### Define a namespace

Each Q# program starts with a user-defined namespace, which helps you organize related functionality. For this quickstart, your namespace is `BellPair`:

```qsharp
namespace BellPair {
    // Your code goes here.
}
```

### Open a quantum library

The QDK includes the Q# standard library with predefined functions and operations for your quantum programs. To use them, you must first open the relevant library.

In your `BellPair` namespace, use an `open` statement to import the `Microsoft.Quantum.Diagnostics` library. This gives you access to all its functions and operations, including `DumpMachine()`, which you later use to display the entangled state.

```qsharp
    open Microsoft.Quantum.Diagnostics;
```

### Define an operation

After opening the relevant libraries, define your quantum operation and its input and output values. For this quickstart, your operation is `EntangleQubits`. This is where you'll write the remaining Q# code to allocate, manipulate, and measure two qubits.

`EntangleQubits` takes no parameters and returns two Result values, Zero or One, which represent the results of the qubit measurements:

```qsharp
    operation EntangleQubits() : (Result, Result) {
        // Your entanglement code goes here.
}
```

### Allocate two qubits

The `EntangleQubits` operation is currently empty, so the next step is to allocate two qubits, `q1` and `q2`. In Q#, you allocate qubits using the `use` keyword:

```qsharp
        // Allocate two qubits, q1 and q2, in the 0 state.
        use (q1, q2) = (Qubit(), Qubit());
```

{: .note }
> In Q#, qubits are always allocated in the ∣0⟩ state.

### Put one qubit into superposition

The qubits `q1` and `q2` are in the ∣0⟩ state. To prepare the qubits for entanglement, you must put one of them into an even superposition, where it has a 50% chance of being measured as ∣0⟩ or ∣1⟩.

You put a qubit into superposition by applying the Hadamard, `H`, operation:

```qsharp
        // Put q1 into an even superposition.
        H(q1);
```

The resulting state of q1 is <img src="https://latex.codecogs.com/svg.image?\frac{1}{\sqrt{2}}" alt="One over the square root of two." width="15"/>(∣0⟩ + ∣1⟩), which is an even superposition of ∣0⟩ and ∣1⟩.

### Entangle the qubits

You're now ready to entangle the qubits using the controlled-NOT, `CNOT`, operation. `CNOT` is a control operation that takes two qubits, one acting as the control and the other as the target.

For this quickstart, you set `q1` as the control qubit and `q2` as the target qubit. This means CNOT flips the state of `q2` when the state of `q1` is ∣1⟩.

```qsharp
        // Entangle q1 and q2, making q2 depend on q1.
        CNOT(q1, q2);
```

The resulting state of both qubits is the Bell pair <img src="https://latex.codecogs.com/svg.image?\frac{1}{\sqrt{2}}" alt="One over the square root of two." width="15"/>(∣00⟩ + ∣11⟩).

{: .tip }
> To learn how the Hadamard and CNOT operations transform the state of the qubits, see [Creating entanglement with quantum operations](https://learn.microsoft.com/en-us/azure/quantum/concepts-entanglement#creating-entanglement-with-quantum-operations).

### Display the entangled state

Before measuring the qubits, it's important to verify that your previous code successfully entangles them. You can use the `DumpMachine` operation, which is part of the `Microsoft.Quantum.Diagnostics` library, to output the current state of your Q# program:

```qsharp
        // Show the entangled state of the qubits.
        DumpMachine();
```

### Measure the qubits

Now that you've verified the qubits are entangled, use the `M` operation to measure them. Measuring `q1` and `q2` collapses their quantum states into `Zero` or `One` with even probability.

In Q#, you use the `let` keyword to declare a new variable. To store the measurement results of `q1` and `q2`, declare the variables `m1` and `m2`, respectively:

```qsharp
        // Measure q1 and q2 and store the results in m1 and m2.
        let (m1, m2) = (M(q1), M(q2));
```

### Reset the qubits

Before being released at the end of each Q# program, qubits must be in the ∣0⟩ state. You do this using the `Reset` operation:

```qsharp
        // Reset q1 and q2 to the 0 state.
        Reset(q1);
        Reset(q2);
```

### Return the measurement results

Finally, to complete the `EntangleQubits` operation and observe the entangled state, return the measurement results of `m1` and `m2`:

```qsharp
        // Return the measurement results.
        return (m1, m2);
```

{: .tip }
> To learn more about a Q# function or operation, hover over it.
> 
> ![Screenshot of the details that appear when you hover the 'H' operation in Visual Studio Code.](https://github.com/user-attachments/assets/8a216327-6bc4-4df9-9963-251155c5223d)

## Run your Q# code

Congratulations! You wrote a Q# program that entangles two qubits and creates a Bell pair. Before running your program, use the `@EntryPoint()` attribute to tell the Q# compiler where to start executing the program. Every Q# program must contain one `@EntryPoint()`. In this case, place `@EntryPoint()` before the `EntangleQubits` operation.

Your final Q# program should look like this:

```qsharp
namespace BellPair {
    open Microsoft.Quantum.Diagnostics;
        
    @EntryPoint()
    operation EntangleQubits() : (Result, Result) {  
        // Allocate two qubits, q1 and q2, in the 0 state.
        use (q1, q2) = (Qubit(), Qubit());

        // Put q1 into an even superposition.
        // It now has a 50% chance of being measured as 0 or 1.
        H(q1);

        // Entangle q1 and q2, making q2 depend on q1.
        CNOT(q1, q2);

        // Show the entangled state of the qubits.
        DumpMachine();

        // Measure q1 and q2 and store the results in m1 and m2.
        let (m1, m2) = (M(q1), M(q2));

        // Reset q1 and q2 to the 0 state.
        Reset(q1);
        Reset(q2);

        // Return the measurement results.
        return (m1, m2);
    }
}
```

To run your program and view the result of both qubits, select **Run** under `@EntryPoint()` or press **Ctrl+F5**:

![Screenshot of the Q# file in Visual Studio Code showing where to find the 'Run' command.](https://github.com/user-attachments/assets/dcf7701c-c2f9-4c9a-8d80-d44cb1838cdd)

You can run the program several times, each with a different result in the debug console. This demonstrates the probabilistic nature of quantum measurements and the entanglement of the qubits.

For example, if the result is `Zero`, your debug console should look like this:

```Result
DumpMachine:

 Basis | Amplitude      | Probability | Phase
 -----------------------------------------------
  |00⟩ |  0.7071+0.0000𝑖 |    50.0000% |   0.0000
  |11⟩ |  0.7071+0.0000𝑖 |    50.0000% |   0.0000

Result: "(Zero, Zero)"
```

## Next step

To learn more about quantum entanglement with Q#, see [Tutorial: Explore quantum entanglement with Q#](https://learn.microsoft.com/en-us/azure/quantum/tutorial-qdk-explore-entanglement). This tutorial expands on the concepts covered in this quickstart and helps you write a more advanced entanglement program.

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
