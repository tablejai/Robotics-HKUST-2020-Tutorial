Original Author: Daniel Cheung (dcheungaa@connect.ust.hk)

Updated by: Lau Ka Kit, Danny (kkdlau@connect.ust.hk)

**hackmd version(with better formatting): https://hackmd.io/@DannyLau1205/Sy4vX-oSw**

# HKUST Robotics Team Software Tutorial 0 - Introduction to Programming

## What is Programming?
Programming is providing instructions to a processing unit to perform specific tasks.

Just like humans understand natural languages, computers understand machine language (0s and 1s). Nowadays, computer programs aren't written directly in machine language but in a human-readable form. These programs need to be converted into machine code so that it could be understood by the processing unit. This conversion procress is called **compilation** and is done by a **compiler**.

## Introduction to C, a procedural language

C is an old language. However, it is still relevant due to its performance. It is a **low-level** language, meaning there is little between it and machine code. This also means that we, the programmer, are responsible for managing the memory (RAM).

C is also a procedural language. This means that when we write C code, the computer will follow each instruction line-by-line. A specific way to write a list of instructions to achieve a particular task is what we call an **algorithm**.

## Project Architecture

A programming project usually consists of some common folders - `src`, `build`, `lib`, etc. And conventionally, those folders only store certain types of files:

* **src**: Conventionally, most of your code will be written here. There will usually be a file named `main.c` (or `main.cpp` for C++), which provides the entry point for your program.
* **build**: After compilation, the executable will be stored in this folder.
* **lib**: This folder includes all libraries that the program uses. 

> **Library:**  Library is a collection of code, which can be added to your application. The main difference between ```src``` and ```lib``` is the code of library is implemented by others, or download from the internet.

## Where do I write my code? (Tutorial Preparation)

