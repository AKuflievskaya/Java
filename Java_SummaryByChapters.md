# Java – Capítulos 3–8 (todo combinado, comentarios simples)

> Objetivo: explicaciones claras para principiantes. Copia-pega en tu `.md`.

---

# Chapter 3 – Java Basics (Explained for Absolute Beginners)

## 1) Classes and Objects
```java
// File: Person.java
// A "class" is a blueprint to build objects (like a cookie cutter).
public class Person {
    // This is a "field" (also called property or attribute).
    // Each Person object will store its own 'name' value.
    private String name;

    // Constructor = special method that runs when we create a new Person.
    // We pass the starting value for 'name'.
    public Person(String name) {
        // 'this.name' means "the field of THIS object", not the parameter.
        this.name = name;
    }

    // A normal "method" = an action the object can do.
    // Here we print a message using the stored name.
    public void sayHello() {
        System.out.println("Hello, I'm " + name);
    }

    // 'main' is the starting point when you run this file.
    public static void main(String[] args) {
        // 'new Person("Ana")' creates an object from the blueprint.
        Person p = new Person("Ana");
        // We call the object's method with the dot syntax.
        p.sayHello();
    }
}
```

---

## 2) The `main` Method
```java
// The JVM (Java Virtual Machine) looks for this exact method to start your program.
public class App {
    public static void main(String[] args) {
        // Prints text on the screen (console).
        System.out.println("Program started");

        // 'args' are the words you type after the program name in the terminal.
        // Example: java App hello world  -> args[0] = "hello"
        if (args.length > 0) {
            System.out.println("First arg: " + args[0]);
        }
    }
}
```

---

## 3) Comments
```java
public class CommentsDemo {
    public static void main(String[] args) {
        // Single-line comment: explains one line.
        int x = 10; // You can also comment at the end of a line.

        /*
         Multi-line comment:
         Good for longer explanations
         or temporary disabling of code.
        */

        /**
         * Javadoc comment:
         * Used to auto-generate documentation pages.
         * Tools read these to make nice HTML docs.
         */
        System.out.println("x = " + x);
    }
}
```

---

## 4) Packages and Imports
```java
// File path should match the package (folders): com/example/util/RandomExample.java
package com.example.util; // Groups related classes; helps avoid name conflicts.

import java.util.Random;  // Brings the Random class into this file so we can use it.

public class RandomExample {
    public static void main(String[] args) {
        Random r = new Random(); // Makes a random number generator.
        int n = r.nextInt(10);   // Gets a random number from 0 to 9.
        System.out.println("Random: " + n);
    }
}
```

---

## 5) Constructors
```java
// A constructor sets up the first values of an object.
public class Animal {
    private final String kind; // 'final' means this value cannot change after construction.
    private int age;

    // No-argument constructor: gives default values when none are provided.
    public Animal() {
        this.kind = "Unknown"; // 'this' = the current object
        this.age = 0;
    }

    // Constructor with parameters: caller chooses the values.
    public Animal(String kind, int age) {
        this.kind = kind;
        this.age = age;
    }

    public void info() {
        System.out.println("Kind=" + kind + ", age=" + age);
    }

    public static void main(String[] args) {
        Animal a1 = new Animal();              // Uses defaults.
        Animal a2 = new Animal("Cat", 2);      // Uses given values.
        a1.info();
        a2.info();
    }
}
```

---

## 6) Data Types (Primitives vs Objects)
```java
public class TypesDemo {
    public static void main(String[] args) {
        // PRIMITIVES: tiny, fixed-size boxes that hold simple values directly.
        int count = 42;        // whole number
        double price = 12.99;  // decimal number
        boolean active = true; // true or false
        char letter = 'A';     // one character

        // OBJECTS: bigger things stored on the heap; the variable holds a "reference" (an address) to them.
        String message = "Hello";  // String is an object (text); Strings cannot be changed (immutable).
        int[] nums = {1, 2, 3};    // Array object: fixed-size list of ints.

        System.out.println(count + ", " + price + ", " + active + ", " + letter);
        System.out.println("message length = " + message.length()); // Ask the object for info.
        System.out.println("first number = " + nums[0]);            // Arrays use [index] starting at 0.
    }
}
```

