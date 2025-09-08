# Chapter 3 – Java Basics (Explained for Beginners)

## 1. Classes and Objects
In Java, **everything lives inside a class**. You create objects (instances) from classes.

```java
// Person.java
public class Person {
    // Instance field (property) - each object has its own copy
    private String name;

    // Constructor - runs when you call 'new Person("Ana")'
    public Person(String name) {
        // 'this' refers to the current object (disambiguates field vs parameter)
        this.name = name;
    }

    // Instance method - operates on the object's state
    public void sayHello() {
        System.out.println("Hello, I'm " + name);
    }

    // Entry point - demo usage
    public static void main(String[] args) {
        Person p = new Person("Ana");   // create an object
        p.sayHello();                   // call an instance method
    }
}
```

---

## 2. The `main` Method
Java programs start at a specific method signature: `public static void main(String[] args)`.

```java
public class App {
    // The JVM looks for this exact signature as the entry point
    public static void main(String[] args) {
        // Print to standard output (like console.log / print)
        System.out.println("Program started");
        // 'args' holds command-line arguments
        if (args.length > 0) {
            System.out.println("First arg: " + args[0]);
        }
    }
}
```

---

## 3. Comments
Java supports single-line, multi-line, and Javadoc comments.

```java
public class CommentsDemo {
    public static void main(String[] args) {
        // Single-line comment: explain a single statement
        int x = 10; // trailing single-line comment

        /*
         * Multi-line comment:
         * Useful for longer explanations or disabling blocks of code.
         */

        /**
         * Javadoc comment:
         * Used to generate API documentation (e.g., with javadoc tool).
         * @param args program arguments
         */
        System.out.println("Comments example: x = " + x);
    }
}
```

---

## 4. Packages and Imports
Packages group related classes; imports bring external classes into scope.

```java
// File: com/example/util/RandomExample.java
package com.example.util;           // declares this file's package (folder structure should match)

import java.util.Random;            // import a class from the Java API

public class RandomExample {
    public static void main(String[] args) {
        Random r = new Random();    // use the imported class
        int n = r.nextInt(10);      // [0..9]
        System.out.println("Random: " + n);
    }
}
```

---

## 5. Constructors
Constructors initialize new objects; their name matches the class and they have no return type.

```java
public class Animal {
    private final String kind;
    private int age;

    // No-args constructor - provides default values
    public Animal() {
        this.kind = "Unknown";
        this.age = 0;
    }

    // Parameterized constructor - customize initial state
    public Animal(String kind, int age) {
        this.kind = kind;
        this.age = age;
    }

    public void info() {
        System.out.println("Kind=" + kind + ", age=" + age);
    }

    public static void main(String[] args) {
        Animal a1 = new Animal();                // uses defaults
        Animal a2 = new Animal("Cat", 2);        // custom init
        a1.info();
        a2.info();
    }
}
```

---

## 6. Data Types
Java has **primitive types** (stored by value) and **reference types** (objects).

```java
public class TypesDemo {
    public static void main(String[] args) {
        // Primitives (fixed-size, stored directly)
        int count = 42;              // 32-bit integer
        double price = 12.99;        // 64-bit floating point
        boolean active = true;       // true/false
        char letter = 'A';           // 16-bit Unicode character

        // Reference types (objects live on the heap; variable holds a reference)
        String message = "Hello";    // String is an object (immutable)
        int[] nums = {1, 2, 3};      // Array is also an object

        System.out.println(count + ", " + price + ", " + active + ", " + letter);
        System.out.println(message + " size=" + message.length());
        System.out.println("nums[0]=" + nums[0]);
    }
}
```

---

## 7. Variables (Local, Instance, Static)
Scope and lifetime depend on where a variable is declared.

```java
public class Vars {
    // Static (class) variable: shared by all instances
    private static int createdCount = 0;

    // Instance variable: each object gets its own copy
    private final int id;

    public Vars() {
        createdCount++;      // update shared counter
        this.id = createdCount;
    }

    public void show() {
        // Local variable: exists only within this method
        String label = "Object";
        System.out.println(label + " id=" + id + ", total=" + createdCount);
    }

    public static void main(String[] args) {
        Vars v1 = new Vars();
        Vars v2 = new Vars();
        v1.show();
        v2.show();
    }
}
```

---

## 8. Scope and Initialization Order
Java enforces declaration before use; initialization follows a defined order.

