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

```c
#include <stdio.h>
#include <cs50.h>

int main(void) {
    string name;
    int age;
    name = get_string("What is your name ?\n");
    printf("Hello %s!\n ", name);
    age = get_int("\nHow old are you ?\n");
    printf("It is fun to be %i! \n", age);
}
```

* The `%s` is called a format code, which just means that we want the printf function to substitute a variable where the `%s` placeholder is. And the variable we want to use is `answer`, which we give to `printf` as another argument, separated from the first one with a comma.

* And we also need to indicate that our variable named answer has a type of `string`, so our program knows to interpret the zeros and ones as text.

* We need to tell the compiler to include the CS50 Library, with #include `<cs50.h>`, so we can use the `get_string` function.

* `\n` is an example of an escape sequence, or some text that represents some other text.

---

### Main, header files

 In C, the first line and the main program is `int main(void)`, followed by an open curly brace {, and a closed curly brace }, wrapping everything that should be in our program.

```c
int main(void)
{

}
```

* Header files that end with `.h` refer to some other set of code, like a library, that we can then use in our program. We include them with lines like `#include <stdio.h>`, for example, for the standard input/output library, which contains the `printf` function.

---

### Tools

* `help50` is a command we can run to explain problems in our code in a more user-friendly way. We can run it by adding help50 to the front of a command we’re trying, like `help50 make hello`, to get advice that might be more understandable.

* In C, new lines and indentation generally don’t affect how the code runs. For example, we can change our main function to be one line, `int main(void){printf("hello, world");}`, but it’s much harder to read, so we would consider it to have bad style. We can run `style50`, as with `style50 hello.c`, with the name of the file of our source code, to see suggestions for new lines and indentation.

* Add comments with `//`

* `check50` will check the correctness of our code with some automated tests. After we run check50, we’ll see some output telling us whether our code passed relevant tests.


