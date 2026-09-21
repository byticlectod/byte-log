## Introduction

Java is a high-level, class-based, object-oriented programming language. Its syntax was influenced by C and C++. Java abstracts away many low-level programming complexities. For example, Java does not support C++-style multiple inheritance of classes, and memory management is handled automatically through garbage collection.

## How Java Works

Java source code such as `Main.java` is compiled by the Java compiler (`javac`) into bytecode by producing a `.class` file. The bytecode can run on any platform that has a compatible Java Virtual Machine (JVM). This is the idea behind Java's **"write once, run anywhere"** approach.

The JVM executes the bytecode and can translate/compile it into native machine instructions that can be executed by the CPU.

- *JVM (Java Virtual Machine)* — executes Java bytecode.
- *JRE (Java Runtime Environment)* — provides the JVM and libraries needed to run Java applications.
- *JDK (Java Development Kit)* — provides the tools needed to develop Java applications, including the compiler (`javac`) and the Java runtime components.

### Java Execution Flow

```text
Main.java
    ↓
  javac
    ↓
Main.class
 (bytecode)
    ↓
   JVM
    ↓
Native machine instructions
    ↓
   CPU
```

### JVM Internals Overview

After the compilation of a Java program, there is a file with the **`.class`** extension. It contains the Java bytecode. In order to execute the code, it needs to get loaded it into the JVM. When the JVM executes a program, it translates the bytecode into platform-native code.

The JVM mainly performs the following activities:

- Loads bytecode
- Verifies bytecode
- Executes bytecode
- Provides the runtime environment

The following image illustrates a common JVM architecture:

![JVM Architecture](./img/jvm-architecture.svg)


#### The Class Loader Subsystem

This subsystem loads the Java bytecode for execution, verifies it and then allocates memory for the bytecode. 
To verify bytecode, there is a module called the **bytecode verifier**. It checks that the instructions don't require any dangerous actions, such as accessing private fields and methods of classes and objects.


#### The Runtime Data Areas

This **subsystem** represents **JVM memory**. The areas are used for different purposes during program execution.

- **PC register** — holds the address of the currently executing instruction.
- **Stack area** — a memory area where method calls and local variables are stored.
- **Native method stack** — stores native method information.
- **Heap** — stores all created objects (instances of classes).
- **Method area** — stores class-level information such as the class name, immediate parent class name, method information     and static variables.

Every thread has its own **PC register**, **stack** and **native method stack** but all threads share the same **heap** and **method area**.


#### Execution Engine

The execution engine is responsible for executing the program (bytecode). It interacts with various data areas of the JVM while executing bytecode.

The execution engine has the following parts:

- **Bytecode interpreter** — interprets the bytecode line by line and executes it (rather slowly).
- **Just-in-time compiler (JIT compiler)** — translates bytecode into native machine language while executing the program.     It executes the program faster than the interpreter.
- **Garbage collector** — cleans unused objects from the heap. Different JVM implementations can contain both a **bytecode     interpreter** and a **just-in-time compiler**, or only one of them.
- 

#### Interfaces and Libraries

Other important parts of the JVM for execution include:

- **Native Method Interface** — provides an interface between Java code and native method libraries.
- **Native Method Library** — consists of C/C++ files that are required for the execution of native code.

---

## Code Summary

### Java Program Structure

