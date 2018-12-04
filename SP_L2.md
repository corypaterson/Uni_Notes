# Introduction to C
---
### Compiler Errors and Warnings

The errors and warnings provided by the compiler are feedback to tell you that there is something wrong with your program.
- An error means that it is **impossible** to run your code.
- An error means that there is an unusual condition that *may* indicate a problem with your code.
- The **-Werror** and **-Wall** compiler flags turn all warnings into errors that will stop complilation.

### MakeFiles
Make files are the bost popular build system for C programs. They automate the process of compiling programs.

            program: source.c
                clang -Wall -Werror source.c -o program
                
- The first two lines form a *rule* which explains how a target should be built
    - The **first** line specifies your **program** and **lists all the dependencies** (after the colon)
    - The **second** line are the **commands that will be run**, defining how the targert will be built.

### C Program Entry Point 
Every C program has exactly one main function which is the entry point into the main program

- When the main function terminates (buy hitting the '}' ). A value of **zero** is returned, indicating a successful compilation.
- A **positive** return value indicates an unsuccessful exectuion.

There are two valid versions of Main(), the second allows for processing commandline arguments.

        int main()
        int main(int argc, char* argv[])
        
### Basic Output
The printf() statement allows for formatted printing of values as follows:
 - The number and order of values corressponds to the position in the string.

        printf("%d + %d = %d", 3, 4, 7)
        OUTPUT: 3 + 4 = 7
| Special Characters| Argument Type  |
| ------------- |-------------|
|%c    | char |
| %s     | string(char *)   |
| %d | int    |
| %f | float/double |
---
# Variables

Variables definitions in C contain:
- The **data type**
- The **name** of the variable 
- and an **initialization expression**

        int x = 4;

### Lexical Scoping

Each pair of {} curly braces is called a *block* in C and introduces a *lexical scope*. Variable names **must** be unique within the same lexical scope. 

**Preprocessor Macros** do not respect lexical scoping.

        #define ADD_A(x) x + a

If this is written at the top of the document, then where ADD_A(x) is typed, it will be replaced with x + a when compiling.


### Variable Lifetime

There are three different cases for the lifetime of a variable these are:
1. *automatic*. These variables are declared locally in a block and their lifetime ends at the end of a block.
2. *static*. The '**static**' keyword or varibles **defined at file-level** (outside any blocks of code). Lifetime is the entire execution of the program.
3. *allocated*. These variables are allocated memory and their lifetime will be when you free up the allocated section again.

Automatic memory allocation:
>Every time a block is entered, memory is put aside for every variable declared in that block. Once a block is exited, those memory locations are then freed. This works in a **last-in-first-out** manner and therefore is deemed **stack-based memory management**. 

### Arrays

Arrays consist of multiple elemnents of the same type. The elements of an array sre stored in locations next to eachother in memory.

### Strings and Characters

Strings in C are represented as **arrays** of characters.

        char greeting[] = "Hello";
        IS THE SAME AS 
        char greeting[] = {'H', 'e', 'l', 'l', 'o', '\0'};

- Strings in C are terminated with '\0' it is added normally for litteral strings *(first example)* but must be added for arrays of characters *(second example)*
- If the terminating character is not added, the program will keep seraching through memory until the next string terminator is found!

---
# Functions
Every function will have:
- A **return type**
- The **name** of the function
- The **function body** 
- A **parameter list**

To call a function, a value must be given for each declared parameter, otherwise it will not compile.

### Declaration vs Definition

A function **definition** fully specifies the behaviour of the function (bit with the algorithm).

A function **declaration** only specifies rthe interface describing how a function can be used.

When compiling, the linker will try and find the definition to a declaration which might be in a different file or library.





