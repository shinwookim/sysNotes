# The C Syntax (Part II)
Now that we've made our first C program, let's discuss some other common features of C.

## Declaring Variables + Integers & Casting (Revisited)
Just like in Java, variables are declared within functions (generally towards the top of the file/function). The type is followed by the name like
```c
int n;
```
and we can initialize them using `=`
```c
n = 5;
int n = 5;  // Declare and initialize in one line!
```
However, unlike Java, when variables are not initialized, their values are considered arbitrary. Technically, the variables are assigned a memory address when they are declared; Before initializing the variable, if we try to read it, they will yield whatever value happens to be at that memory address (no matter how non-sensical it is).

Furthermore, as we have discussed before, we can cast variables (both explicitly and implicitly). For instance, we can implicitly cast values when we initialize the variable like
```c
int n = -50000;
```
Here, the literal `-50000` is coerced into an `int` type. In fact, we can coerce the values like this no matter how much nonsense it might be:
```c
char smaller = n;
```
Additionally, we can explicitly cast the value as well:
```c
unsigned int non_sense = (unsigned int) n;
```
