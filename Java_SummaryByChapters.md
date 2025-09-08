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
