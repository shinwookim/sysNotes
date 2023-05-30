# Hello, World! C Edition
It’s traditional when learning a new language to write a little program that prints the text `Hello, world!` to the screen, so we’ll do the same here.

> Because C maintains a low-level access to hardware, some of its details (like the size of an `int`) is hardware dependent. For this course, we will be using a 64-bit machine running the latest version of Linux to run, compile, and test all code. For compilation, we will use `gcc` or the GNU compiler collection.

We'll start by making a new source file called `hello.c` (C source files end with the *.c* extension). Now, open the *hello.c* and enter the code below:
```c
// File includes must states at the top of the file
#include <stdio.h>
int main(void)
{
    printf("Hello, World!\n");
    return 0;
}
```
Save the file and open the terminal in the working directory. On the terminal, enter the following commands to compile and run the file:
```sh
$ gcc -Wall hello.c -o hello
$ ./hello
Hello, World!
```
## Anatomy of a C Program
Let's now dissect the code we've written. Here's the first piece of the puzzle:
```c
int main(void){

}
```
These lines define a function named `main`. The `main` function is special: it is always the first code that runs in every C program. Here, the first line declares a function named `main` that has no parameters and returns an `int`. If there were parameters, they would go inside the parentheses `()`. The `int` return value indicates whether a function executed successfully. T

Next, the function body is wrapped in `{}` and holds the following code:
```c
println("Hello, world! \n");
```
This line does all the work in this little program: it prints text to the screen. The rules for the string argument is similar to Java. For instance, the `\n` denotes a newline and `\t` denotes a tab.


### Using External Libraries
Notice however, that we are calling the `printf` function without every declaring it in our program. This is because the `printf` function is part of the C standard library. We can use functions that are defined elsewhere as long as we inform the compiler as such.

The very first line in our program has the `#include` statement.
```c
#include <stdio.h>
```
This line tells the C preprocessor to copy over the contents of the *stdio.h* file into the *hello.c* source file (essentially performing a text-replacement). Now, 
if we move into into the directory where the standard library is installed and examine the *stdio.h* file, we will find the declaration for the `printf` function which looks something like:
```c
int printf(const char* format, ...);
```
There are **n** important details to notice here:

First, the *stdio.h* header file does not contain the implementation for the `printf` function; only the function signature is given. The actual code (implementation) for `printf()` is defined elsewhere and is *linked* when our source code goes through the compiler. We will learn what *linking* means later in the course. The function signature is here only to tell the compiler that a function which matches this signature does in fact exists. This is a crucial line because in C, everything (including functions) must be declared before being used.

Second, the function signature indicates that the `printf` function returns an `int`. It is common practice to return an integer value to indicate whether a function has succeeded. Typically, a return value of zero is considered to be "successful".

Third, the function signature indicates that `printf` accepts a memory address of an "array of `const char`s" and a variable number of additional arguments (indicated by the `...`). The character array is equivalent to a string in C and the optional additional arguments are used to pass in values that can replace the placeholder (like `%d`) in the string.

Fourth, we end the line with a semicolon (;), which indicates that this expression is over and the next one is ready to begin. Most lines of C code end with a semicolon.