A Java program is made up of classes, methods, statements and expressions. A simple Java program looks like this:

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("I'm Learning Java!");
    }
}
```

- `class` — a blueprint that can contain data and behavior. Java code is organized into classes.
- `Main` — the name of the class.
- `public` — an access modifier that allows something to be accessed from other classes.
- `static` — means the method belongs to the class rather than a particular object.
- `void` — means the method does not return a value.
- `main()` — the entry point of a Java application. Program execution starts here.
- `String[] args` — an array of strings that can contain command-line arguments.
- `System.out` — provides access to the standard output stream.
- `print()` — prints something.
- `println()` — prints something and moves to the next line.

---

### Statements

A statement is an instruction that tells the program to perform an action. For example:

```java
int age = 24;
System.out.print(age);
```

The semicolon (`;`) marks the end of a statement in Java.

---

### Variables and Data Types

A variable is a named place used to store a value. Every variable has a **data type**, which determines what kind of value it can hold.

```java
int age = 24;
String name = "Taneem";
boolean isAdult = true;
```

- `age` is an `int`.
- `name` is a `String`.
- `isAdult` is a `boolean`.

Java has two broad categories of types:

**Primitive types** store simple values directly, such as:

```text
byte
short
int
long
float
double
char
boolean
```

**Reference types** refer to objects, such as `String` and arrays.

---

### Output

Java provides `System.out.print()` and `System.out.println()` to display output.

`print()` displays the value without automatically moving to the next line.

`println()` displays the value and then moves to the next line.

```java
System.out.print("I'm Learning");
System.out.print("Java!");
```

Output:

```text
I'm Learning Java!
```

While:

```java
System.out.println("I'm Learning");
System.out.println("Java!");
```

Output:

```text
I'm Learning
Java!
```

---

### `println()` and `\n`

`println()` can be used to output a statement and move to the next line.

Instead of `println()`, the escape character `\n` can be used inside a string to move to the next line.

Strings can be concatenated by putting `+` between them.

```java
public class Main {
    public static void main(String[] args) {
        System.out.print("I'm Learning\n" + "Java!");
    }
}
```

Output:

```text
I'm Learning
Java!
```

**Background:** A string is a sequence of characters. In Java, `String` is a class and therefore a reference type.

---

### Variables and `var`

Java normally requires the data type to be explicitly written when declaring a variable:

```java
String language = "Java";
int version = 10;
```

`var` can be used instead of explicitly writing the type for **local variables**.

This feature, called **local variable type inference**, was introduced in Java 10.

```java
var language = "Java"; // String
var version = 10;      // int
```

The compiler determines the type from the value assigned to the variable.

`var` does not make Java dynamically typed.

```java
var language = "Java";

language = 10; // Error
```

The compiler has inferred `language` as a `String`, so an `int` cannot be assigned to it.

---

### Comparing Values

For primitive types, `==` compares values:

```java
int a = 10;
int b = 10;

System.out.println(a == b); // true
```

Reference types work differently. With reference types, `==` checks whether two references point to the same object.

For comparing the contents of objects, `equals()` can be used when the class provides an appropriate implementation.

```java
String s1 = new String("java");
String s2 = new String("java");
String s3 = s2;

System.out.println(s1 == s2);      // false
System.out.println(s1.equals(s2)); // true
System.out.println(s2 == s3);      // true
```

Here:

- `s1` and `s2` contain the same text but refer to different objects.
- `s3` refers to the same object as `s2`.
- Therefore, `s1 == s2` is `false`.
- `s1.equals(s2)` is `true` because their contents are equal.
- `s2 == s3` is `true` because both references point to the same object.

---

### Escape Characters

An escape sequence starts with a backslash (`\`) and gives special meaning to the following character inside a string.

Common escape sequences include:

| Escape | Meaning |
|---|---|
| `\n` | New line |
| `\t` | Tab |
| `\"` | Double quotation mark |
| `\\` | Backslash |

Example:

```java
System.out.println("Name:\tJohn\nAge:\t24");
```

Output:

```text
Name:   John
Age:    24
```

---

### Comments

Comments are notes written inside source code. They are ignored by the compiler and do not affect the program's execution.

A single-line comment starts with `//`:

```java
// This is a comment
int age = 24;
```

A multi-line comment starts with `/*` and ends with `*/`:

```java
/*
    This is a
    multi-line comment.
*/
```

---

### User Input with `Scanner`

