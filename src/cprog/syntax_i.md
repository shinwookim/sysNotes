# The C Syntax (Part I)
## C Dialects
C is a very old language. Because of this, there are a lot of different styles of C in the world. Luckily, throughout the many standard revisions, the syntax has changed very little. However, newer C standards (or versions) support additional features. As such, we can declare the C version explicitly when we compile using the `-std` flag like: 

```sh
# For C versions later than C99
gcc -std=c99 source.c
# For C389 (ANSI/ISO C)
gcc -ansi -–Wpedantic source.c
```

The main versions of C are:
- C89 (ANSI/ISO C) which is the original C standard
- C99 (released 1999) which adds 'complex' numbers and single-line comments
- C11 (released 2011) which standardizes Unicode and supports newer threading libraries (for better parallelism)
- C18 (released 2018) which makes minor refinements to C11

For us, we will more or less focus on the C99 standard in this course.

## Learning C as a Java Programmer
Unlike Java which is a *Object-Oriented language*, C is a **procedural language**. This means that C code specifies a series of well-structured steps and procedure instead of *encapsulating* functions and data into classes (or abstract data types). Consequently, the basic programming unit in C is a **function**.

Additionally, as we have discussed before, compilation of C program requires a compiler (like gcc) which can translate the source code into machine language code. In contrast, Java code uses a compiler (javac) that translates source code into Java virtual machine language bytecode. 
```sh
# Compiling a C program using gcc
gcc source.c

# Compiling a Java program using javac
javac source.c
```
As such, Java programs require a bytecode interpreter whereas C programs can be loaded directly on the underlying hardware
```sh
# Execute a compiled C executable
./a.out

# Execute a compiled Java executable
java prog
```

One of the more interesting feature of C is its capacity to directly access memory. In Java, memory management is done automatically with memory being allocated with the `new` keyword and the garbage collector automatically freeing memory when the object loses its reference. In C, however, memory allocation must be done manually using the `malloc()` function and freed using the `free()` function.

Syntax wise, C supports the same single line comments (`//...`) and multi-line comments (`/* ... */`) just like in Java. Constants, on the other hand, can be defined using the `#define` macro or the `const` keyword. In comparison, Java uses the `final` keyword. The macros (defined using `#define`) are filled in using text-replacement by the **preprocessor** prior to compilation. In Java, there is no equivalent preprocessor.

Furthermore, like in Java, variables need to be declared before being used. However, in older versions of C (mainly those before C99), variables need to be declared at the top of the file. In fact, it is still common practice to declare variable and function names at the top of the file. When declaring variables, the common convention is to use `snake_case`.[^java-case]

Lastly, to access an external library, we can use the `#include` preprocessor directive with the appropriate header file like:
```c
#include <stdio.h>
```
Header files are simply text files which contain the names of the functions in the external library. The angle brackets (`< >`) tell the preprocessor to look for the file in the location of the system's standard library. If instead, we were using a custom (non-standard) library, we would need to use quotation marks and explicitly state the path to the header file like:
```c
#include "path/to/header.h"
```

|                             | C                                                                  | Java                                                                 |
| --------------------------- | ------------------------------------------------------------------ | -------------------------------------------------------------------- |
| Language Type               | Procedural                                                         | Object Oriented                                                      |
| Programming Unit            | Functions                                                          | Classes (Abstract Data Types)                                        |
| Compilation                 | `gcc source.c` creates a machine language code                     | `javac source.java` creates a Java virtual machine language bytecode |
| Execution                   | `./a.out` loads and executes the program                           | `java prog` runs the JVM which interprets the bytecode               |
| Memory Management           | Manual using `malloc()` and `free()`                               | Automatic using the `new` keyword and the garbage collector          |
| Comments                    | `// single line comments` and `/* multi-line comments */`          | `// single line comments` and `/* multi-line comments */`            |
| Variable Declaration        | Before using it (additional restrictions with older versions of C) | Before using it                                                      |
| Variable Naming Conventions | `snake_case`                                                       | `camelCase`                                                          |
| Accessing a Library         | `#include <stdio.h>`                                               | `import java.io.File;`                                               |
