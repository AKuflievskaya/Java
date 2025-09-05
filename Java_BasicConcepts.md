# 🧠 Java Basics (for Python developers)

## 📦 Class (`class`)

A **class** in Java is like a **class in Python**: a blueprint for creating objects.

```java
public class Person {
    // Attributes (instance variables)
    String name;
    int age;

    // Method (function inside a class)
    public void greet() {
        System.out.println("Hi, my name is " + name);
    }
}
```

🟡 In Python:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        print(f"Hi, my name is {self.name}")
```

---

## 🔁 Method

A **method** in Java is a **function inside a class**, similar to methods in Python.

```java
public void greet() {
    System.out.println("Hi");
}
```

📌 Methods can have a return type (`int`, `void`, `String`, etc.) and can take parameters.

---

## 🧮 Variable

A **variable** in Java stores data. It can be inside a class, inside a method, or passed as a parameter.

```java
int age = 25;       // Local variable inside a method
String name = "Ana";
```

🔵 Variables must have a **type**: `int`, `String`, `double`, `boolean`, etc.

---

## 🔐 Instance Variable

An **instance variable** (also called a **field** or **attribute**) belongs to an **object**. It's defined inside a class but outside any methods.

```java
public class Person {
    String name;   // Instance variable
    int age;       // Instance variable
}
```

📌 Equivalent to `self.name` or `self.age` in Python.

---

## 🎯 Parameter

A **parameter** in Java is a variable passed into a method or constructor.

```java
public void greetWithName(String name) {
    System.out.println("Hi " + name);
}
```

🟢 In Python:

```python
def greet_with_name(name):
    print(f"Hi {name}")
```

---

# ✅ Quick Summary

| Java Concept             | What is it?                                           | Python Equivalent     |
|--------------------------|--------------------------------------------------------|------------------------|
| `class`                  | Blueprint for objects                                  | `class`               |
| Method                   | Function inside a class                                | Method                |
| Variable                 | Stores data (with type)                                | Variable              |
| Instance Variable        | Variable that belongs to the object (`this.variable`)  | `self.variable`       |
| Parameter                | Value passed to a method or constructor                | Parameter             |