Java can receive input from the user using the `Scanner` class. It is available in the `java.util` package, so it needs to be imported before it can be used.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        String name = scanner.next();

        System.out.println("Hello, " + name);

        scanner.close();
    }
}
```

`System.in` represents the standard input, while `Scanner` provides methods for reading different types of input.

Some commonly used methods are:

| Method | Reads |
|---|---|
| `next()` | The next word/token |
| `nextLine()` | The entire current line |
| `nextInt()` | An integer |
| `nextDouble()` | A decimal number |

For example:

```java
String name = scanner.next();
int age = scanner.nextInt();
double height = scanner.nextDouble();
```

`next()` reads input separated by whitespace, while `nextLine()` reads everything until the end of the current line.

For example, if the input is:

```text
Mahbubur Rahman
```

then:

```java
scanner.next();     // Mahbubur
scanner.next();     // Rahman
```

while:

```java
scanner.nextLine(); // Mahbubur Rahman
```

**Background:** `Scanner` is a class provided by Java's standard library. It can read input from different sources, including keyboard input through `System.in`.

---

### Arithmetic Operators

Arithmetic operators are used to perform mathematical calculations in Java. Java provides five **binary arithmetic operators**: addition `+`, subtraction `-`, multiplication `*`, division `/`, and remainder `%`.

```java
System.out.println(13 + 25); // 38
System.out.println(70 - 30); // 40
System.out.println(21 * 3);  // 63
```

Binary operators are called **binary** because they take two values as operands.

When two integer values are divided using `/`, Java returns only the **integer part** of the result. The fractional part is discarded.

```java
System.out.println(8 / 3);  // 2
System.out.println(41 / 5); // 8
```

The `%` operator returns the **remainder** of a division.

```java
System.out.println(10 % 3); // 1
System.out.println(12 % 4); // 0
System.out.println(5 % 9);  // 5
```

---

### Expressions

Multiple arithmetic operations can be combined to create more complex **expressions**.

```java
System.out.println(1 + 3 * 4 - 2); // 11
```

Java follows a specific **precedence order** when evaluating expressions. Multiplication, division and remainder have a higher precedence than addition and subtraction.

**Parentheses** can be used to specify the order of execution and can also be nested.

```java
System.out.println((1 + 3) * (4 - 2)); // 8
```

---

### Unary Operators

A **unary operator** takes a single value as its operand.

The **unary plus** operator indicates a positive value. It is optional.

```java
System.out.println(+5); // 5
```

The **unary minus** operator negates a value or an expression.

```java
System.out.println(-8);          // -8
System.out.println(-(100 + 4));  // -104
```

Unary plus and unary minus have a higher precedence than multiplication and division.

---

### Precedence

Java has a precedence order for arithmetic operators from **highest to lowest**:

1. Parentheses `()`
2. Unary plus/minus `+` `-`
3. Multiplication, division, and remainder `*` `/` `%`
4. Addition and subtraction `+` `-`

Example of arithmetic operations:

```java
public class Expressions {
    public static void main(String[] args) {
        int a = 5, b = 11;
        System.out.println(b + a); // Prints 16

        System.out.println(b - a); // Prints 6

        System.out.println(b * a); // Prints 55

        System.out.println(b / a); // Prints 2

        System.out.println(b % a); // Prints 1

        System.out.println((a - b) + a * (b - a) - a % b); // Prints 19

    }
}
```

---

### Integer Types

Java provides integer types for representing whole numbers including positive, negative, and zero. The most commonly used types are `int` and `long`. `int` can store a smaller range of numbers while `long` can store much larger values.

```java
int two = 2;
int ten = 10;

int twelve = two + ten; // 12
int eight = ten - two;  // 8
int twenty = two * ten; // 20
int five = ten / two;   // 5
int zero = ten % two;   // 0

int minusTwo = -two; // -2
```

An `int` variable can also be printed using `System.out.println()`.

```java
int number = 100;
System.out.println(number); // 100
```

---

### Long

The `long` type is used for integer values that are too large for `int`. The underscore `_` can be used to separate groups of digits to make large numbers easier to read.

```java
long one = 1L;
long twentyTwo = 22L;
long bigNumber = 100_000_000_000L;

