---
Tags: complete ead 
---
Links: [[EAD|HomePage]]
## Compilation Process

1. C# Source code
2. compiler (Roselyn). There are other langauges in .NET, every language has its own compiler.
	- F# -- f# compiler
	- Vb.net -- Vb.net compiler
3. Assembly (`.dll or .exe`)
	1. *Intermediate language:* intermediate code ( it is converted to machine specific code at runtime by "Common Language Runtime CLR")  CLR^[The Common Language Runtime, the virtual machine component of Microsoft .NET Framework, manages the execution of .NET programs. Just-in-time compilation converts the managed code into machine instructions which are then executed on the CPU of the computer.] implements Just in Time (JIT) compilation i.e it only translates the portion of code that is required to execute instead of translating the whole code., `mono` is JIT compiler for C# in macos. MSIL is an CIL are examples of intermediate languages. All programs written for the `.NET Framework`, regardless of programming language, are executed in the CLR. All versions of the `.NET Framework` include CLR. ^d0e203
	2. *Assembly Metadata:* Information about assembly. such as name, version and stuff.
	3. *Type Metadata:* Information about classes such as their count, available constructors, methods and other information about the code more specifically Types/Classes.
	4. *Resources:* It includes images, icons, audio and other resources used in application are included in this section of the assembly.
5. Native  / Machine code (using CLR)
6. OS / Hardware
<br>
```mermaid
graph TD
	A[C# source code]
	B["Assembly (.exe or .dll)<br>--------------------------------------------<br>1. Intermediate Code (Machine Indpendent)<br>2. Assembly MetaData<br>3. Type MetaData<br>4. Resources<br>--------------------------------------------"] 
	D[Native Machine Code]
	E[OS<br>- - - - - -<br>Hardware]

	A --> |"Compiled by compiler like Roselyn"| B
	B --> |"Converted to machine specific code at runtime by CLR like mono"| D
	D --> |"Executed By"|E
```

```ad-info 
title: .exe vs .dll

1. EXE is an extension used for executable files while DLL is the extension for a dynamic link library.
2. An EXE file can be run independently while a DLL is used by other applications.
3. A DLL file can be reused by other applications while an EXE cannot.
```

##  File Hierarchy in DotNet Project
Here is a general overview of the file structure of a .NET project:
-   **Solution file:** A solution file (with the .sln extension) is the top-level container for a .NET project. It contains references to all the projects in the solution and stores information about the solution's configuration.
    
-   **Project files:** A project file (with the .csproj or .vbproj extension) represents a buildable unit in a .NET solution. It contains references to all the source code files and other resources that are part of the project, as well as information about the project's build settings and dependencies.
    
-   **Source code files:** Source code files contain the actual code for the project, written in C# or Visual Basic. These files typically have the .cs or .vb extension.
    
-   **Configuration files:** Configuration files (such as app.config or web.config) contain settings and configuration information for the project.
    
-   **Resources:** Resources are files that are used by the project, such as images, audio files, and data files. These files are typically stored in a separate "Resources" folder within the project.
    
-   **References:** References are libraries and assemblies that are referenced by the project. These files are typically stored in a separate "References" folder within the project.
    

This is just a general overview of the file structure of a .NET project. The actual file structure may vary depending on the specific requirements and needs of the project.




<br>
Created: 2022-10-21