Since some of you may not have installed an **IDE** (integrated development environment) on your computer yet, you may use an online version to write your programs in. [Repl.it C Language](https://repl.it/languages/c) is a good choice.

### Instructions

1. Simply go onto [Repl.it C Language](https://repl.it/languages/c).
2. In the middle section, you will see a sample code already in place, under the file name `main.c`. You can also see all the files on the left column associated with this setup. Do not worry about other files, editing `main.c` in the middle column is sufficient for now.
3. After you have finished writing your code, click "Run" to compile and run the program. You can then interact with the program on the right, by passing any input it might receive. If there are any errors in the code, the program will stop and display its error message in the console as well. Follow its prompt or maybe search online to find out how to fix the problem.
4. Click "Save", you will see your URL change to `https://repl.it/repls/SomeRandomWords`, you can access your code with this URL later.

## Hello, World!
```c
//main.c
#include <stdio.h>  // This includes functions useful 
                    // for input/output.

// This is the main function, which is your program entry.
int main() {
    // This is a comment.
    
    /* This is a multi-line comment.
     * These gray lines are ignored by the program.
     * It is only here for the programmer(s) to take 
     * notes or to tell their peers how the program works.
     *
     * It is good practice to add comments to your code!
     */
    printf("Hello, World!\n");  // Print Hello world! 
                                // on the console.
    
    return 0;
}
```
In `main.c` (which is the starting point of your program), there is a function called `main`. The computer always execute the main function first. Just like how we end sentences in English with a full stop, we end statements in C with a semi-colon (`;`).

In the example above, `printf("Hello, World!\n");` and `return 0;` are both statements telling the computer specific instructions.

The second line of code, `#include <stdio.h>` is a completely different kind of statement. 

> **Function:**  A function is a collection of commands that perform tasks.


In the main function, we can call other functions, which can be from ```src```, ```lib```, or other places. Compilers also provide some standard functions (e.g. ```printf```). To access the standard functions, you must include a header with the **#include directive**.

```c
#include <stdio.h>
```
This line tells the program we are using features within a library named ```stdio.h```. The ```printf()``` function is defined within this library.

To include **user-defined** libraries, use `""`.

For example:
```c
#include "uart.h"
#include "gpio.h"
#include "motor.h"
```

To include **compiler-defined** libraries, use `<>`.

> **stdio.h**: `stdio.h` is **compiler-defined**, it doesn't appear in `lib`. (Usually user-defined libraries are stored in `lib`.)

In the example above, one of the statements is:
```c
printf("Hello, World!\n");
```

![](https://i.imgur.com/UjpWAg8.png)

This is a **function call**. Some functions take *parameters*, which can take the form of any data. In the example above, we pass `printf` some text data: `Hello, World!` (this is a *character array*, to be exact).

`\n` represents a "newline" character, since we cannot actually store an Enter key in a single line, we use `\n` to break lines.

> **Q:**  How to represent character array in code?
> 
> **A:**  Use `"` to enclose the text you want.

The last statement in the example of above is:

```c
return 0;
```

We use this to give an exit code to the program, to indicate whether or not there is a problem.

> :warning: **warning**: The `main` function is a specific case, in that you can omit the `return` statement. The compiler will automatically add the `return 0;` for you. However, for other functions, you must return something, unless the return type is `void`.

> :exclamation: **Return vs return**: One thing that need to bare in mind: C is **case-sensitive**. Upper-case letters and lower-case letters are entirely different! The following will generate an error:
> 
> ```c
> Return 0;
> ```
> 
> ![](https://i.imgur.com/93cI7uf.png)
> 
> So don't confuse them!


> [Practice - Modify Hello, World!](https://hackmd.io/@DannyLau1205/ByaD6cMNw#ex-1)

## Variables

Let's say we want a program to interact with users. For instance, it allows the user to input a number and then modifies that input somehow.

Before we ask for an input, we first need a place to store it. We use **variables** to store this data.

Variables are containers for values. We use different typed variables to store different types of values, e.g. integer, decimal numbers, text.

The process of creating a variable is called **declaration**.

To declare a variable, you use the syntax `<type> <variable name>;`：
```c
/**
 * A basic variable declaration.
 * The statements below declare integer variables.
 */
int my_number;
int myNumber;

int a, b, c, d; // declare multiple variables in one line
```

> **Q:**  What is the difference between `my_number` and `myNumber`?
> 
> **A:**  They are two distinct variables with different naming styles. You are free to choose the naming style you prefer.

It is good practice to give variables meaningful names.

### Variable Assignment

When a variable is declared, we can assign a value to the variable using the equals sign `=` (aka the assignment operator). We can declare and initialise a variable in the same statement. We assign values like so:

```c
int age = 42;  // age stores 42
age = 100;     // age stores 100

char letter = 'A'; // character variable, for storing a character
char letter_2 = letter;
```

In the above example, we first declare an int (integer) variable `age` and initialise it to `42`. Similarly, we declared a char (character) variable `letter` and initialised it to the character `'A'`. Note that characters must be quoted using **single quotes**.

We then declare a second char variable `letter_2` and initialise it with the value stored in `letter` so that it now has the value `'A'`. Note that here, `a = b` does not mean "`a` equals `b`", but "assign `b` to `a`".

It is good practice to initialize variables when declaring them. Reading from a non-initialized variable is "undefined behavior", meaning the compiler may or may not crash.

### Data Types

These are some of the **primitive types** in C, the most basic variable types:

| Type     | Description                                                                         | Example |
|:-------- |:----------------------------------------------------------------------------------- |:-------:|
| `char`   | 8-bit integer for storing an [ASCII](https://en.wikipedia.org/wiki/ASCII) character |  `'a'`  |
| `int`    | 16-bit/32-bit signed(i.e. can represent +ve and -ve) integer                        |   `1`   |
| `float`  | 32-bit, single-precision floating point value                                       | `3.0f`  |
| `double` | 64-bit, double-precision floating point value                                       |  `5.0`  |


> **Q:** What is the difference between `int` and `float`?
> 
> **A:**  An int variable only stores integers (i.e. it cannot handle decimals). Even if you assign a value with decimal to an int variable, the decimal will be discarded. Ints and floats have different binary representations.


> [Practice - Swapping contents](https://hackmd.io/xwpeswfZTp6_oDtg8KrhFQ#ex-2)


Non-primitive type:

|  Type  | Description                                                                             | Example |
|:------:|:--------------------------------------------------------------------------------------- |:-------:|
| `bool` | 8-bit boolean (i.e. `true` / `false`). To use this type, you must include `<stdbool.h>` | `true`  |
| `void` | The absence of type                                                                     |    /    |

#### Signs, Modifiers, and Value Range

The size of a variable can affect its **value range**. For example, a 32-bit int variable has a value range of -2,147,483,648 to 2,147,483,647. Signed integers will use half of the distinct bit combinations for negative numbers and the other for positive numbers. The ranges are as follows:

![Signed range equation](https://latex.codecogs.com/svg.latex?%5Ctext%7BSigned%20Range%7D%20%3D%20%5B-2%5E%7B%5Ctext%7Bn%7D-1%7D%2C2%5E%7B%5Ctext%7Bn%7D-1%7D-1%5D)

![Unsigned range equation](http://latex.codecogs.com/svg.latex?%5Ctext%7BUnsigned%20Range%7D%20%3D%20%5B0%2C2%5E%7B%5Ctext%7Bn%7D%7D-1%5D)

where ![Unsigned range equation](http://latex.codecogs.com/svg.latex?n) is the number of bits the variable contains.


We can add the `signed` and `unsigned` modifiers to `char` and `int` to set the range the variable can hold.

For example, in order to store the integer 3,000,000,000 (3 billion), we need at least `unsigned long` or `uint32_t`. A signed `int` or `long` is not viable, as their maximum value is lower than 3 billion.

```c=
#include <stdint.h>

int main() {
    unsigned int var0 = 1; // 32-bit unisgned integer
    
    /**
     * stdint.h defines integer types with different data size.
     * For example: uint8_t, uint16_t, uint32_t and uint64_t.
     */
    uint16_t var1 = 1; // 16-bit unsigned integer
    uint32_t var2 = 2; // 32-bit unisgned integer
    int8_t var3 = 3; // 8-bit signed integer
    
    return 0;
}
```

> :warning: **warning**: Memory is very limited for some computers, such as embedded systems. It's a good practice that save memory as much as possible so that out-of-memory can be avoided. That's why we have `uint8_t`, `uint16_t`, etc.

#### Variables and `printf`

To print variables to the console, we call `printf` by first passing a format string, then passing subsequent variables as additional parameters.

```c=
#include <stdio.h>

int main() {
    int n = 10;
    float f = 3.14f;
    char c = 'a';
    
    printf("int: %d\n", n);
    printf("float: %f\n", f);
    printf("char: %c\n", c);
    return 0;
}
```

`%d`, `%f`, and `%c` are **format specifiers**, replaced by subsequent parameters.


| Format specifier | Meaning         | subsequent parameter type |
|:---------------- |:--------------- |:-------------------------:|
| `%d`             | Decimals        |           `int`           |
| `%f`             | Floating Points |          `float`          |
| `%x`             | Hexadecimals    |           `int`           |
| `%c`             | Characters      |          `char`           |



> [Practice -  Printing size of variables](https://hackmd.io/@DannyLau1205/ByaD6cMNw#ex-3)


#### Casting

Assigning a variable or literal from one type to another type is possible through **casting**. Saving a lower-bit value to a higher-bit container is often safe, but the converse may erase information stored in, because information may be lost in the higher bits. Below are some examples:

```c=
int main() {
    bool b = true;
    int n = b; // compiler casts a boolean to an integer, n would be 1 because true -> 1; false -> 0

    char c = 'c';
    n = c; // compiler casts a character to an integer, by using ASCII conversion, n is now 99

    float f = 0.55f;
    n = f; // compiler casts a float to an integer, by truncating the floating point value, n is now 0, same goes with double
  
    return 0;
}
```

The type conversions above demonstrate **implicit** casting, i.e. the compiler casts a value without an explicit indication by the programmer. Usually, instead, we would prefer a safer approach, that we explicitly specify the converted type in a cast.

```c=
float f = 2.5f;
int n = (int)f; //n is now 2
```
Explicit casting also allows us to do this:
```c=
float f = 3.14f;
// both print 3, one formatted as an int, the other as a float
printf("%d %f", (int)f, (float)(int)f);
```

## Function

A function is a collection of commands that perform tasks. You are already familiar with some functions such as `main` and `printf`. These functions perform different tasks and may even return values.

A **function declaration** tells the compiler about a function's name, return type, and its parameters. The format of a function declaration is:

```c
<return_type> <function_name>(<parameters>);
```

If your function does not take any parameters (i.e. `<parameters>` is empty), you can type in `void` or leave it as it is.


Here is an example:
```c
// this function accepts zero parameters
int get_current_time(void);

/**
 * The major difference is:
 * without putting void in the parentheses means this function has any number of parameters.
 * That means you pass any parameter into the function, but you cannnot access it.
 * 
 * However, in C++, there are no differences.
 */
int get_current_time2();

// this function accepts two integers
int addition(int a, int b);

// "void" return type means this function doesn't return anything
void robot_move(int pos_x, int pos_y, int pos_z);

/**
 * You can also pass a function as a parameter.
 * The declaration below accepts a function called "operation".
 * The details will be taught in later tutorials.
 */
int calculator(int a, int b, int (*operation)(int, int));
```

> **Example of void parentheses and empty parentheses**:
> 
> ```c=
> #include <stdio.h>
> 
> int test_funcs(void) {
>     return 2;
> }
> 
> int test_funcs2() {
>     return 1;
> }
> int main() {
>     printf("test_funcs: %d\n", test_funcs());
>     printf("test_funcs2: %d\n", test_funcs2(0, 1, 2));
>     return 0;
> }
> ```
> 
> ![](https://i.imgur.com/RrAlq2F.png)
> 
> Although the compiler throws a warning, the program works. However, if you change add extra arguments to `test_funcs`:
> ```c=
> printf("test_funcs: %d\n", test_funcs(0, 1, 2));
> ```
> ![](https://i.imgur.com/Eh1BNfZ.png)
> 
> The program cannot be compiled successfully. For more details about empty parentheses, read **[this](https://wiki.sei.cmu.edu/confluence/display/c/DCL20-C.+Explicitly+specify+void+when+a+function+accepts+no+arguments)**.

After function declaration, you can define your function body (i.e. **function definition**). The format is
```c
<return_type> <function_name>(<parameters>) {
    // your code
}
```

Remember, `<return_type>`, `<function_name>` and `<parameters>` must be the same as the function declaration.

Here are some examples:
```c=
int addition(int a, int b) {
    const int sum = a + b; // by adding const before the type, the value of the variable is constant
    printf("%d + %d = %d", a, b, sum); // you can call other functions inside a function too!
    return sum; //return the result
}

int calculator(int a, int b, int (*operation)(int, int)) {
    // we can treat "operation" as a function:
    return operation(a, b);
}
```

> [Practise -  Area of circle](https://hackmd.io/@DannyLau1205/ByaD6cMNw#ex-4)

## Standard Input / Output

The standard input/output library `stdio.h` provides some basic functions which allow you to display data, or feed data into your program.

### Output

The function `void printf(const char*, ...)` is used to print output to the console.

```c=
#include <stdio.h>

void print_birthday(int day, int month, int year);
float floating_point_addition(float f1, float f2);

int main() {
    print_birthday(5, 12, 2000);
    float sum = floating_point_addition(10, 0.1f); // 10 will be implicitly casted to 10.0f
    printf("result from floating_point_addition(): %f\n", sum);
    return 0;
}

float floating_point_addition(float f1, float f2) {
    printf("%f + %f = %f\n", f1, f2, f1 + f2);
    return f1 + f2;
};

void print_birthday(int day, int month, int year) {
    printf("My birthday is: %d-%d-%d\n", day, month, year);
}
```

### Input

The function `void scanf(const char*, ...)` reads input from the console and stores it into the given variables. To read variables, specify the data type token and provide the address to the variable. The syntax for `scanf` is similar to `printf`, but an **ampersand** (`&`) is required before the variable name.

```c=
#include <stdio.h>

int main() {
    int user_input = 0;
    // enter an integer and press enter
    scanf("%d", &user_input); // your program will be stop here until enter is pressed
    printf("retrieved value: %d", user_input);
    
    return 0;
}
```

> **Q**: What is the use of `&`?
> 
> **A**: A variable consists of a name, value and address. `&` returns the address of the variable. This topic (pointers) will be taught in depth in later tutorials.


## Operators
**Operators** help us perform the most fundamental mathematical or logical operations on variables.

For example:
```C
10 + 20
```

Here, `+` is an operator, which performs addition. This operator takes two operands: `10` and `20`.

Operators can be classified to 3 categories, based on the number of operands they take:

* **Unary operator**: takes a single operand (`+x`, `-x`, `*x`, `++x`, `--x`, `x++`, `x--`, `!x`, `~x`)
* **Binary oeprator**: takes a two operands (`x + y`, `x - y`, `x * y`, `x / y`, `x % y`, `x && y`, `x || y`)
* **Ternary operator**: takes three operands (`x ? y : z`)

### Arithmetic operators

* `+`: addition
* `-`: subtraction
* `*`: multiplication
* `/`: division
* `%`: modulo (calculates the remainder of the first number divided by the second number)

```c=
#include <stdio.h>

int main() {
    printf("addition: %d\n", 2 + 3); // prints 5
    printf("subtraction: %d\n", 20 - 8); // prints 12
    printf("multiplication: %d\n", 500 * 4); // prints 2000
    printf("division (int): %d\n", 5 / 2); // prints 2
    printf("division (float): %f\n", 5.0f / 2.0f); // prints 2.5
    printf("modulo: %d\n", 13 % 5); // prints 3
    
    return 0;
}
```

Note the two different divisions in the example above.
In math, 5 / 2 = 2.5. However, in C, both `5` and `2` are integers, so integer division is performed. This means the decimal part is discarded giving `2` as its result.

In contrast to this, `5.0f` and `2.0f` are floats, so floating-point division is performed and the decimal part is retained, giving (about) `2.5` as its result.


### Assignment Operators

* `=`: Assigns value from right operand to left operand.

### Compound Assignment Operators

These operators merge arithmetic and assignment into one operation. For example:

* `+=`: Adds right operand to left operand, and assigns the resultant value to left operand.

```c
int a = 1;
int b = 2;

a += b; // equal to a = a + b
```

There are more assignment operators (e.g. `-=`, `/=`, `%=`). Read [this](https://www.tutorialspoint.com/cprogramming/c_assignment_operators.htm) for more details.

### Relational Operators

These operators take two operators and return `true`/`1` or `false`/`0`.

* `==`: returns `true` if the values of two operands are equal.
* `!=`: returns `true` if the values of two operands aren't equal.
* `>`: returns `true` if the left operand is greater than the right operand.
* `>=`: returns `true` if the left operand is greater than or equal to the right operand.
* `<`: returns `true` if the left operand is less than the right operand.
* `<=`: returns `true` if the left operand is less than  or equal to the right operand.

### Logical Operators

- `||` (OR): returns `true` if left or right operands are `non-zero`.
- `&&` (AND): returns `true` if left and right operands are `non-zero`.
- `!` (NOT): reverses the truthness of its operand.

These operators accept **boolean represented** values on both sides, and perform logical operations on them to return a boolean value.

`!` has a higher precedence than `||` and `&&`.

#### Truth Table

| P | Q | P or Q | P and Q | not P |
|:---:|:---:|:------:|:------:|:----:|
|`false`|`false`|`false`|`false`|`true`|
|`false`|`true`|`true`|`false`|`true`|
|`true`|`false`|`true`|`false`|`false`|
|`true`|`true`|`true`|`true`|`false`| 


> **:bulb:TIPS**: Conditions can be chained by logical operators. For example:
> ```c
> int_a != int_b || !(int_c > int_d)
> ```

### Ternary Operator

The **ternary operator** is also known as **conditional operator**. It is similar to `if...else...`, but is faster to type and is considered as a shortcut for `if`.

#### Syntax:
```c
<condition> ? <value1> : <value2>
```
When the condition is true (i.e. `non-zero`), `value1` is returned, else `value2` is returned.

let's look at an example:
```c=
#include <stdio.h>

int main() {
    int midterm_score = 60;
    int final_score = 90;
    /**
     * let's say the method of calculating total score
     * is based on midterm_score
     *
     * if midterm_score is greater than 50,
     * total score = midterm_score * 0.6 + final_score * 0.4
     * otherwise,
     * total score = midterm_score * 0.3 + final_score * 0.7
     */
    int total_score = midterm_score > 50?
        midterm_score * 0.6f + final_score * 0.4f:
        midterm_score * 0.3f + final_score * 0.7f;
    
    // 60 * 0.6 + 90 * 0.4 = 36 + 36 = 72
    printf("total score: %d", total_score);
    
    return 0;
}
```

Since `midterm_score > 50` is true, so `midterm_score * 0.6 + final_score * 0.4` is returned. And the resultant value is assigned to `total_score`.

As above mentioned, ternary operator is a shortcut for `if` statement, so the above example can also be expressed using `if`:
```c=
#include <stdio.h>

int main() {
    int midterm_score = 60;
    int final_score = 90;

    int total_score = 0;
    
    if (midterm_score > 50)
        total_score = midterm_score * 0.6 + final_score * 0.4;
    else
        total_score = midterm_score * 0.3 + final_score * 0.7;
    
    printf("total score: %d", total_score);
    
    return 0;
}
```

One more example (Nested ternary operator):
```c=
#include <stdio.h>

int main() {
    int midterm_score = 30;
    int final_score = 90;
    
    int total_score = midterm_score > 60?
        midterm_score * 0.8 + final_score * 0.2: 
        midterm_score > 40?
            midterm_score * 0.6 + final_score * 0.4:
            midterm_score * 0.4 + final_score * 0.6;
            
    // 30 * 0.4 + 90 * 0.6 = 12 + 54 = 66
    printf("total score: %d", total_score);
}
```

Since `midterm_score > 60` is false, so the second value is returned, which is another ternary operator. Similarly, since `midterm_score > 40` is false, so `midterm_score * 0.4 + final_score * 0.6` is returned.

## Statements

A statement is a fragment of code in C. All statement types are on [cppreference](https://en.cppreference.com/w/c/language/statements).

### Expression Statement

Expression statements are the lines of code that ends in `;`. Or in other words: an expression statement is **a line of code**. Most statements are expression statements and returns a value.

For example:
```c=
#include <stdio.h>

int main() {
    int some_integer = 0;
    printf("updated value: %d", some_integer = 100);
    
    return 0;
}
```

`some_integer = 100` is an expression. After execution, the expression statement returns 100. So eventually `updated value: 100` is printed. By making good use of this feature, you can minimize the lines of code.

### Compound Statements (Code Blocks)

Compound statements consists of one or more lines of code. It defines a **scope**. They are also called **code blocks**.

For example:
```c=
#include <stdio.h>

int main() {
    int a = 10;
    int b = 20;
    printf("a: %d, b: %d\n", a, b);
    a = a + b;
    b = a - b;
    a = a - b;
    printf("a: %d, b: %d\n", a, b);
    return 0;
}
```

the code inside `{}` are compound statements.

#### Selection Statements

Selection statements modify the **control flow** of the program. It uses different sets of code depending on the condition at **runtime**.

##### If Statements

If-statements have the following formats:

- `if (<expression>) <statement_true>`
- `if (<expression>) <statement_true> else <statement_false>`

If `expression` evaluates to a `non-zero` value, then `statement_true` is evaluated. Otherwise, `statement_false` is evaluated if provided along with the `else` clause.

For example:
```c=
uint32_t money = 100;
if (money) {
    printf("I have $%d.\n", money);
} else {
    printf("I have no money.\n");
}

money = money - 100;

if (money) {
    printf("I have $%d.\n", money);
}
```

At the beginning, the value of money is 100. When the program is executing the first if statement, `money` is a non-zero value, so `printf("I have $%d.\n", money);` is executed.

The value of `money` is then substracted by 100, so the value is now equal to `0`. Then when the program runs the second `if` statement, the if-block is skipped.

We can chain multiple if-conditions by writing another if-statement after an `else`.

The following is an example:

```c
if (x > 85) {
    // if x > 85 evaluates to true, this part is run.
    // otherwise, this part is skipped.
} else if (x == 0) {
    // some other code
    // only runs if (x > 85) is false and if (x == 0)
} else {
    // some other code
    // only runs if both (x > 85) and (x == 0) are false
}
```

#### Switch statements

Switch statements allow a variable to be tested for each case. They act as alternatives to if-statements on the superficial level. The format is as follows:

- `switch (<expression>) <statement>`

  The "expression" here must evaluate to some integral value. And the "statement" here is typically a block with case labels.

- `case <integer_constant_expression>: <statement>`
- `default: <statement>`

```c
switch (x) {//value to compare against the cases
    case 1:
        //code for when x == 1
        break; //jumps to the end of the switch statement
    case 2:
        //code for when x == 2
    case 3:
        //code carries on from line above and for when x == 3
        break;
        
    default:
        //code when none of the cases match. The default label is optional
}
```

Each case is compared against the expression in the switch parenthesis, if a match is found, the program **jumps** to that case and starts executing line by line, exiting when encountering `break;` or when the code block ends.

Basically, switch-statements are just if-statements with all their conditions being `x == case_1`, `x == case_2`, etc.

### Iteration Statements

Iteration statements are used to repeat a section of code.

#### While Loop

This statement will execute repeatedly as long as the expression returns `non-zero`. The format is as follows:

- `while (<expression>) <statement>`

The following is an example:

```c
int i = 0;
while (i < 10) {
    printf("%d\n", i);
    i++; // you treat i++ as i = i + 1
}
```

The program checks if `i < 10`. If true, then the statements inside `{}` block are executed. After the block is executed, the program loops back to `i < 10` and executes the block again, until the condition is false.

#### Do-While Loop

This statement will execute, then repeatedly execute as long as the condition is met. The format is as follows:

- `do <statement> while (<expression>);`

```c
int i = 0;
do {
    printf("%d\n", i);
    i++;
} while(i < 10);
```

The statements inside `{}` are executed first, then the condition `i < 10` is checked. If true, the statements are excuted again, until the condition is false. Since, the condition is checked *after* the block is executed, the block is guaranteed to execute at least once.

#### For Loop

For-loops are similar to while-loops but instead, encases the **iterator** (the counting number) within the scope of the loop. The following example illustrates this.

```c
//This program prints from 0 to 9
int i = 0;
while (i < 10) {
    printf("%d\n", i);
    i++;
}

//Written more concisely as:
for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}
```

The for-loop format is as follows:

- `for (<init_expression>; <condition>; <final_expression>) <statement>`

- **`init_expression`**

  This expression is run before the loop. Usually, an iterator variable is declared and initialized here.
  
- **`condition`**

  This expression is run before every iteration of the loop to determine whether the loop continues or ends. Similar to `while`-loops, the loop continues only if this expression is a non-zero value.
  
- **`final_expression`**

  This expression is run after every iteration of the loop. Usually, the iterator is incremented or decremented here.
  
This is the for loop version of the number printing program above:

```c＝
for (int i = 0; i < 10; i++) {
    printf("%d\n", i);
}
```

Since the body only contains a single statement, the curly braces may be omitted:

```c
for (int i = 0; i < 10; i++)
    printf("%d\n", i);
```

In fact, you can omit the one of the clauses, or even all of them:

```c
int i = 0;
for (; i < 10; i++) {
    printf("%d\n", i);
}
```

### Jump Statements

Jump statements alter the flow of the program by literally jumping to a different section of code to execute.

- `break;`

  This statement is only valid in loops and switch statements. It is used to exit the statement, *breaking* the execution.
  
  Example:
  
  ```c
  for (int i = 0; i < 20; i++) {
      printf("%i = d\n", i);
      if (i == 15) break;
  }
  ```

- `continue;`

  This statement is only valid in loops. It skips the rest of the code in the current iteration and jumps to condition to *continue* the loop. For-loops will execute the final-expression before the condition.
  ```c
  for (int i = 0; i < 50; i++) {
      if (i % 2) continue; // skips the printf...
                           // i++ will run, then i < 50
      printf("i = %d\n", i);
  }
  ```

- `return <expression (optional)>;`

  This statement is only valid inside function bodies. It terminates the function, then *returns* a resulting value to the caller. It is seen in the `main()` function, returning a program termination code to the operating system.
  
  `return;` is treated as returning `void`.

- `goto <identifier>;`

  This statement is used to jump to a certain label to continue program execution. **This statement is highly unrecommended, since it may create an erratic control flow as it can jump from scope to scope, and is harmful to debugging as it is difficult to follow the execution path of the program.**
  
## Array

Variables are nice, but what if we need to store a hundred integers :thinking_face:?

```c
int var_0;
int var_1;
int var_2;
int var_3;
.
.
.
int var_99;
```

Although this above method is possible, it is not efficient or feasible. Hence, we use **Array**.

An array is a variable that can store multiple elements. Each element is accessible by an index. The syntax of declaring an array:
```htmlmixed
<data_type> <variable_alias>[<size>]
```

An example of using an array:
```c
int scores[3] = {0};
printf("score: %d\n", scores[0]); // print first element
printf("score: %d\n", scores[1]); // print second element
printf("score: %d\n", scores[2]); // print third element
```


> :exclamation: **Index**: The first index of an array is `0`, not `1`.

> :exclamation: **Boundary Issue**: **Accessing an array out of bounds** is **undefined behavior**, it may not generate any error when used. ([Read more.](https://www.geeksforgeeks.org/accessing-array-bounds-ccpp/))

Examples of declaring an array:
* Declare an `uint32_t` array with size 100:
```c
uint32_t timestamps[100];
```

* Delcare an `uint16_t` array with size `4`, and initialize all elements to `0`:
```c
uint16_t adc_values[4] = {0};
```

* Declare an int array with size `20`:
```c
int natural_numberes[20] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10}; // remaining spaces are filled with 0s
```

* Declare a float array omitting `<size>`:
```c
float position_x_log[] = {0.3f, 0.5f, 0.2f};
```
The size of `position_x_log` is based on the number of values enclosed by `{}`. Since there are three values, the size of the array is `3`.

* Declare an int array, and initialize specific elements:
```c
int grading[] = {
    [0] = 90,
    [1] = 80,
    [3] = 40,
}; // since 3 is the last index, so the size is 4
```

The above initializes values for index `0`, `1` and `3`. Any omitted indices are initialized to `0`. The size of the array is calculated automatically.

```c
float grades[] = {
    ['A'] = 4.0f, // char can cast to integer as well, therefore it is a valid initalization
    ['B'] = 3.1f,
    ['C'] = 2.2f
};
```

> **Q**: Can I initialize an arrays' size using variables?
> ```c
> int n = 10;
> int my_arr[n] = {0};
> ```
> 
> **A**:  Yes, this is possible in C (starting from C99). However, this is not supported in C++ (except with GCC extensions).


> **Q**: Can we change the size of an array **after array declaration**?
> 
> **A**: No. The size of an array is constant. However, by using memory management functions and pointer arithmetic, dynamic arrays can be implemented. For more info, read **[this](http://www.mathcs.emory.edu/~cheung/Courses/255/Syllabus/2-C-adv-data/dyn-array.html)**. (Dynamic arrays won't be covered in the tutorials.)

#### Update Elements
```c
int distance[3] = {0}; // declare and initalize an int array
distance[0] = 1; // update value
distance[2] = 2; // update value
int d = distance[2]; // d is now 2
```
Arrays are usually used with `for`-loops, to iterate over the length of the array for data manipulation.

This example populates the array with the natural numbers:
```c
int n[100];

for (int i = 0; i < 100; i++) {
    n[i] = i + 1;
}
```

The **boundary issue** usually appears while using **loop** and **pointers**, so it is important that make sure the **iterator value** is bounded by using **loop condition**.

### Character Array

In C, there is no built-in `string` type. As an alternative, we use **character arrays** to represent a string:
```c
char name[] = "Danny";
```

Although the length of `Danny` is `5`, there is an invisible character `'\0'` at the end, which C uses to indicate the end of the character array. Hence, the size of `name` array is actually `6`.

Just like normal arrays, you can initialize char arrays using `{}` (note that here, we have to add the `'\0'` character by ourselves):
```c
char day[] = {'2', '4', '-', '0', '7', '-', '2', '0', '2', '0', '\0'};
```

And then you can print the character array using a loop:
```c=
int i = 0;
while (day[i] != '\0') {
    // i++ is post-increment,
    // that means it returns the original value of i,
    // before adding 1 to i
    printf("%c", day[i++]);
}

printf("\n");
```

## What should I do if I get stuck while programming?

Although programming can be fun, debugging is stressful and exhausting. You may come across some bugs that you cannot solve by yourself. Here are some useful websites to use:

* https://www.google.com/
* https://stackoverflow.com/

![](https://scontent-hkg4-1.xx.fbcdn.net/v/t1.0-9/118682379_3245845102131012_3953367756451253336_n.jpg?_nc_cat=1&_nc_sid=730e14&_nc_ohc=iv05igxZrLAAX-iGqlc&_nc_ht=scontent-hkg4-1.xx&oh=293232767c55e233ddc512be681526f9&oe=5F787422)

The easiest way to debug is to print stuff out, so that you can track (1) how your values change and (2) whether your code reaches a certain line of code (e.g. maybe an if-condition failed).

If you really don't know which lines of code cause bugs, you can comment parts of your code and run the code again to see if the bugs reappear or not.

Enjoy your time debugging!