long result = bigNumber + twentyTwo - one;
System.out.println(result); // 100000000021
```

A number ending with `L` or `l` is treated as a `long`. Otherwise, an integer literal is treated as an `int`.

```java
int bigNumber = 5_000_000_000; // Does not compile
```

The value is too large for an `int` but adding `L` makes it a `long`.

```java
long bigNumber = 5_000_000_000L; // Compiles successfully
```

---

### Assignment Operators

The assignment operator `=` assigns a value to a variable.

```java
int n = 10;
n = n + 4; // 14
```

Java also provides **compound assignment operators** that combine an operation with assignment. For example, `+=` can be used instead of repeating the variable name.

```java
int n = 10;
n += 4; // 14
```

Other compound assignment operators include:

```text
+=
-=
*=
/=
%=
```

---

### Increment and Decrement Operators

Java has two opposite operations called **increment** (`++`) and **decrement** (`--`) which increase or decrease the value of a variable by one.

```java
int n = 10;
n++; // 11
n--; // 10
```

The code above is equivalent to:

```java
int n = 10;
n += 1; // 11
n -= 1; // 10
```

---

### Prefix and Postfix Forms

Both increment and decrement operators have two forms:

- **Prefix** (`++n` or `--n`) changes the value of a variable **before** it is used.
- **Postfix** (`n++` or `n--`) changes the value of a variable **after** it is used.

#### Prefix Increment

```java
int a = 4;
int b = ++a;

System.out.println(a); // 5
System.out.println(b); // 5
```

Here, `a` is incremented first and then its new value is assigned to `b`.

#### Postfix Increment

```java
int a = 4;
int b = a++;

System.out.println(a); // 5
System.out.println(b); // 4
```

Here, the original value of `a` is assigned to `b` first and then `a` is incremented. Therefore, `b` is `4` and `a` is `5`.

The same prefix and postfix behavior applies to the decrement operator.

```java
int a = 4;
int b = --a; // a = 3, b = 3

int x = 4;
int y = x--; // x = 3, y = 4
```

For example:

```java
int a = 16;
int b = 4;
int remainder = --a % b++;
System.out.println(remainder); // Prints 3
```

---

### Boolean Type

The `boolean` is a data type that has only two possible values: `true` and `false`. It is also known as the **logical type**.

```java
boolean open = true;
boolean closed = false;