---

## 7) Variables: Local, Instance, Static
```java
public class Vars {
    // STATIC field: one shared copy for the whole class (all objects see the same number).
    private static int createdCount = 0;

    // INSTANCE field: each object has its own value.
    private final int id;

    public Vars() {
        createdCount++;     // increase the shared counter
        this.id = createdCount; // give this object a unique id
    }

    public void show() {
        // LOCAL variable: exists only while this method runs.
        String label = "Object";
        System.out.println(label + " id=" + id + ", totalMade=" + createdCount);
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

## 8) Initialization Order (Who runs first?)
```java
public class InitOrder {
    // STEP 1: static stuff runs once when the class is loaded.
    static int s = initStatic();
    static int initStatic() {
        System.out.println("1) static init");
        return 100;
    }

    // STEP 2: instance fields initialize each time you create an object.
    int a = initA();
    int initA() {
        System.out.println("2) instance field init");
        return 10;
    }

    // STEP 3: instance initializer blocks run next.
    { System.out.println("3) instance initializer block"); }

    // STEP 4: constructor runs last for each new object.
    public InitOrder() {
        System.out.println("4) constructor");
    }

    public static void main(String[] args) {
        System.out.println("Main start");
        new InitOrder(); // see the sequence
        new InitOrder(); // static won't run again (already done)
    }
}
```

---

## 9) Garbage Collection (GC)
```java
public class GCDemo {
    static class Big {
        // Big array to simulate memory usage (5 MB).
        private byte[] data = new byte[5_000_000];
    }

    public static void main(String[] args) {
        Big b = new Big();  // we create a big object
        System.out.println("Allocated Big");
        b = null;           // we drop our reference -> now it's trash (eligible for GC)
        System.gc();        // ask Java to clean (not guaranteed right now)
        System.out.println("Requested GC");
    }
}
```

---

# Chapter 4 – Operators and Statements (Step-by-step)

## 1) Operators Overview (What they do)
```java
public class Operators {
    public static void main(String[] args) {
        int x = 5;

        // ++x: add 1, then use the value (so it prints 6)
        System.out.println(++x);

        // x--: use the value, then subtract 1 (prints 6, x becomes 5)
        System.out.println(x--);

        // ! flips true/false
        boolean flag = !false;
        System.out.println(flag); // true

        // * has higher priority than +
        int a = 2 + 3 * 4; // 2 + 12 = 14
        System.out.println(a);

        // (...) changes the order so + happens first
        int b = (2 + 3) * 4; // 5 * 4 = 20
        System.out.println(b);

        // condition ? valueIfTrue : valueIfFalse
        int max = (a > b) ? a : b;
        System.out.println("max=" + max);
    }
}
```

---

## 2) Arithmetic, Assignment, Casting (Converting types)
```java
public class ArithmeticCasting {
    public static void main(String[] args) {
        int x = 10;
        x += 5; // same as x = x + 5 -> 15
        x *= 2; // same as x = x * 2 -> 30

        double d = 3.9;
        // Casting = force a value into another type (may lose info)
        int i = (int) d; // 3.9 becomes 3 (cuts off decimals)
        System.out.println("i=" + i);

        // Widening (safe): small type becomes bigger automatically.
        double sum = i + 2.5; // int becomes double for the math
        System.out.println("sum=" + sum);
    }
}
```

---

## 3) Relational, Equality, Logical (Comparing values)
```java
public class Comparisons {
    public static void main(String[] args) {
        int a = 5, b = 8;

        System.out.println(a < b);  // true, because 5 is less than 8
        System.out.println(a == 5); // true, because a is exactly 5
        System.out.println(a != b); // true, because they are different

        // '&&' short-circuits: if left is false, right is not checked (saves time).
        // Here left is true, so it calls expensiveCheck().
        boolean result = (a < b) && expensiveCheck();
        System.out.println("result=" + result);
    }