```java
public class InitOrder {
    // 1) Static fields/blocks (run once when class is loaded)
    static int s = initStatic();

    static int initStatic() {
        System.out.println("Static init");
        return 100;
    }

    // 2) Instance fields/blocks (run per object, before constructor)
    int a = initA();

    int initA() {
        System.out.println("Instance field init");
        return 10;
    }

    { // Instance initializer block
        System.out.println("Instance initializer block");
    }

    // 3) Constructor (runs last for each new object)
    public InitOrder() {
        System.out.println("Constructor");
    }

    public static void main(String[] args) {
        System.out.println("Main start");
        new InitOrder();
        new InitOrder();
    }
}
```

---

## 9. Memory and Garbage Collection
The **Garbage Collector (GC)** reclaims unreachable objects automatically.

```java
public class GCDemo {
    static class Big {
        // Simulate memory usage
        private byte[] data = new byte[5_000_000];
    }

    public static void main(String[] args) {
        Big b = new Big();         // allocate a big object
        System.out.println("Allocated Big");
        b = null;                  // drop reference; object becomes eligible for GC
        System.gc();               // request GC (not guaranteed to run immediately)
        System.out.println("Requested GC");
    }
}
```

---

## 🔑 Key Takeaway
- Everything is inside classes.
- Program execution starts in `main`.
- Declare types explicitly.
- Understand variable kinds (local/instance/static) and init order.
- GC frees unreachable objects.

---

# Chapter 4 – Operators and Statements

## 1. Operators Overview
Unary (one operand), binary (two), and ternary (three) operators.

```java
public class Operators {
    public static void main(String[] args) {
        int x = 5;               // unary increment/decrement
        System.out.println(++x); // pre-increment: x becomes 6, then prints 6
        System.out.println(x--); // post-decrement: prints 6, then x becomes 5

        boolean flag = !false;   // logical NOT
        System.out.println(flag);

        int a = 2 + 3 * 4;       // precedence: * before +
        System.out.println(a);   // 14

        int b = (2 + 3) * 4;     // parentheses override precedence
        System.out.println(b);   // 20

        int max = (a > b) ? a : b; // ternary operator
        System.out.println("max=" + max);
    }
}
```

---

## 2. Arithmetic, Assignment, Casting
Use compound assignments; cast when narrowing types.

```java
public class ArithmeticCasting {
    public static void main(String[] args) {
        int x = 10;
        x += 5;                 // x = x + 5  -> 15
        x *= 2;                 // x = x * 2  -> 30

        double d = 3.9;
        int i = (int) d;        // cast double -> int (truncates to 3)
        System.out.println("i=" + i);

        // Widening conversion (safe, automatic)
        double sum = i + 2.5;   // int -> double automatically
        System.out.println("sum=" + sum);
    }
}
```

---

## 3. Relational, Equality, Logical
Comparison and boolean logic with short-circuiting.

```java
public class Comparisons {
    public static void main(String[] args) {
        int a = 5, b = 8;
        System.out.println(a < b);     // true
        System.out.println(a == 5);    // true
        System.out.println(a != b);    // true

        // Short-circuit: right side not evaluated if left decides the result
        boolean result = (a < b) && expensiveCheck();
        System.out.println("result=" + result);
    }

    static boolean expensiveCheck() {
        System.out.println("expensiveCheck called");
        return true;
    }
}
```

---

## 4. Control Flow: if/switch/loops
Classic branching and looping constructs.

```java
public class Flow {
    public static void main(String[] args) {
        int dayNum = 5;

        // if-else
        if (dayNum < 6) {
            System.out.println("Weekday");
        } else {
            System.out.println("Weekend");
        }

        // switch (supports String, int, char, etc.)
        String day = "Fri";
        switch (day) {
            case "Mon":
                System.out.println("Beginning");
                break;
            case "Fri":
                System.out.println("Almost weekend");
                break;
            default:
                System.out.println("Midweek");
        }

        // while
        int i = 0;
        while (i < 3) {
            System.out.println("while i=" + i++);
        }

        // do-while (runs at least once)
        int j = 0;
        do {
            System.out.println("do-while j=" + j++);
        } while (j < 1);

        // for
        for (int k = 0; k < 3; k++) {
            System.out.println("for k=" + k);
        }

        // enhanced for (for-each)
        String[] names = {"Ana", "Luis"};
        for (String n : names) {
            System.out.println("Hello " + n);
        }
    }
}
```

---

## 5. break / continue / labels
Control loop execution precisely.

