# About
[CS 449](https://courses.sci.pitt.edu/courses/view/CS-449), titled *Introduction to Systems Software*, is the second course (of three sequential courses) in the University of Pittsburgh's Computer Science "Systems" curriculum. This course follows [CS 447](https://courses.sci.pitt.edu/courses/view/CS-447) (Computer Organization and Assembly) which focuses on how the CPU works (using MIPS assembly). With a good understanding of how the CPU interacts with the software we write, this course shifts focus on to memory and how each process manages its address space. Once students have a solid foundation on how the hardware interacts with the software, the final course in the three course sequence, [CS 1550](https://courses.sci.pitt.edu/courses/view/CS-1550) (Introduction to Operating Systems), looks at how various abstractions can help ease the user from worrying about the specific hardware details.


# Introduction
Most programs today are written using high-level programming languages (such as Java or Python) and many programs merely glue together existing components. However, the best craftsmen are those who understand their tools. For software builders, this means having a solid foundational knowledge of how a computer works internally. CS 449 aims to provide that knowledge by exploring how computers use memory to hold data and instructions, how high level languages abstract from the hardware (with the help of compilers), and how operating systems combine programs and libraries to create running code.

## What is Systems?
This course is titled *Introduction to Systems Software*, but what do we mean by a *Systems Software*?

**Systems** is a broad subfield of computer science that deals with the interaction of hardware and software. Typically, a programmer works on top of the layers of abstractions that hide away hardware details. For instance, when we want to display something to the monitor screen, we can use a function like `print` that is provided by a standard library instead of manipulating the monitor pixel-by-pixel. Similarly, if we were to write to a file, we can utilize the operating system's file system rather than moving the hard disk's write head and changing the magnetic poles manually. These abstractions are designed so that a programmer can focus on software design elements rather than working out the quirks and details of various computer hardware.

However, when studying Systems, we will go beneath the layer of abstractions to explore how they are built/implemented. This will allow us to:
1. Better understand how these abstractions work & potentially improve on them
2. Design our programs to take advantage of/avoid pitfalls of the hardware quirks

and much more.

## The C Programming Language
One of the most useful tools that can help us understand the interaction of hardware and software will be the **C programming language**. We will use many programs that are written with C (which we can modify), but also use it to write and test our own programs.

C is particularly useful because it provides high-level abstraction of assembly (with its syntax) while maintaining low-level access to memory (through pointers). This direct memory access is crucial for us as it is key to manipulating the CPU and other hardware. Since the CPU fetches instructions from RAM, by making changes to memory content, we are able to control and manipulate the CPU as well as other hardware devices.[^von-neumann]

Additionally, many common system-level programs are written in C (or C-like languages). For instance, most operating systems are written in C; and C itself, in fact, was created in 1972 with the purpose of being used in the Unix operating system.[^linux] As such, by learning to use C, we will learn to write and make modifications to the operating system which can further our understanding of how hardware abstractions work. With systems knowledge in one hand and C knowledge in the other, we will be able to ensure that our abstractions do not hurt performance and alleviate design fatigue.[^abstraction]

## Why Learn Systems?
Even if you are not a computer (hardware) engineer, 
Learning how programs interact with the underlying hardware is crucial for any software builder that wishes to write better software (regardless of if you are a '*hardware person*'). By the end of this courses, you will be able to:
- make optimizations to make your program more performant
- bypass the abstract interfaces to get the level of control or the performance you need
- fix bugs that come as a result of undefined behavior
- write/modify existing abstract layers such as operating systems or compilers
- debug higher-level programs (The Python interpreter is written in C!)
- and break things for the greater good (remove copy-protection or reverse-engineer programs)!







---
[^von-neumann] A computer with a CPU that fetches instructions from main memory is said to be of the **Von Neumann Architecture**.

[^linux] The Linux operating system (which is the most popular of the UNIX-like operating systems) and its device drivers are written mostly in C with over 10 million lines of code.

[^abstraction] Ensuring that abstractions are performant is a crucial task for any operating system developer. If an operating system's abstraction is slow, the performance of all application that run on that computer system will suffer.