    static boolean expensiveCheck() {
        System.out.println("expensiveCheck called"); // shows that right side ran
        return true;
    }
}
```

---

## 4) Control Flow (if, switch, while, do-while, for, for-each)
```java
public class Flow {
    public static void main(String[] args) {
        int dayNum = 5;

        // if-else = choose between two paths
        if (dayNum < 6) {
            System.out.println("Weekday");
        } else {
            System.out.println("Weekend");
        }

        // switch = pick one case out of many
        String day = "Fri";
        switch (day) {
            case "Mon":
                System.out.println("Beginning");
                break; // stop here, don't fall into next case
            case "Fri":
                System.out.println("Almost weekend");
                break;
            default:
                System.out.println("Midweek");
        }

        // while = repeat WHILE condition is true (checks first)
        int i = 0;
        while (i < 3) {
            System.out.println("while i=" + i);
            i++;
        }

        // do-while = do once, THEN check condition (so it runs at least once)
        int j = 0;
        do {
            System.out.println("do-while j=" + j);
            j++;
        } while (j < 1);

        // for = classic counter loop (start; keep-going-while-true; step)
        for (int k = 0; k < 3; k++) {
            System.out.println("for k=" + k);
        }

        // for-each = loop through items in a list or array
        String[] names = {"Ana", "Luis"};
        for (String n : names) {
            System.out.println("Hello " + n);
        }
    }
}
```

---

## 5) break / continue / labels (Controlling loops)
```java
public class BreakContinue {
    public static void main(String[] args) {
        // 'continue' skips the rest of this loop turn and jumps to the next
        for (int i = 1; i <= 3; i++) {
            if (i == 2) continue; // skip printing 2
            System.out.println("i=" + i); // prints 1 and 3
        }

        // 'break' stops the loop completely
        for (int j = 1; j <= 3; j++) {
            if (j == 2) break; // stop when j hits 2
            System.out.println("j=" + j); // prints 1
        }

        // Labeled break: jump out of an outer loop from inside an inner loop
        outer:
        for (int r = 1; r <= 2; r++) {
            for (int c = 1; c <= 3; c++) {
                if (c == 2) break outer; // exit both loops immediately
                System.out.println("r=" + r + ", c=" + c);
            }
        }
    }
}
```

---

# Chapter 5 – Java API Essentials (Must-know tools)

## 1) String (Immutable text)
```java
public class StringDemo {
    public static void main(String[] args) {
        String s = "  hello  ";                // original text (has spaces)
        String t = s.trim().toUpperCase()      // 'trim' removes edge spaces; 'toUpperCase' makes it uppercase
                     .concat("!");             // 'concat' adds text at the end
        // IMPORTANT: Strings don't change; each step makes a NEW String.

        System.out.println("s='" + s + "'");   // original unchanged
        System.out.println("t='" + t + "'");   // new value
        System.out.println("Length=" + t.length());
        System.out.println("Starts with HE? " + t.startsWith("HE"));
        System.out.println("Substring(0,2)=" + t.substring(0, 2)); // first two letters
    }
}
```

---

## 2) StringBuilder (Mutable text for speed)
```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        // StringBuilder lets you change the text without creating new objects each time.
        StringBuilder sb = new StringBuilder(64); // optional: start capacity to avoid resizing
        for (int i = 1; i <= 5; i++) {
            if (i > 1) sb.append('-'); // add '-' between numbers
            sb.append(i);              // add number
        }
        System.out.println(sb.toString()); // turn builder into a normal String: "1-2-3-4-5"
    }
}
```

---

## 3) Arrays (Fixed-size lists)
```java
import java.util.Arrays;

public class ArraysDemo {
    public static void main(String[] args) {
        int[] a = {3, 1, 2};         // array of ints, length = 3
        Arrays.sort(a);              // sorts the array in place (changes it)
        System.out.println(Arrays.toString(a)); // prints [1, 2, 3]

        // binarySearch: works only on a sorted array; returns the index of the value (or negative if not found)
        int idx = Arrays.binarySearch(a, 2);
        System.out.println("Index of 2 = " + idx);

        // 2D array: array of arrays
        int[][] grid = {{1,2}, {3,4}};
        System.out.println(grid[1][0]); // row 1, column 0 -> 3
    }
}
```

---

## 4) ArrayList (Growable list)
```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        // ArrayList grows automatically when you add items.
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        System.out.println(list.get(0));  // get first item: "A"
        System.out.println(list.contains("B")); // check if "B" is inside
        list.remove("A");                 // remove by value
        System.out.println("Size=" + list.size());

        // For numbers, use wrapper types (Integer, Double, etc.) because ArrayList stores objects, not primitives.
        ArrayList<Integer> nums = new ArrayList<>();
        nums.add(10); // "autoboxing": int 10 becomes Integer automatically
        System.out.println(nums);
    }
}
```

---

## 5) Dates and Times (java.time)
```java
import java.time.*;
import java.time.format.DateTimeFormatter;

