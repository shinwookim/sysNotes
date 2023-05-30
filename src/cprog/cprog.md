# The C Programming Language
> C is not a “very high-level” language, nor a “big” one, and is not specialized to any particular area of application. But its absence of restrictions and its generality make it more convenient and effective for many tasks than supposedly more powerful languages.
> 
> — *Kernighan & Ritchie*

## Compiling C Programs
Unlike Java (which uses the Java Virtual Machine) and Python (which uses an interpreter), C is a **compiled language**. C source code is generally converted into machine code which can run directly on the CPU. The difference is in a trade-off about when and how to create a machine-level representation of the source code.

Generally, a C compiler will typically convert a `*.c` source file into an intermediate `*.o` object file. Then, a linker will *link* these together to form an actually executable.

```mermaid
flowchart LR
    code([Source Code]) --> Compiler
    Compiler --> asm([Assembly Code])
    asm --> Assembler
    Assembler --> m([Machine Code])
    m --> Linker
    Linker --> exe([Executable])
```

Later, we will look at each of the phases to compiling a C program. For now, we can consider the compiler as a program that simply takes the C source code and translates it into a machine-code executable.

## Compilation vs Interpretation
In a compiled language, like C, the source code is translated prior to run-time (during compilation) into a format that can be executed directly on the hardware. This, alongside various compiler optimization techniques, mean that compiled languages can run very fast. However, since each program needs to be translated to its respective architecture's machine code, to move a program from one machine to another, may require recompilation of the source code.

In an interpreted language, like Python, the source code is executed as it is read by a interpreter program (which is often written in some other language) and translated into machine code line-by-line. Because of this, interpreted languages do not rely on the hardware as long as the appropriate interpreter is installed on the target system. However, since the source code needs to be translated at run-time, interpreted languages are often much slower than compiled languages.

Another approach for languages is to use both an interpreter and a compiler.Java can be considered both a compiled and an interpreted language because its source code is first compiled into a binary byte-code. Byte code is a pseudo-architecture in that there are no real hardware that can run byte code. Instead, a type of virtual machine (like the Java Virtual Machine) simulates the byte-code architecture and the byte-code is translated into machine code periodically. This is a type of delayed compilation called Just-In-Time compilation. Just-In-Time compilation is a compromise to both approaches (compiler/interpreter) and it is surprisingly competitive in its execution speed.