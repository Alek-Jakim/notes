## C programming

* **C** is a general-purpose, procedural, imperative computer programming language developed in 1972 by Dennis M. Ritchie at the Bell Telephone Laboratories to develop the UNIX operating system.

### Facts about C

* C was invented to write an operating system called UNIX.

* C is a successor of B language which was introduced around the early 1970s.

* The language was formalized in 1988 by the American National Standard Institute (ANSI).

* The UNIX OS was totally written in C.

* Today C is the most widely used and popular System Programming Language.

* Most of the state-of-the-art software have been implemented using C.
---
### CS50 IDE

* **IDE** - integrated development environment which includes programs and features for writing code. 

```c
#include <stdio.h>

int main(void)
{
    printf("hello, world");
}
```

To run the program above, use a **CLI**, or command-line interface, a prompt at which we need to enter text commands. This is in contrast to a graphical user interface, or **GUI**, like Scratch, where we have images, icons, and buttons in addition to text.

### Compiling

* In the terminal in the bottom pane of our IDE, we’ll compile our code before we can run it. Computers only understand binary, which is also used to represent instructions like printing something to the screen. Our source code has been written in characters we can read, but it needs to be compiled: converted to machine code, patterns of zeros and ones that our computer can directly understand.

* A program called a **compiler** will take source code as input and produce machine code as output. In the CS50 IDE, we have access to a compiler already, through a command called `make`. In our terminal, we’ll type in `make hello`, which will automatically find our hello.c file with our source code, and compile it into a program called hello. There will be some output, but no error messages in yellow or red, so our program compiled successfully.

---
### Functions and arguments

* **Functions** - small actions or verbs that we can use in our program to do something, and the inputs to functions are called **arguments**.

Functions can also have two kinds of outputs:
1. **side effects**, such as something printed to the screen  
2. **return values**, a value that is passed back to our program that we can use or store for later