```java
public class BreakContinue {
    public static void main(String[] args) {
        // continue skips this iteration
        for (int i = 1; i <= 3; i++) {
            if (i == 2) continue;
            System.out.println("i=" + i); // prints 1 and 3
        }

        // break exits the loop
        for (int j = 1; j <= 3; j++) {
            if (j == 2) break;
            System.out.println("j=" + j); // prints 1
        }

        // labeled break: exit outer loop from inner loop
        outer:
        for (int r = 1; r <= 2; r++) {
            for (int c = 1; c <= 3; c++) {
                if (c == 2) break outer; // jumps out of both loops
                System.out.println("r=" + r + ", c=" + c);
            }
        }
    }
}
```

---

# Chapter 5 – Java API Essentials

## 1. String (Immutable)
Strings are immutable: modifications create new objects.

```java
public class StringDemo {
    public static void main(String[] args) {
        String s = "  hello  ";
        String t = s.trim().toUpperCase().concat("!");
        // s unchanged; t is a new String
        System.out.println("s='" + s + "'");
        System.out.println("t='" + t + "'");
        System.out.println("Length=" + t.length());
        System.out.println("Starts with HE? " + t.startsWith("HE"));
        System.out.println("Substring(0,2)=" + t.substring(0, 2));
    }
}
```

---

## 2. StringBuilder (Mutable)
Use for efficient concatenation in loops.

```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder(64); // optional capacity
        for (int i = 1; i <= 5; i++) {
            if (i > 1) sb.append('-');
            sb.append(i);
        }
        System.out.println(sb.toString()); // 1-2-3-4-5
    }
}
```

---

## 3. Arrays
Fixed-size; index-based access; can be multi-dimensional.

```java
import java.util.Arrays;

public class ArraysDemo {
    public static void main(String[] args) {
        int[] a = {3, 1, 2};
        Arrays.sort(a);                      // in-place sort
        System.out.println(Arrays.toString(a));

        int idx = Arrays.binarySearch(a, 2); // requires sorted array
        System.out.println("Index of 2 = " + idx);

        int[][] grid = {{1,2}, {3,4}};       // 2D array
        System.out.println(grid[1][0]);      // 3
    }
}
```

---

## 4. ArrayList (Resizable List)
Use generics for type safety; stores references (wrappers for primitives).

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        System.out.println(list.get(0));     // "A"
        System.out.println(list.contains("B"));
        list.remove("A");                    // remove by value
        System.out.println("Size=" + list.size());

        // Autoboxing: int -> Integer
        ArrayList<Integer> nums = new ArrayList<>();
        nums.add(10);                        // auto-boxed
        System.out.println(nums);
    }
}
```

---

## 5. Dates and Times (java.time)
Modern, immutable, timezone-aware types.

```java
import java.time.*;
import java.time.format.DateTimeFormatter;

public class TimeDemo {
    public static void main(String[] args) {
        LocalDate d = LocalDate.of(2025, 9, 8);
        LocalTime t = LocalTime.now();
        LocalDateTime dt = LocalDateTime.now();
        ZonedDateTime zdt = ZonedDateTime.now(ZoneId.systemDefault());

        // Arithmetic
        LocalDate nextWeek = d.plusWeeks(1);
        LocalTime minusHour = t.minusHours(1);

        // Format / parse
        DateTimeFormatter f = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String ds = d.format(f);
        LocalDate parsed = LocalDate.parse(ds, f);

        System.out.println("d=" + d + ", nextWeek=" + nextWeek);
        System.out.println("t=" + t + ", minusHour=" + minusHour);
        System.out.println("zdt=" + zdt);
        System.out.println("formatted=" + ds + ", parsed=" + parsed);
    }
}
```

---

# Chapter 6 – Methods and Encapsulation

## 1. Method Structure
Signature = modifiers + return type + name + parameters + exceptions + body.

```java
public class Methods {
    // 'public' visible everywhere, 'static' belongs to class, returns int, takes two ints, throws nothing
    public static int add(int a, int b) {
        return a + b;
    }

    // Example with checked exception declaration
    public static void nap(long ms) throws InterruptedException {
        Thread.sleep(ms); // could throw InterruptedException, so we declare 'throws'
    }