public class TimeDemo {
    public static void main(String[] args) {
        // LocalDate = date only (year-month-day)
        LocalDate d = LocalDate.of(2025, 9, 8);
        // LocalTime = time only (hour-minute-second)
        LocalTime t = LocalTime.now();
        // LocalDateTime = date + time (no timezone)
        LocalDateTime dt = LocalDateTime.now();
        // ZonedDateTime = date + time + timezone
        ZonedDateTime zdt = ZonedDateTime.now(ZoneId.systemDefault());

        // Add/subtract time
        LocalDate nextWeek = d.plusWeeks(1);
        LocalTime minusHour = t.minusHours(1);

        // Formatting (date -> text) and parsing (text -> date)
        DateTimeFormatter f = DateTimeFormatter.ofPattern("dd/MM/yyyy");
        String ds = d.format(f);              // "08/09/2025"
        LocalDate parsed = LocalDate.parse(ds, f); // back to a LocalDate

        System.out.println("d=" + d + ", nextWeek=" + nextWeek);
        System.out.println("t=" + t + ", minusHour=" + minusHour);
        System.out.println("zdt=" + zdt);
        System.out.println("formatted=" + ds + ", parsed=" + parsed);
    }
}
```

---

# Chapter 6 – Methods and Encapsulation (Clean, safe code)

## 1) Method Structure (What each part means)
```java
public class Methods {
    // public: anyone can call it
    // static: belongs to the class (no object needed)
    // int: it RETURNS an int
    // add: method name
    // (int a, int b): you must pass two ints
    public static int add(int a, int b) {
        return a + b; // send the result back to the caller
    }

    // This method might be interrupted while sleeping, so we must declare 'throws'.
    public static void nap(long ms) throws InterruptedException {
        Thread.sleep(ms); // may throw InterruptedException
    }

    public static void main(String[] args) throws InterruptedException {
        System.out.println(add(2, 3)); // prints 5
        nap(100);                      // pauses ~100ms
    }
}
```

---

## 2) Varargs (Accept many values easily)
```java
public class VarargsDemo {
    // 'String... parts' means you can pass 0, 1, or many Strings.
    static String joinWithComma(String... parts) {
        // Inside the method, 'parts' acts like an array.
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < parts.length; i++) {
            if (i > 0) sb.append(", ");
            sb.append(parts[i]);
        }
        return sb.toString();
    }

    public static void main(String[] args) {
        System.out.println(joinWithComma("A", "B", "C")); // "A, B, C"
        System.out.println(joinWithComma());              // ""
    }
}
```

---

## 3) Access Modifiers (Who can see what?)
```java
public class Access {
    private   int secret = 42; // only this class
              int pkgVal = 1;  // same package (no keyword = package-private)
    protected int semi = 2;    // same package + subclasses
    public    int open = 3;    // anywhere

    // Use a public method to safely access private data (encapsulation).
    public int getSecret() { return secret; }
}
```

---

## 4) Static vs Instance (Shared vs personal)
```java
public class Counter {
    private static int total = 0; // one shared number for ALL Counter objects
    private final int id;         // each object gets its own id