System.out.println(open);   // true
System.out.println(closed); // false
```

A `boolean` variable cannot store an integer value. In Java, `0` is not the same as `false`.

---

### Logical Operators

Boolean variables are often used to build logical expressions. Java has four logical operators: **NOT**, **AND**, **OR** and **XOR**.

**NOT** `!` is a unary operator that reverses a boolean value.

```java
boolean f = false;
boolean t = !f; // true
```

**AND** `&&` is a binary operator that returns `true` only when both operands are `true`.

```java
boolean b1 = false && false; // false
boolean b2 = false && true;  // false
boolean b3 = true && false;  // false
boolean b4 = true && true;   // true
```

**OR** `||` is a binary operator that returns `true` when at least one operand is `true`.

```java
boolean b1 = false || false; // false
boolean b2 = false || true;  // true
boolean b3 = true || false;  // true
boolean b4 = true || true;   // true
```

**XOR** `^` (exclusive OR) is a binary operator that returns `true` when the operands have different values. It returns `false` when they have the same value.

```java
boolean b1 = false ^ false; // false
boolean b2 = false ^ true;  // true
boolean b3 = true ^ false;  // true
boolean b4 = true ^ true;   // false
```

---

### Logical Operator Precedence

The logical operators are evaluated in the following order from **highest to lowest precedence**:

1. `!` — NOT
2. `^` — XOR
3. `&&` — AND
4. `||` — OR

For example:

```java
boolean b = true && !false; // true
```

Here, `!false` is evaluated first, producing `true` and then `true && true` produces `true`.

Parentheses can be used to change the order of execution.

---

### Short-Circuit Evaluation

The `&&` and `||` operators use **short-circuit evaluation**, meaning they do not evaluate the second operand when the result can already be determined from the first operand.

```text
false && ... → false
true  || ... → true
```

For `&&`, if the first operand is `false`, the entire expression must be `false`, so the second operand is not evaluated.

For `||`, if the first operand is `true`, the entire expression must be `true`, so the second operand is not evaluated.

Short-circuit evaluation can reduce unnecessary computation and can also help avoid some errors in programs.

---

### Division and Remainder

Division can produce a whole-number quotient or a quotient with a fractional part. When one number is not a multiple of another, the division can be described using a **quotient** and a **remainder**.

For example:

```text
6 / 2 = 3
7 / 2 = 3.5
```

The number being divided is the **dividend**, the number we divide by is the **divisor**, and the result is the **quotient**.

For integer division, the relationship can be represented as:

```text
6 = 3 × 2 + 0
7 = 3 × 2 + 1
```

The last value is the **remainder**. It represents what is left after subtracting the maximum possible multiple of the divisor from the dividend.

The remainder is always a non-negative integer that is strictly less than the divisor when working with positive numbers.

---

### Modulo Division

The **modulo** operation returns the remainder of a division.

If:

```text
x = n × y + z
0 ≤ z < y
```

then:

```text
x mod y = z
```

For example:

```text
6 mod 2 = 0
7 mod 2 = 1
```

If `x` is smaller than `y`, then:

```text
x mod y = x
```

In Java, the modulo operator is written as `%`.

```java
System.out.println(10 % 3); // 1
System.out.println(12 % 4); // 0
System.out.println(5 % 9);  // 5
```

A number is divisible by another number if and only if the remainder is `0`.

```java
x % y == 0
```

For example, a number is **even** if it is divisible by `2`, so we can check it with:

```java
x % 2 == 0
```

---

### Using Modulo with Time

The modulo operator can also be used to convert a `24`-hour time to a `12`-hour format.

For example:

```text
16 mod 12 = 4
```

Because:

```text
16 = 1 × 12 + 4
```

Therefore, `16` o'clock corresponds to `4` p.m. in the `12`-hour format.

The general idea is to take the `24`-hour time modulo `12`.

---

### Why Modulo Is Useful

The modulo operator is useful in many programming tasks, such as checking divisibility, determining whether a number is even or odd, and working with repeating cycles such as time.

It is also used in areas such as **cryptography** and computations involving very large numbers. For example, knowing that:

```text
x mod 25 = 3
```

means that `x` can have the form:

```text
x = n × 25 + 3
```

where `n` is a natural number. Therefore, many different values of `x` can produce the same remainder.

> **Key takeaway:** The `%` operator gives the remainder after division. A remainder of `0` means that the dividend is divisible by the divisor.

---

### Binary Number System

The **binary numeral system**, or **base-2 numeral system**, represents numbers using only two digits: `0` and `1`. Each digit is called a **bit** (**bi**nary digi**t**).

Unlike the decimal system, which uses powers of `10`, the binary system uses powers of `2`.

For example, the decimal number `4251` can be represented as:

```text
4 × 10³ + 2 × 10² + 5 × 10¹ + 1 × 10⁰
```

A binary number works in the same way, but uses powers of `2`. For example, binary `1011` is:

```text
1 × 2³ + 0 × 2² + 1 × 2¹ + 1 × 2⁰
```

---

### Binary Counting

Binary counting uses only `0` and `1`.

| Decimal | Binary | Powers of Two |
|---:|---:|---|
| `0` | `0` | `0 × 2⁰` |
| `1` | `1` | `1 × 2⁰` |
| `2` | `10` | `1 × 2¹ + 0 × 2⁰` |
| `3` | `11` | `1 × 2¹ + 1 × 2⁰` |
| `4` | `100` | `1 × 2² + 0 × 2¹ + 0 × 2⁰` |
| `5` | `101` | `1 × 2² + 0 × 2¹ + 1 × 2⁰` |
| `6` | `110` | `1 × 2² + 1 × 2¹ + 0 × 2⁰` |
| `7` | `111` | `1 × 2² + 1 × 2¹ + 1 × 2⁰` |
| `8` | `1000` | `1 × 2³ + 0 × 2² + 0 × 2¹ + 0 × 2⁰` |

For example, decimal `5` is binary `101` because:

```text
1 × 2² + 0 × 2¹ + 1 × 2⁰
= 4 + 0 + 1
= 5
```

In binary counting, when a digit reaches `1`, the next number resets that digit to `0` and increases the digit to its left.

---

### Zero Padding

**Zero padding** means adding insignificant zeros to the left side of a binary number. It does not change the value of the number.

```text
11  → 0011
101 → 0101
```

Common fixed-length formats include:

- **Triads:** `000`, `001`, `010`
- **Tetrads:** `0110`, `0111`
- **8-digit numbers:** `00000000`, `01010101`

---

### Binary in Computers

Modern digital devices use the binary number system because computer hardware can represent two different states. Components such as transistors can switch between these two states.

Computer memory is also represented using binary values. Information is commonly grouped into **8 bits**, which is called a **byte**.

An 8-bit binary number can represent **256 different values**, from `0` to `255`.

This way of storing information is called **binary code** and is used to represent many types of data.

---

### Binary Encoding

Text can be represented using binary encoding. For example, **ASCII** (American Standard Code for Information Interchange) originally represented each character using 7 bits. Later, ASCII was modified to use 8 bits.

For example, lowercase `a` can be represented as:

```text
1100001
```

Colors can also be represented using binary values. The **RGB** (Red, Green, Blue) color system uses three values, one for each color component.

For example:

```text
(11111111, 00000000, 00000000)
```

represents pure red, with no green or blue component.

In general, binary code can be used to represent many different types of information.

---

### Binary Addition

Binary addition works like normal column addition, but the only digits are `0` and `1`.

Write the larger number on top, align both numbers to the right, and add from **right to left**.

Binary place values are powers of 2:

```text
... 2³  2²  2¹  2⁰
```
---

### Binary Addition Rules

The basic rules are:

```text
0 + 0 = 0
0 + 1 = 1
1 + 0 = 1
1 + 1 = 10
```

`10` is binary for decimal `2`.

When `1 + 1` produces `10`, write `0` in the current position and **carry `1`** to the next position.

For example:

```text
  1011