    public static void main(String[] args) throws InterruptedException {
        System.out.println(add(2, 3));
        nap(100);
    }
}
```

---

## 2. Varargs
Variable-length argument lists compiled as arrays.

```java
public class VarargsDemo {
    static String joinWithComma(String... parts) {
        // 'parts' is an array inside the method
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < parts.length; i++) {
            if (i > 0) sb.append(", ");
            sb.append(parts[i]);
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        System.out.println(joinWithComma("A", "B", "C"));
        System.out.println(joinWithComma()); // empty -> ""
    }
}
```

---

## 3. Access Modifiers
Control visibility and encapsulation.

```java
public class Access {
    private int secret = 42;   // only this class
            int pkgVal = 1;    // package-private (no modifier)
    protected int semi = 2;    // package + subclasses
    public int open = 3;       // everywhere

    public int getSecret() {   // controlled access to private data
        return secret;
    }
}
```

---

## 4. Static vs Instance
Static (class-level) vs instance (object-level) members.

```java
public class Counter {
    private static int total = 0; // shared counter
    private final int id;         // unique per object

    public Counter() {
        id = ++total;             // increment shared counter, assign id
    }

    public void show() {
        System.out.println("id=" + id + ", total=" + total);
    }

    public static void main(String[] args) {
        Counter c1 = new Counter();
        Counter c2 = new Counter();
        c1.show();
        c2.show();
    }
}
```

---

## 5. Pass-by-Value (Important)
Java always passes **values**: for objects, the **reference value** is copied.

```java
public class PassByValue {
    static class Box { int v; }

    static void mutate(Box b) { b.v = 99; }          // modifies the object pointed to by the reference copy
    static void reassign(Box b) { b = new Box(); }   // changes only local copy of the reference (caller unaffected)

    public static void main(String[] args) {
        Box b = new Box();
        b.v = 10;
        mutate(b);
        System.out.println(b.v); // 99 (object mutated)

        reassign(b);
        System.out.println(b.v); // still 99 (original reference unchanged)
    }
}
```

---

## 6. Overloading
Same method name, different parameter lists.

```java
public class Overload {
    public void log(String msg)  { System.out.println("S: " + msg); }
    public void log(int code)    { System.out.println("I: " + code); }
    public void log(String m, int c) { System.out.println("S+I: " + m + " " + c); }

    public static void main(String[] args) {
        Overload o = new Overload();
        o.log("hello");
        o.log(200);
        o.log("ok", 200);
    }
}
```

---

## 7. Constructors and `this()`
Chain constructors for DRY initialization.

```java
public class Dog {
    private final String name;
    private final int age;

    public Dog() {
        this("NoName", 0);         // calls the other constructor (must be first line)
    }