    public Counter() {
        id = ++total; // grow the shared number and store it as this object's id
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

## 5) Pass-by-Value (Important truth about Java)
```java
public class PassByValue {
    static class Box { int v; }

    // We can change the object that 'b' points to (its inside value).
    static void mutate(Box b) { b.v = 99; }

    // We cannot make the caller's variable point to a new object by reassigning the parameter.
    static void reassign(Box b) { b = new Box(); }

    public static void main(String[] args) {
        Box b = new Box(); b.v = 10;
        mutate(b);   // changes b.v to 99 (same object)
        reassign(b); // only changes the local copy of the reference, caller still has original
        System.out.println(b.v); // 99
    }
}
```

---

## 6) Overloading (Same name, different inputs)
```java
public class Overload {
    // Different parameter types/counts -> allowed.
    public void log(String msg)       { System.out.println("S: " + msg); }
    public void log(int code)         { System.out.println("I: " + code); }
    public void log(String m, int c)  { System.out.println("S+I: " + m + " " + c); }

    public static void main(String[] args) {
        Overload o = new Overload();
        o.log("hello");
        o.log(200);
        o.log("ok", 200);
    }
}
```

---

## 7) Constructors and `this()` (Avoid repeating setup)
```java
public class Dog {
    private final String name;
    private final int age;

    // Calls another constructor to reuse code. Must be the FIRST line.
    public Dog() {
        this("NoName", 0);
    }

    public Dog(String name, int age) {
        this.name = name;  // store given data
        this.age = age;
    }

    public void info() {
        System.out.println(name + " (" + age + ")");
    }

    public static void main(String[] args) {
        new Dog().info();          // uses default values
        new Dog("Rex", 5).info();  // uses custom values
    }
}
```

---

## 8) Encapsulation & Immutability (Protect your data)
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

// 'final' class = no one can extend it (optional).
public final class Team {
    private final String name;          // cannot change after creation
    private final List<String> members; // store a safe, unmodifiable copy

    public Team(String name, List<String> members) {
        this.name = name;
        // Defensive copy + unmodifiable wrapper = callers cannot modify your internal list.
        this.members = Collections.unmodifiableList(new ArrayList<>(members));
    }

    public String getName() { return name; }
    public List<String> getMembers() { return members; } // safe to expose (read-only)
}
```

---

# Chapter 7 – Class Design (How classes relate)

## 1) Inheritance (Child gets features from Parent)
```java
class Animal {
    private int age;
    public int getAge() { return age; }      // public -> visible to everyone
    public void setAge(int a) { this.age = a; }
}

class Lion extends Animal {
    public void roar() {
        // We can use getAge() inherited from Animal
        System.out.println("Roar! I am " + getAge() + " years old");
    }
}
```

---

## 2) One public class per file (File name must match)
```java
// File: Zoo.java
public class Zoo { } // public class name == file name
// This package-private class can share the file (less common for beginners)
class Pen { }
```

---

## 3) Constructors & `super()` (Call parent's setup)
```java
class Base {
    Base() { System.out.println("Base constructor"); }
}

class Derived extends Base {
    Derived() {
        super(); // call parent's constructor (Java adds this automatically if you don't)
        System.out.println("Derived constructor");
    }

    public static void main(String[] args) {
        new Derived(); // see the order: Base then Derived
    }
}
```

---

## 4) Overriding (Replace parent behavior)
```java
class Bird {
    public void fly() { System.out.println("Bird flying"); }
}
class Eagle extends Bird {
    @Override
    public void fly() { System.out.println("Eagle soaring"); } // replaces parent version
}
```

---

## 5) Abstract Classes (Templates you must complete)
```java
abstract class Shape {
    // No body -> child classes must write the code for this method.
    abstract double area();
}
class Circle extends Shape {
    private final double r;
    Circle(double r){ this.r = r; }
    double area(){ return Math.PI * r * r; } // now we provide the behavior
}
```

---

## 6) Interfaces (Promises)
```java
// An interface says: "any class that implements me WILL have these methods".
interface CanFly { void fly(); }

class Sparrow implements CanFly {
    @Override
    public void fly() { System.out.println("Sparrow flaps!"); }
}
```

---

## 7) Polymorphism & Casting (Use parent types to hold child objects)
```java
class Animal2 { void sound(){ System.out.println("..."); } }
class Dog2 extends Animal2 { @Override void sound(){ System.out.println("Woof"); } }

public class Poly {
    public static void main(String[] args) {
        Animal2 a = new Dog2(); // OK: a Dog2 IS-AN Animal2 (upcast)
        a.sound();              // calls Dog2's version (runtime decides)

        // To use Dog2-only features, you must cast back (downcast).
        if (a instanceof Dog2) {
            Dog2 d = (Dog2) a;
            d.sound();
        }
    }
}
```

---

## 8) Lambdas (Short functions)
```java
import java.util.Arrays;
import java.util.List;

// Lambdas are tiny functions you can pass around to methods.
public class LambdasIntro {
    public static void main(String[] args) {
        List<String> list = Arrays.asList("a", "b", "c");
        // forEach needs a "Consumer" (a thing with a method that takes one value).
        // s -> System.out.println(s) creates that tiny method on the fly.
        list.forEach(s -> System.out.println(s));
    }
}
```

---

# Chapter 8 – Exceptions (Handling problems)

## 1) Throwing & Declaring (Say there is a problem)
```java
public class Throwing {
    // 'throws Exception' warns callers: "I might fail, you must handle me."
    static void risky() throws Exception {
        // 'throw' actually creates and sends the error up to the caller.
        throw new Exception("Something went wrong");
    }

    public static void main(String[] args) {
        try {
            risky(); // this may throw
        } catch (Exception e) { // we catch and handle the problem
            System.out.println("Handled: " + e.getMessage());
        }
    }
}
```

---

## 2) Types of problems (Checked / Unchecked / Errors)
```java
public class Kinds {
    static void checkedExample() throws java.io.IOException {
        // Checked exceptions: the compiler forces you to handle or declare them.
        throw new java.io.IOException("I/O failed");
    }

    static void uncheckedExample() {
        // Unchecked exceptions (RuntimeException): compiler does NOT force handling.
        throw new IllegalArgumentException("Bad argument");
    }

    // 'Error' (like OutOfMemoryError) = serious system problem; usually don't catch.
}
```

---

## 3) try-catch-finally (Handle + Cleanup)
```java
import java.io.*;

public class TryCatchFinally {
    public static void main(String[] args) {
        BufferedReader br = null; // a "resource" we must close
        try {
            br = new BufferedReader(new FileReader("data.txt")); // may fail if file missing
            System.out.println(br.readLine()); // may fail while reading
        } catch (FileNotFoundException e) { // specific problem: file does not exist
            System.out.println("File not found");
        } catch (IOException e) { // general I/O problem
            System.out.println("I/O error");
        } finally {
            // This block runs ALWAYS (success or failure).
            // Good place to release resources (close files, network, etc.).
            try {
                if (br != null) br.close(); // closing may also fail
            } catch (IOException e) {
                System.out.println("Close failed");
            }
        }
    }
}
```

> Tip: Use **try-with-resources** to auto-close things.

```java
import java.io.*;

public class TryWithResources {
    public static void main(String[] args) {
        // 'br' will be closed automatically when the try block ends.
        try (BufferedReader br = new BufferedReader(new FileReader("data.txt"))) {
            System.out.println(br.readLine());
        } catch (IOException e) { // covers both open/read/close problems
            System.out.println("I/O problem: " + e.getMessage());
        }
    }
}
```

---

## 4) Printing Exceptions (See what happened)
```java
public class Printing {
    public static void main(String[] args) {
        try {
            Integer.parseInt("not-a-number"); // will fail
        } catch (Exception e) {
            System.out.println(e);              // shows type + message
            System.out.println(e.getMessage()); // just the message
            e.printStackTrace();                // full details (useful for debugging)
        }
    }
}
```

---

## Key Takeaways (All Chapters)
- **Class** = blueprint, **object** = thing you build.
- **main** is the starting door of your program.
- **Primitives** are small value boxes; **objects** are bigger things with behavior.
- **String** is immutable; **StringBuilder** is mutable and fast for building text.
- **Array** is fixed-size; **ArrayList** grows.
- **Static** = shared; **instance** = per object.
- Java passes **values** (object references are copied, not the object itself).
- **Inheritance** shares features; **interfaces** promise behavior.
- **Exceptions** report problems; handle them with `try/catch` and clean up with `finally` or **try-with-resources**.
