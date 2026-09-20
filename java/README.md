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