    public Dog(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void info() {
        System.out.println(name + " (" + age + ")");
    }

    public static void main(String[] args) {
        new Dog().info();
        new Dog("Rex", 5).info();
    }
}
```

---

## 8. Encapsulation & Immutability
Hide fields; expose controlled access; prefer immutable data where reasonable.

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public final class Team {
    private final String name;         // immutable
    private final List<String> members;// defensive copies for collections

    public Team(String name, List<String> members) {
        this.name = name;
        // Create an unmodifiable copy to protect internal state
        this.members = Collections.unmodifiableList(new ArrayList<>(members));
    }

    public String getName() { return name; }
    public List<String> getMembers() { return members; } // returns safe unmodifiable view
}
```

---

# Chapter 7 – Class Design

## 1. Inheritance Basics
A class can extend a single parent; it inherits accessible members.

```java
class Animal {
    private int age;
    public int getAge() { return age; }
    public void setAge(int a) { this.age = a; }
}

class Lion extends Animal {
    public void roar() {
        // getAge() is inherited (public in parent)
        System.out.println("Roar! I am " + getAge() + " years old");
    }
}
```

---

## 2. Class Visibility & File Rules
One public top-level class per file; file name must match the public class.

```java
// File: Zoo.java
public class Zoo { } // this file must be named Zoo.java
// package-private (no modifier) classes can share the file but are less common for beginners
class Pen { }
```

---

## 3. Constructors & `super()`
Constructors can call parent constructors; if omitted, `super()` is inserted.

```java
class Base {
    Base() { System.out.println("Base ctor"); }
}

class Derived extends Base {
    Derived() {
        super();               // calls Base()
        System.out.println("Derived ctor");
    }

    public static void main(String[] args) {
        new Derived();
    }
}
```

---

## 4. Overriding Methods
Child replaces parent behavior; annotate with `@Override`.

```java
class Bird {
    public void fly() { System.out.println("Bird flying"); }
}
class Eagle extends Bird {
    @Override
    public void fly() { System.out.println("Eagle soaring"); }
}
```

---

## 5. Abstract Classes
Cannot be instantiated; may contain abstract methods.

```java
abstract class Shape {
    abstract double area(); // must be implemented by concrete subclasses
}
class Circle extends Shape {
    private final double r;
    Circle(double r){ this.r = r; }
    double area(){ return Math.PI * r * r; }
}
```

---

## 6. Interfaces (Contracts)
Classes implement interfaces; can implement multiple interfaces.

```java
interface CanFly { void fly(); }

class Sparrow implements CanFly {
    @Override
    public void fly() {
        System.out.println("Sparrow flaps!");
    }
}
```

---

## 7. Polymorphism & Casting
Reference type controls visible methods; runtime type controls implementation.

```java
class Animal2 { void sound(){ System.out.println("..."); } }
class Dog2 extends Animal2 { @Override void sound(){ System.out.println("Woof"); } }

public class Poly {
    public static void main(String[] args) {
        Animal2 a = new Dog2(); // upcast (implicit)
        a.sound();              // "Woof" (dynamic dispatch)

        // Downcast (explicit) - only safe if object is actually that type
        if (a instanceof Dog2) {
            Dog2 d = (Dog2) a;
            d.sound();
        }
    }
}
```

---

## 8. Lambdas (Intro with Functional Interfaces)
Use lambdas with interfaces that have a single abstract method.

```java
import java.util.Arrays;
import java.util.List;

public class LambdasIntro {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("a", "b", "c");
        // s -> System.out.println(s) is a lambda implementing Consumer<String>#accept
        list.forEach(s -> System.out.println(s));
    }
}
```

---

# Chapter 8 – Exceptions

## 1. Throwing & Declaring
`throw` raises an exception; `throws` declares it to callers.

```java
public class Throwing {
    static void risky() throws Exception {
        // Signal an error condition to the caller
        throw new Exception("Something went wrong");
    }

    public static void main(String[] args) {
        try {
            risky();
        } catch (Exception e) {
            System.out.println("Handled: " + e.getMessage());
        }
    }
}
```

---

## 2. Checked vs Unchecked vs Errors
- **Checked** (subclasses of `Exception`, excluding `RuntimeException`): must handle or declare.
- **Unchecked** (`RuntimeException` and its subclasses): optional to declare.
- **Errors** (`Error`): serious problems; generally do not catch.

```java
public class Kinds {
    static void checkedExample() throws java.io.IOException {
        // Checked: must be declared or handled
        throw new java.io.IOException("I/O failed");
    }

    static void uncheckedExample() {
        // Unchecked: no need to declare; may happen at runtime
        throw new IllegalArgumentException("Bad argument");
    }
}
```

---

## 3. try-catch-finally
Catch specific exceptions and use `finally` for cleanup.

```java
import java.io.*;

public class TryCatchFinally {
    public static void main(String[] args) {
        BufferedReader br = null;
        try {
            br = new BufferedReader(new FileReader("data.txt"));
            System.out.println(br.readLine());
        } catch (FileNotFoundException e) {
            System.out.println("File not found");
        } catch (IOException e) {
            System.out.println("I/O error");
        } finally {
            // Always attempt to close resources
            try {
                if (br != null) br.close();
            } catch (IOException e) {
                // If closing fails, log and move on
                System.out.println("Close failed");
            }
        }
    }
}
```

> Tip: Prefer **try-with-resources** for auto-closing resources.

```java
import java.io.*;

public class TryWithResources {
    public static void main(String[] args) {
        // The resource is closed automatically at the end of the try block
        try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
            System.out.println(br.readLine());
        } catch (IOException e) {
            System.out.println("I/O problem: " + e.getMessage());
        }
    }
}
```

---

## 4. Printing Exceptions & Best Practices
Always log useful info; avoid swallowing exceptions silently.

```java
public class Printing {
    public static void main(String[] args) {
        try {
            Integer.parseInt("not-a-number"); // will throw NumberFormatException
        } catch (Exception e) {
            System.out.println(e);              // type + message
            System.out.println(e.getMessage()); // message only
            e.printStackTrace();                // full stack trace with call chain
        }
    }
}
```

---

## 🔑 Key Takeaways
- Use specific exception types and order `catch` from most specific to general.
- Prefer try-with-resources for I/O.
- `throw` to raise; `throws` to declare.
- Do not use exceptions for normal control flow.