+ 0001
------
  1100
```

The carried `1` is added to the next column.

---

### Carrying in Binary Addition

Consider:

```text
  1011
+ 0111
------
```

Start from the right:

```text
1 + 1 = 10
```

Write `0` and carry `1`.

The next column becomes:

```text
1 + 1 + 1 = 11
```

Write `1` and carry `1` again.

Continue the same process until all columns are calculated.

The result is:

```text
  1011
+ 0111
------
 10010
```

Check in decimal:

```text
1011₂ = 11
0111₂ = 7

11 + 7 = 18

18₁₀ = 10010₂
```

---

### Binary Subtraction

Binary subtraction also works like decimal column subtraction.

Write the larger number on top, align the numbers to the right, and subtract from **right to left**.

The basic rules are:

```text
0 - 0 = 0
1 - 1 = 0
1 - 0 = 1
10 - 1 = 1
```

---

### Borrowing in Binary Subtraction

When we need to calculate:

```text
0 - 1
```

we cannot subtract `1` directly from `0`, so we **borrow `1` from the next digit**.

In binary, borrowing `1` gives us `10₂`, which equals decimal `2`.

Therefore:

```text
10₂ - 1₂ = 1₂
```

For example:

```text
  1100
- 0001
------
  1011
```

The borrowing process is similar to decimal subtraction, but the borrowed value is `10₂` instead of `10₁₀`.

---

### Borrowing Multiple Times

Sometimes there are several zeros between the digit we need to borrow from and the current digit.

For example:

```text
10000₂ - 1₂
```

We need to borrow through the zeros.

The result is:

```text
01111₂
```

So:

```text
10000₂ - 1₂ = 01111₂
```

or simply:

```text
10000₂ - 1₂ = 1111₂
```

---

### Checking Binary Calculations

A useful way to verify binary addition or subtraction is to convert the numbers to decimal.

For example:

```text
11010110₂ = 214
111010₂   = 58

