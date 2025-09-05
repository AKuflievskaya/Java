# 📚 Complete Java Command Guide

A fully categorized and explained list of typical Java commands, structures, and keywords. Includes a vocabulary section at the end.

---

## 🛠️ 1. Basic Commands

| Command/Keyword         | Description |
|--------------------------|-------------|
| `public`                | Access modifier: makes the class/method accessible from anywhere. |
| `class`                 | Declares a new class. |
| `static`                | Indicates that a method or variable belongs to the class, not instances. |
| `void`                  | Specifies that the method doesn't return any value. |
| `main`                  | Entry point method for a Java application. |
| `System.out.println()`  | Prints text to the console. |
| `import`                | Imports a class or package. |
| `package`               | Declares the package a class belongs to. |

**Example:**

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
```

---

## 🧮 2. Primitive Data Types

| Type      | Size   | Example              | Use |
|-----------|--------|----------------------|-----|
| `int`     | 32-bit | `int age = 25;`      | Whole numbers |
| `double`  | 64-bit | `double pi = 3.14;`  | Decimal numbers |
| `float`   | 32-bit | `float x = 2.5f;`    | Smaller decimal numbers |
| `char`    | 16-bit | `char c = 'A';`      | Single characters |
| `boolean` | 1-bit  | `boolean flag = true;`| True or false |
| `long`    | 64-bit | `long big = 123456789L;`| Large integers |
| `short`   | 16-bit | `short s = 1000;`    | Small integers |
| `byte`    | 8-bit  | `byte b = 127;`      | Very small integers |

---

## 🔁 3. Control Structures

### Conditionals

```java
if (condition) {
    // Code
} else if (anotherCondition) {
    // Code
} else {
    // Code
}
```

```java
switch (variable) {
    case value1:
        // Code
        break;
    case value2:
        // Code
        break;
    default:
        // Code
}
```

### Loops

```java
while (condition) {
    // Code
}
```

```java
do {
    // Code
} while (condition);
```

```java
for (int i = 0; i < 10; i++) {
    // Code
}
```

```java
for (Type item : collection) {
    // Code
}
```

---

## 🧰 4. Classes, Objects, and Methods

### Class Declaration

```java
public class Person {
    String name;
    int age;
}
```

### Creating Objects

```java
Person p = new Person();
p.name = "John";
p.age = 30;
```

### Methods

```java
public int add(int a, int b) {
    return a + b;
}
```

### Constructors

```java
public Person(String name, int age) {
    this.name = name;
    this.age = age;
}
```

---

## 🔒 5. Access Modifiers

| Modifier    | Description |
|-------------|-------------|
| `public`    | Accessible from any class. |
| `private`   | Accessible only within the declared class. |
| `protected` | Accessible within the same package and subclasses. |
| (default)   | Accessible within the same package. |

---

## 📦 6. Packages and Libraries

```java
package com.myapp;

import java.util.Scanner;
import java.util.ArrayList;
import java.util.HashMap;
```

### Common Packages

| Package           | Description |
|-------------------|-------------|
| `java.lang`       | Core classes like `String`, `Math`, `Object`, etc. (imported by default) |
| `java.util`       | Utilities like collections, dates, etc. |
| `java.io`         | Input and output operations. |
| `java.net`        | Networking capabilities. |
| `javax.swing`     | GUI components. |

---

## 🧵 7. Object-Oriented Programming (OOP)

| Concept          | Description |
|------------------|-------------|
| Inheritance      | One class inherits from another (`extends`). |
| Polymorphism     | Methods behave differently depending on the object. |
| Encapsulation    | Data hiding using access modifiers and getters/setters. |
| Abstraction      | Showing only the necessary features and hiding implementation. |

### Inheritance

```java
public class Animal {
    void makeSound() {
        System.out.println("Generic sound");
    }
}

public class Dog extends Animal {
    void makeSound() {
        System.out.println("Woof");
    }
}
```

### Interfaces

```java
interface Flyable {
    void fly();
}

class Bird implements Flyable {
    public void fly() {
        System.out.println("Bird is flying");
    }
}
```

---

## 🧱 8. Collections Framework

| Collection         | Description |
|--------------------|-------------|
| `ArrayList`        | Resizable array. |
| `LinkedList`       | Doubly linked list. |
| `HashMap`          | Key-value pair mapping. |
| `HashSet`          | Set with no duplicates. |
| `TreeMap`, `TreeSet`| Sorted map/set. |

### Example:

```java
ArrayList<String> names = new ArrayList<>();
names.add("Alice");
names.add("Bob");
```

---

## 🔄 9. Exception Handling

### Try-Catch Block

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero.");
} finally {
    System.out.println("This always executes.");
}
```

### Throwing Exceptions

```java
throw new IllegalArgumentException("Invalid argument");
```

---

## 📘 10. Java Vocabulary

| Term                | Definition |
|---------------------|------------|
| **JVM** (Java Virtual Machine) | Executes Java bytecode. |
| **JRE** (Java Runtime Environment) | Environment to run Java programs, includes JVM and libraries. |
| **JDK** (Java Development Kit) | Tools for developing Java apps (includes compiler, JRE). |
| **Bytecode**        | Compiled intermediate code (`.class` file). |
| **`javac`**         | Java compiler (compiles `.java` to `.class`). |
| **IDE**             | Integrated Development Environment (e.g., IntelliJ, Eclipse). |
| **Garbage Collector** | Automatically frees memory from unused objects. |
| **Constructor**     | Special method to initialize new objects. |
| **Instance**        | A specific object created from a class. |
| **Reference**       | A variable that points to an object in memory. |
| **Polymorphism**    | Ability to process objects differently based on their types. |
| **Encapsulation**   | Wrapping data and code into a single unit (class). |
| **Abstraction**     | Hiding implementation details, exposing only functionality. |
| **Inheritance**     | Mechanism to inherit features from another class. |

---

# ✅ Done!

This Markdown document serves as a detailed cheat sheet for Java development. Use it for reference, study, or as documentation for your learning path.

Need more advanced sections like multithreading, JavaFX, or file handling? Let me know!
