---
layout: default
title: Ways to run Q# programs
parent: Microsoft
nav_order: 2
permalink: /microsoft/qsharp-ways-to-run
---

# Different ways to run Q# programs
{: .no_toc }

August 5, 2024 ∙ [Original document](https://learn.microsoft.com/en-us/azure/quantum/qsharp-ways-to-work)
{: .fs-5 : .fw-300 }

Azure Quantum offers different development options for writing and running quantum programs. Each environment uses the Quantum Development Kit (QDK), a set of open-source tools that includes the Q# programming language. For more information, see [Introduction to Q#](/portfolio/microsoft/qsharp-intro).

In this article, you learn the differences between each option and how to choose the right one for your needs.

## Options for running Q# programs

Azure Quantum is available through three development environments:

- **Azure Quantum website:** Use Copilot to write, run, and explain Q# code in your browser. No installation or Azure account required.
- **Azure portal:** Manage your Azure subscription and Azure Quantum workspace, where you can write and run Q# and Python programs in Jupyter Notebooks. No installation required.
- **Visual Studio Code:** Write, run, and debug quantum code in your local environment, using Q# as a standalone program or with Python. Installation required.

The option you choose for running Q# programs depends on your coding experience, quantum knowledge, and goals. Because each option has different features and functionality, you typically use them together, such as writing Q# programs with the QDK extension in VS Code while managing your quantum workspace in the Azure portal. For more information, see the following table:

|                            | Azure Quantum website | Azure portal | Visual Studio Code |
|:--------------------------:|:---------------------:|:------------:|:------------------:|
| Built-in Q# support        |           ✔           |       ✔      |          ✔ *       |
| QPU access                 |           ✔           |       ✔      |          ✔ **      |
| Jupyter Notebooks          |                       |       ✔      |          ✔         |
| Resource Estimator         |                       |       ✔      |          ✔         |
| Python support             |                       |       ✔      |          ✔         |
| Cirq and Qiskit support    |                       |       ✔      |          ✔         |
| Integrated hybrid          |                       |              |          ✔         |
| Local setup                |                       |              |          ✔         |
| Quantum workspace creation |                       |       ✔      |                    |

\* VS Code provides rich Q# support, such as CodeLens, IntelliSense, and debugging.

\** QPU access in VS Code requires an Azure subscription.

## Azure Quantum website

On the [Azure Quantum website](https://quantum.microsoft.com/), you can run Q# programs in an online code editor—no installation or Azure account required. Write your own Q# code, explore the built-in Q# samples, or prompt Copilot to code for you.

The Azure Quantum website also features blogs, articles, and videos from quantum experts and enthusiasts. The [Quantum Katas](https://quantum.microsoft.com/en-us/experience/quantum-katas) deepen your knowledge with self-paced tutorials on the fundamentals of quantum computing and Q#.

For more information, see [Explore Azure Quantum](https://learn.microsoft.com/en-us/azure/quantum/get-started-azure-quantum).

### Is the Azure Quantum website right for me?

The Azure Quantum website lets you run Q# programs in your browser and access various learning resources. If you're a quantum enthusiast who wants to learn by doing, the Azure Quantum website is for you.

The following table shows what you can and can't do on the Azure Quantum website:

From the Azure portal, you can grant a group of users, like your team members or students, access to your quantum workspace. If you want to manage your subscriptions, review your invoices, or add quantum providers, the Azure portal is for you.

| You can: | You can't: | You need: |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|-----------------------------------------------------------------------|
| <br> • &nbsp; Create quantum workspaces. <br> • &nbsp; Manage your subscriptions and workspaces. <br> • &nbsp; Copy access keys of your workspace. <br> • &nbsp; Manage your quantum jobs. <br> • &nbsp; Run Q# and Python programs in Azure notebooks. <br> • &nbsp; Save your programs and results. <br> • &nbsp; Select any quantum computing provider. | <br> • &nbsp; Access the Quantum Copilot. <br> • &nbsp; Debug your programs. | <br> • &nbsp; An Azure subscription. <br> • &nbsp; A quantum workspace. <br> • &nbsp; No installation required. |

## Azure portal

The [Azure portal](https://portal.azure.com/https://portal.azure.com/) is the main interface of the Microsoft Azure cloud computing platform. From the portal, you can create an [Azure Quantum workspace](https://learn.microsoft.com/en-us/azure/quantum/how-to-create-workspace) to run quantum programs, send them to [quantum hardware providers](https://learn.microsoft.com/en-us/azure/quantum/qc-target-list), and store their results in an Azure Quantum storage account. You can also manage your subscriptions, activity, credit usage, quotas, and access control.

{: .tip }
> First-time users automatically receive USD500 free Azure Quantum Credits to use with any participating quantum hardware provider.

Quantum workspaces include [Azure Quantum notebooks](https://learn.microsoft.com/en-us/azure/quantum/get-started-jupyter-notebook), which are web-based Jupyter Notebooks in the Azure portal. Use Azure notebooks to create, upload, store, and run Q# and Python programs on quantum simulators or hardware. From your quantum workspace, you can use sample notebooks to get started with quantum programming.

You can also use the [Azure Quantum Resource Estimator](https://learn.microsoft.com/en-us/azure/quantum/intro-to-resource-estimation) in Azure notebooks to estimate the physical resources required to run your Qiskit and QIR programs. For more information, see [Run the Resource Estimator in the Azure portal](https://learn.microsoft.com/en-us/azure/quantum/how-to-submit-re-jobs).

### Is the Azure portal right for me?

From the Azure portal, you can grant a group of users, like your team members or students, access to your quantum workspace. If you want to manage your subscriptions, review your invoices, or add quantum providers, the Azure portal is for you.

| You can: | You can't: | You need: |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|-----------------------------------------------------------------------|
| <br> • &nbsp; Create quantum workspaces. <br> • &nbsp; Manage your subscriptions and workspaces. <br> • &nbsp; Copy access keys of your workspace. <br> • &nbsp; Manage your quantum jobs. <br> • &nbsp; Run Q# and Python programs in Azure notebooks. <br> • &nbsp; Save your programs and results. <br> • &nbsp; Select any quantum computing provider. | <br> • &nbsp; Access the Quantum Copilot. <br> • &nbsp; Debug your programs. | <br> • &nbsp; An Azure subscription. <br> • &nbsp; A quantum workspace. <br> • &nbsp; No installation required. |

## Visual Studio Code

[VS Code](https://code.visualstudio.com/) is a free, open-source code editor from Microsoft. With the QDK extension for VS Code, you can create Q# programs, load built-in Q# samples, and use features like error messaging, syntax highlighting, debugging, circuit diagram visualization, CodeLens, and IntelliSense—all in your local development environment.

You can also use the [Azure Quantum Resource Estimator](https://learn.microsoft.com/en-us/azure/quantum/intro-to-resource-estimation) to estimate the physical resources required to run your Q# programs on quantum computers. The Resource Estimator is part of the QDK, so you don't need an Azure subscription to use it. For more information, see [Run the Resource Estimator in VS Code](https://learn.microsoft.com/en-us/azure/quantum/how-to-submit-re-jobs).

You don't need an Azure account to use the QDK in VS Code. However, if you have an Azure account, you can connect to your Azure Quantum workspace from VS Code and run Q# programs on the quantum computers and simulators of your selected providers.

To get started, see [Set up the QDK](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk).

{: .note }
> The QDK extension is also available for [VS Code for the Web](https://vscode.dev/quantum), which provides the same Azure connectivity and Q# language features as the desktop version. However, it doesn't support Python, Qiskit, or Cirq.

### Integration of Q# and Python

In VS Code, you can use Q# by itself or with Python, which requires the `qsharp` and `azure-quantum` Python packages. To install these packages, see [Add support for Python and Jupyter Notebooks](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk#add-support-for-python-and-jupyter-notebooks).

The following table shows how to use Q# with and without Python in VS Code:

| Format           | Files       | Description                                                                                                                                                                                                                                                                      |
|------------------|-------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Q#               | .qs         | A Q# program that contains only Q# code. |
| Q# and Python    | .qs and .py | The Python program is a host program that, at some point in its routine, calls and uses the results of the Q# program. This is typically for complex projects. |
| Jupyter Notebook | .ipynb      | The Python kernel supports both code and text cells. By default, code cells use Python, but you can change them to Q# with the `%%qsharp` command. This means you can have Python code, Q# code, and explanatory text in one file. For more information, see [The %%qsharp command](https://learn.microsoft.com/en-us/azure/quantum/qsharp-overview#the-qsharp-command). |

### Is Visual Studio Code right for me?

VS Code is a feature-rich environment that includes CodeLens and IntelliSense for writing, running, and debugging quantum programs. If you have coding experience and want to explore Q# in depth, VS Code is for you.

The following table shows what you can and can't do in VS Code:

| You can: | You can't: | You need: |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| <br> • &nbsp; Run Q# and Python programs. <br> • &nbsp; Load Q# samples. <br> • &nbsp; Debug your programs. <br> • &nbsp; Save your programs and results. <br> • &nbsp; Select any quantum computing provider. <br> • &nbsp; Visualize quantum circuit diagrams. <br> • &nbsp; Create and run Jupyter Notebooks. <br> • &nbsp; Have compiler error messages. <br> • &nbsp; Use the Resource Estimator. | <br> • &nbsp; Access the Quantum Copilot. <br> • &nbsp; Manage your subscriptions and workspaces. <br> • &nbsp; Manage your quantum jobs. | <br> • &nbsp; To install [VS Code](https://code.visualstudio.com/). <br> • &nbsp; To install the [QDK extension](https://marketplace.visualstudio.com/items?itemName=quantum.qsharp-lang-vscode). <br> • &nbsp; An Azure subscription and a quantum workspace (to run programs on real hardware). |

## Q# learning resources
To learn and explore the Q# programming language, use the following resources:

- **[Azure Quantum learning path](https://learn.microsoft.com/en-us/training/paths/quantum-computing-fundamentals):** If you're interested in quantum computing but don't know where to start, take this learning path. Through a series of interactive modules, you learn about quantum computing and how to develop quantum solutions using Q# and the QDK.
- **[Quantum Katas](https://quantum.microsoft.com/experience/quantum-katas):** Learn quantum computing and programming simultaneously with these self-paced tutorials, each with relevant theory and Q# exercises to test your knowledge.
- **[Q# code samples](https://github.com/microsoft/qsharp/tree/main/samples):** Build your first quantum solution with these ready-to-use Q# samples. They cover four areas: quantum algorithms, resource estimation, language constructs, and Jupyter Notebooks.
- **[QDK playground](https://vscode.dev/quantum/playground/):** Explore common quantum algorithms written in Q#. The playground is hosted on VS Code for the Web and comes preconfigured with the QDK, so you don't need to install anything.

## Related content

- [Set up the QDK](https://learn.microsoft.com/en-us/azure/quantum/install-overview-qdk)
- [Quickstart: Create your first Q# program](/portfolio/microsoft/qsharp-quickstart)
- [Reference: QDK extension for VS Code](https://learn.microsoft.com/en-us/azure/quantum/vscode-qsharp-reference)

---

[Back to top](#top)

Thanks for visiting my portfolio! Don't hesitate to get in touch if you have any questions or feedback.
