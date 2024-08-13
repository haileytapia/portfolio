---
layout: default
title: Introduction to Q#
parent: Microsoft
nav_order: 1
permalink: /microsoft/qsharp-intro
---

# Introduction to Q#
{: .no_toc }

August 5, 2024 ∙ [Original document](https://learn.microsoft.com/en-us/azure/quantum/qsharp-overview)
{: .fs-5 : .fw-300 }

Q# is a high-level, [open-source](https://github.com/microsoft/qsharp) programming language for developing and running quantum algorithms. Q# is included in the Quantum Development Kit (QDK). For more information, see [Set up the QDK](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk).

As a quantum programming language, Q# meets the following language, compiler, and runtime requirements:

- **Hardware agnostic:** Qubits in quantum algorithms aren't tied to a specific quantum hardware or layout. The Q# compiler and runtime handle the mapping from program qubits to physical qubits.
- **Integrates quantum and classical computing:** The ability to perform classical and quantum computations is essential in a universal quantum computer.
- **Respects the laws of physics:** Q# and quantum algorithms follow the rules of quantum physics. For example, you can't directly copy or access the qubit state in Q#.

## Structure of a Q# program

Before you start writing quantum programs, it's important to understand their structure and components. Consider the following Q# program that creates a superposition state:

```Q#
namespace Superposition {
    @EntryPoint()
    operation MeasureOneQubit() : Result {
        // Allocate a qubit. By default, it's in the 0 state.  
        use q = Qubit();  
        // Apply the Hadamard operation, H, to the state.
        // It now has a 50% chance of being measured as 0 or 1.
        H(q);      
        // Measure the qubit in the Z-basis.
        let result = M(q);
        // Reset the qubit before releasing it.
        Reset(q);
        // Return the result of the measurement.
        return result;
    }
}
```

Based on the comments (`//`), the `Superposition` program first allocates a qubit, applies an operation to put the qubit in superposition, measures the qubit state, resets the qubit, and finally returns the result. Let's break this program down into its components.

### User namespaces

Q# programs start with a user-defined [namespace](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/programstructure/namespaces), such as:

```qsharp
namespace Superposition {
    // Your code goes here.
}
```

Namespaces help you organize related functionality. Each Q# program can have only one `namespace`.

The Q# standard library has predefined namespaces that contain functions and operations you can use in quantum programs. For more information, see [Built-in namespaces](#built-in-namespaces).

### Entry points

The `@EntryPoint()` attribute tells the Q# compiler where to start executing the program. In a program with multiple functions and operations, you can place `@EntryPoint()` before any of them to make the program start there and continue sequentially.

```qsharp
@EntryPoint()
operation MeasureOneQubit() : Result {
    ...
```

### Types

Q# provides [built-in types](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/typesystem/) that are common to most languages, including `Int`, `Double`, `Bool`, and `String`, and types that are specific to quantum computing. For example, the `Result` type represents the result of a qubit measurement and can have one of two values: `Zero` or `One`.

In the `Superposition` program, the `MeasureOneQubit()` operation returns a `Result` type, which corresponds to the return type of the `M` operation. The measurement result is stored in a new variable that's defined using the `let` statement:

```qsharp
// The operation definition returns a Result type.
operation MeasureOneQubit() : Result {
    ...
    // Measure the qubit in the Z-basis, returning a Result type.
    let result = M(q);
    ...
```

Q# also provides types that define ranges, arrays, and tuples. You can even define your own [custom types](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/programstructure/typedeclarations).

## Allocating qubits

In Q#, you allocate qubits using the `use` keyword. Qubits are always allocated in the ∣0⟩ state.

The `Superposition` program defines a single qubit:

```qsharp
// Allocate a qubit.
use q = Qubit();
```

You can also allocate multiple qubits and access each one through its index:

```qsharp
use qubits = Qubit[2]; // Allocate two qubits.
H(qubits[0]); // Apply H to the first qubit.
X(qubits[1]); // Apply X to the second qubit.
```

For more information, see [Use statement](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/statements/quantummemorymanagement#use-statement).

### Quantum operations

After allocating a qubit, you can pass it to operations and functions, also known as [callables](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/programstructure/callabledeclarations). [Operations](https://learn.microsoft.com/en-us/azure/quantum/user-guide/language/typesystem/operationsandfunctions) are the basic building blocks of a Q# program. A Q# operation is a quantum subroutine, or a callable routine that contains quantum operations that change the state of the qubit register.

To define a Q# operation, you specify a name for the operation, its inputs, and its output. In the `Superposition` program, the `MeasureOneQubit()` operation is essentially the entire program. It takes no parameters and returns a `Result` type:

```qsharp
operation MeasureOneQubit() : Result {
    ...
}
```

Here's a basic example that takes no parameters and expects no return value. The Unit value is equivalent to `NULL` in other languages:

```qsharp
operation SayHelloQ() : Unit {
    Message("Hello quantum world!");
}
```

The Q# standard library also provides operations you can use in quantum programs, such as the Hadamard operation, `H`, in the `Superposition` program. Given a qubit in the Z-basis, `H` puts the qubit into an even superposition, where it has a 50% chance of being measured as `Zero` or `One`.

### Measuring qubits

While there are many types of quantum measurements, Q# focuses on projective measurements on single qubits, also known as [Pauli measurements](https://learn.microsoft.com/en-us/azure/quantum/concepts-pauli-measurements).

In Q#, the `Measure` operation measures one or more qubits in the specified Pauli basis, which can be `PauliX`, `PauliY`, or `PauliZ`. `Measure` returns a `Result` type of either `Zero` or `One`.

To implement a measurement in the computational basis {∣0⟩, ∣1⟩}, you can also use the `M` operation, which measures a qubit in the Pauli Z-basis. This makes `M` equivalent to `Measure([PauliZ], [qubit])`.

The `Superposition` program uses the `M` operation:

```qsharp
// Measure the qubit in the Z-basis.
let result = M(q);
```

### Resetting qubits

In Q#, qubits must be in the ∣0⟩ state when they're released. Use the `Reset` operation to reset each qubit to the ∣0⟩ state before releasing it at the end of the program. Failure to reset a qubit results in a runtime error.

```qsharp
// Reset a qubit.
Reset(q);
```

### Built-in namespaces

The Q# standard library has built-in namespaces that contain functions and operations you can use in quantum programs. For example, the `Microsoft.Quantum.Intrinsic` namespace contains commonly used operations and functions, such as `M` to measure results and `Message` to display user messages anywhere in the program.

To call a function or operation, you can specify the full namespace or use an open statement, which makes all the functions and operations for that namespace available and makes your code more readable. The following examples call the same operation:

```qsharp
Microsoft.Quantum.Intrinsic.Message("Hello quantum world!");
```

```qsharp
open Microsoft.Quantum.Intrinsic;
Message("Hello quantum world!");
```

The `Superposition` program doesn't have any open statements or calls with full namespaces. That's because the Q# development environment automatically loads two namespaces: `Microsoft.Quantum.Core` and `Microsoft.Quantum.Intrinsic`, which contain commonly used functions and operations.

You can take advantage of the `Microsoft.Quantum.Measurement` namespace by using the `MResetZ` operation to optimize the `Superposition` program. `MResetZ` combines the measurement and reset operations into one step, as in the following example:

```qsharp
namespace Superposition {
    // Open the namespace for the MResetZ operation.
    open Microsoft.Quantum.Measurement;

    @EntryPoint()
    operation MeasureOneQubit() : Result {
        // Allocate a qubit. By default, it's in the 0 state.      
        use q = Qubit();  
        // Apply the Hadamard operation, H, to the state.
        // It now has a 50% chance of being measured as 0 or 1. 
        H(q);   
        // Measure and reset the qubit, and then return the result value.
        return MResetZ(q);
    }
}
```

## Related content

- [Different ways to run Q# programs](https://learn.microsoft.com/en-us/azure/quantum/qsharp-ways-to-work)
- [Set up the QDK](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk)
- [Quickstart: Create your first Q# program](https://learn.microsoft.com/en-us/azure/quantum/qsharp-quickstart)

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