214 - 58 = 156
```

And:

```text
156₁₀ = 10011100₂
```

Therefore:

```text
11010110₂ - 111010₂ = 10011100₂
```

The same method can be used to check binary addition.

---

### Key Points

- Binary addition and subtraction use the same **column method** as decimal arithmetic.
- Always calculate from **right to left**.
- In addition, `1 + 1 = 10₂`, **carry `1`**.
- In subtraction, when `0 - 1` occurs, **borrow `1`** from the next position.
- A borrowed `1` in binary gives `10₂`, which equals decimal `2`.
- Leading zeros can be added to make numbers easier to align.
- Converting the final answer to decimal is a useful way to check the calculation.

---

### Implicit Casting

**Implicit casting** is when Java automatically converts a value from one data type to another without requiring the programmer to write the conversion explicitly.

It generally works when the **target type is wider** than the source type, meaning it can represent all possible values of the source type.

For example:

```java
int num = 100;
long bigNum = num; // 100
```

Here, Java automatically converts the `int` value to `long`.

---

### Common Implicit Castings

Some common widening conversions are:

```text
byte → short → int → long → float → double
```

`char` can also be implicitly converted to an integer type such as `int`.

For example:

```java
int num = 100;
long bigNum = num;

short shortNum = 100;
int num2 = shortNum;

char ch = '?';
int code = ch; // 63
```

A value can generally be assigned implicitly to a type further along the widening conversion path.

However, the reverse direction is not automatically allowed.

For example:

```java
long bigNum = 100;
int num = bigNum; // compilation error
```

The conversion from `long` to `int` requires explicit casting.

---

### Implicit Casting and Information Loss

Widening a type does not always guarantee that the exact value will be preserved.

For example, converting an integer to `float` can cause a **loss of precision** because `float` cannot represent every large integer exactly.

```java
long bigLong = 1_200_000_002L;
float bigFloat = bigLong; // 1.2E9
```

The value is within the range of `float` but some less significant bits may be lost.

---

### `char` and Numeric Types

A `char` can be implicitly converted to an integer type.

Java uses Unicode character representation and the values `0`–`127` have the same numeric values as ASCII.

For example:

```java
char character = 'a';
char upperCase = 'A';

int code1 = character;  // 97
int code2 = upperCase;  // 65
```

So:

```text
'a' → 97
'A' → 65
'?' → 63
```

---

### Boolean Cannot Be Cast

`boolean` is not part of the numeric casting system.

For example:

```java
boolean value = true;

// int num = value; // invalid
```

---

### Explicit Casting

When Java cannot automatically perform the conversion, the programmer can use **explicit casting**.

The syntax is:

```java
(targetType) source
```

For example:

```java
double d = 2.00003;

long l = (long) d; // 2
```

The cast from `double` to `long` removes the fractional part.

---

### Examples of Explicit Casting

```java
double d = 2.00003;

long l = (long) d; // 2

int i = (int) l; // 2

int val = (int) (3 + 2L); // 5

char ch = (char) 55L; // '7'
```

Explicit casting is required when converting from a wider type to a narrower type.

---

### Narrowing Can Lose Information

A narrower type may not be able to represent the original value.

For example:

```java
long bigNum = 100_000_000_000_000L;
int n = (int) bigNum;
```

The resulting `int` does not contain the original value.

---

### Type Overflow

When a value cannot be represented correctly by the target type, the conversion can result in **overflow** or loss of information.

For example:

```java
long bigNum = 100_000_000_000_000L;
int n = (int) bigNum;
```

The `long` can store a much larger range of values than `int`, so converting a large `long` to `int` can produce a different value.

The same issue can occur when converting:

```text
long → int
int  → short
int  → byte
```

Before narrowing a value, make sure the value can safely fit inside the target type.

---

### Explicit Casting Can Also Be Used for Widening

Explicitly casting even when Java would perform the conversion automatically.

```java
int num = 10;
long bigNum = (long) num;
```

However, this is unnecessary because Java already allows:

```java
int num = 10;
long bigNum = num;
```

Therefore, unnecessary explicit casts should generally be avoided.

---

### Key Points

- **Implicit casting** is automatic conversion performed by Java.
- It normally happens when converting from a **narrower type to a wider type**.
- Example: `int → long`.
- **Explicit casting** requires the programmer to specify the target type.
- Syntax: `(targetType) value`
- Example: `(int) 3.14` produces `3`.
- Narrowing conversions can cause **loss of information or precision**.
- `char` can be converted to numeric types.
- `boolean` cannot be cast to or from numeric types.
- Explicit casting is unnecessary when Java already performs the conversion implicitly.

---


