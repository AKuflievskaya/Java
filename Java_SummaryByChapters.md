# Chapter 3 – Java Basics (Explained for Python Developers)

## 1. Classes and Objects
- In Java **everything must be inside a class** (unlike Python, where you can write functions at the top level).
- A class has:
  - **properties** (like Python instance variables: `self.name`)
  - **methods** (like functions inside a class)
- To use a class, you must create an **object** with `new`.

### Python
```python
class Person:
    def __init__(self, name):
        self.name = name

p = Person("Ana")
print(p.name)
```

### Java
```java
public class Person {
    String name;

    public Person(String n) {
        this.name = n;
    }

    public static void main(String[] args) {
        Person p = new Person("Ana");
        System.out.println(p.name);
    }
}
```

---

## 2. The `main` Method
- Acts like `if __name__ == "__main__":` in Python.
- It’s the entry point of every Java program.

### Java
```java
public static void main(String[] args) {
    System.out.println("Hello");
}
```

---

## 3. Comments
- `//` → single line  
- `/* ... */` → multi-line  
- `/** ... */` → Javadoc (like Python docstrings, but auto-generated into HTML docs)

---

## 4. Packages and Imports
- Similar to Python **modules/packages**.
- `package` = folder where your class lives.
- `import` = bring in other classes.

### Java
```java
import java.util.Random;

public class Example {
    public static void main(String[] args) {
        Random r = new Random();
        System.out.println(r.nextInt(10));
    }
}
```

### Python
```python
import random

print(random.randint(0, 9))
```

---

## 5. Constructors
- Like Python’s `__init__`, but in Java the method name = class name.

### Python
```python
class Animal:
    def __init__(self, kind):
        self.kind = kind
```

### Java
```java
public class Animal {
    String kind;

    public Animal(String k) {
        this.kind = k;
    }
}
```

---

## 6. Data Types
- **Primitives**: `int`, `double`, `boolean`, `char` (simple, fixed size, stored directly).
- **References**: Objects like `String`, `ArrayList`, etc.
- Unlike Python, **types must be declared**.

---

## 7. Variables
- **Local variables**: inside methods (like normal variables in Python).
- **Instance variables**: belong to the object (`self.x` in Python).
- **Class variables (`static`)**: shared across all instances.

---

## 8. Scope and Initialization Order
- `{}` define code blocks (like indentation in Python).
- You must declare variables **before using them**.
- Order matters:
  1. Properties initialized
  2. Instance initializer blocks
  3. Constructor runs

---

## 9. Memory and Garbage Collection
- Like Python, Java has **Garbage Collector** to clean up unused objects automatically.

---

## 🔑 Key Takeaway
Think of Java as Python but:
- Everything must be inside a **class**
- You must **declare types**
- Use `{}` instead of indentation
- Programs always start at a **`main` method**

# Chapter 4 – Operators and Statements (Explained for Python Developers)

## 1. Operators in Java
- Operators are special symbols that act on variables/values and return a result.
- Three types:
  - **Unary**: act on one operand (`++x`, `--x`, `!flag`).
  - **Binary**: act on two operands (`x + y`, `a > b`).
  - **Ternary**: act on three operands (`condition ? value1 : value2`).

---

## 2. Arithmetic Operators
- `+`, `-`, `*`, `/`, `%` (remainder).
- Precedence works like math: `* / %` before `+ -`.
- Use parentheses to control order.

### Python
```python
x = 2 * 5 + 3 * 4 - 8   # 14
```

### Java
```java
int x = 2 * 5 + 3 * 4 - 8;  // 14
```

---

## 3. Unary Operators
- `++x` / `x++` (increment by 1).
- `--x` / `x--` (decrement by 1).
- `!flag` (logical NOT).

### Example
```java
int counter = 0;
System.out.println(++counter); // 1 (pre-increment)
System.out.println(counter--); // 1 (post-decrement)
```

---

## 4. Assignment and Casting
- `=` assigns values.
- **Compound assignment**: `+=`, `-=`, `*=`, `/=`, etc.
- **Casting**: convert between primitive types.

```java
int a = (int) 3.5;   // cast double → int
```

---

## 5. Relational & Equality Operators
- `<`, `<=`, `>`, `>=` → compare numbers.
- `==`, `!=` → equality check.
- `instanceof` → check if an object is of a type.

### Python vs Java
```python
print(5 == 5.0)   # True
```

```java
System.out.println(5 == 5.0);  // true (auto-promotion to double)
```

---

## 6. Logical Operators
- `&&` (AND, short-circuit).
- `||` (OR, short-circuit).
- `!` (NOT).
- Bitwise versions: `&`, `|`, `^`.

---

## 7. Conditional (Ternary) Operator
- Syntax: `condition ? value1 : value2`.
- Equivalent to Python’s inline `a if condition else b`.

```java
int y = 10;
int x = (y > 5) ? 2 * y : 3 * y;
```

---

## 8. Control Flow Statements

### if / if-else
```java
if (x > 0) {
    System.out.println("Positive");
} else {
    System.out.println("Non-positive");
}
```

### switch
- Works with `int`, `char`, `String` (from Java 7).
```java
switch(day) {
    case "Mon": System.out.println("Start"); break;
    case "Fri": System.out.println("End"); break;
    default:    System.out.println("Midweek");
}
```

### Loops
- **while**: checks condition before loop.
```java
while(x < 5) {
    x++;
}
```

- **do-while**: executes at least once.
```java
do {
    x++;
} while(x < 5);
```

- **for**: classic counter loop.
```java
for(int i=0; i<5; i++) {
    System.out.println(i);
}
```

- **for-each**: iterate collections/arrays.
```java
for(String name : names) {
    System.out.println(name);
}
```

---

## 9. Advanced Flow
- **Nested loops**: loops inside loops.
- **Labels**: optional tags to control outer loops.
- **break**: exit a loop.
- **continue**: skip current iteration.

```java
for(int i=1; i<=3; i++) {
    for(int j=1; j<=3; j++) {
        if(j==2) continue; // skip when j==2
        System.out.println(i + "," + j);
    }
}
```

---

## 🔑 Key Takeaways
- Java operators behave like math/logic but require strict typing.
- Control flow: `if`, `switch`, `while`, `for`, `for-each`.
- Use `break` and `continue` to manage loops.
- The ternary operator is a shortcut for `if-else`.

# Chapter 5 – Java API (Explained for Python Developers)

## 1. Strings
- A `String` is an **immutable sequence of characters**.
- Ways to create:
```java
String s1 = "Bottle";               // literal
String s2 = new String("Bottle");   // with new
```
- Concatenation:
```java
System.out.println("a" + "b");   // ab
System.out.println(1 + 2 + "c"); // 3c
```
- **String Pool**: literals are reused for efficiency.
- Common methods:
  - `length()`, `charAt(i)`, `substring(a,b)`, `toLowerCase()`, `toUpperCase()`, `trim()`, `equals()`, `equalsIgnoreCase()`, `contains()`, `startsWith()`, `endsWith()`, `replace()`, `split()`.
- Methods can be chained:
```java
String msg = " hello ".trim().toUpperCase().concat("!");
```

---

## 2. StringBuilder
- **Mutable strings** (unlike `String`).
- More efficient for repeated modifications.
- Example:
```java
StringBuilder sb = new StringBuilder("hi");
sb.append(" there").insert(0, ">>> ");
System.out.println(sb.toString());  // >>> hi there
```
- Common methods: `append()`, `insert()`, `delete()`, `reverse()`, `capacity()`, `length()`.

---

## 3. Equality
- `==` checks **references** (same object).
- `.equals()` checks **content**.
```java
String a = "cat";
String b = new String("cat");
System.out.println(a == b);      // false
System.out.println(a.equals(b)); // true
```

---

## 4. Arrays
- Fixed-size collections.
- Declaration:
```java
int[] nums = new int[3];          // [0,0,0]
String[] pets = {"dog","cat"};
```
- Multi-dimensional:
```java
int[][] matrix = { {1,2}, {3,4} };
```
- Sorting & searching with `Arrays.sort()` and `Arrays.binarySearch()`.

---

## 5. ArrayList
- Resizable alternative to arrays.
- Declaration:
```java
import java.util.*;

ArrayList<String> list = new ArrayList<>();
list.add("A"); list.add("B");
System.out.println(list.get(0)); // A
```
- Useful methods: `add()`, `remove()`, `size()`, `contains()`, `isEmpty()`, `clear()`.
- Wrapper classes: primitives have object equivalents (`int` → `Integer`, `double` → `Double`).
- Autoboxing: automatic conversion between primitives and wrappers.
```java
ArrayList<Integer> nums = new ArrayList<>();
nums.add(5);  // auto-boxes int → Integer
```

---

## 6. Dates and Times
- Use **java.time API** (Java 8+).
- Create:
```java
LocalDate d = LocalDate.of(2023, 9, 8);
LocalTime t = LocalTime.now();
LocalDateTime dt = LocalDateTime.now();
```
- Manipulate:
```java
d.plusDays(10);
t.minusHours(2);
```
- Periods:
```java
Period p = Period.between(LocalDate.now(), d);
```
- Formatting:
```java
DateTimeFormatter f = DateTimeFormatter.ofPattern("dd/MM/yyyy");
System.out.println(d.format(f));
```
- Parsing:
```java
LocalDate parsed = LocalDate.parse("01/02/2020", f);
```

---

## 🔑 Key Takeaways
- `String` = immutable, use carefully.
- `StringBuilder` = mutable, faster for concatenations.
- `==` vs `.equals()` is critical for objects.
- Arrays are fixed size; use `ArrayList` for flexibility.
- Wrapper classes + autoboxing integrate primitives with collections.
- Modern Java date/time API is powerful and type-safe.

# Chapter 6 – Methods and Encapsulation (Explained for Python Developers)

## 1. Designing Methods
A method in Java has several parts:
```java
public final void nap(int minutes) throws InterruptedException {
    // take a nap
}
```
- **Access modifier**: `public`, `private`, `protected`, or default (package-private).
- **Optional specifiers**: `final`, `static`, `abstract`, `synchronized`.
- **Return type**: `void` or any type.
- **Method name**: follows Java naming rules.
- **Parameters**: typed, can be empty.
- **Exceptions**: optional `throws`.
- **Body**: code inside `{}`.

---

## 2. Varargs
- Variable arguments let a method accept many parameters of the same type.
```java
public void printAll(String... words) {
    for (String w : words) {
        System.out.println(w);
    }
}
```
- Inside the method, `words` behaves like an array.

---

## 3. Access Modifiers
- **private** → only accessible in the same class.
- **default (package-private)** → accessible in the same package.
- **protected** → accessible in the same package and subclasses.
- **public** → accessible everywhere.

---

## 4. Static vs Instance
- **Instance members**: belong to objects.
- **Static members**: belong to the class itself.
```java
public class Counter {
    static int total = 0;   // shared by all
    int id;                 // unique per object

    public Counter() {
        total++;
        id = total;
    }
}
```

---

## 5. Passing Data
- Java is **pass-by-value**.  
- For primitives → value is copied.  
- For objects → reference is copied (so methods can modify the object, but not reassign it).

---

## 6. Method Overloading
- Same method name, different parameter list.
```java
public void fly(int km) {}
public void fly(String where) {}
public void fly(int km, String where) {}
```
- Rules:
  - Must differ in **number** or **types** of parameters.
  - Return type alone is not enough.

---

## 7. Constructors
- Special methods to create objects.
- No return type, same name as class.
- If no constructor is defined → Java adds a default one.
- Constructors can call each other with `this()`.
- Must be the first statement.

```java
public class Dog {
    String name;
    int age;

    public Dog() {
        this("NoName", 0);
    }
    public Dog(String n, int a) {
        name = n; age = a;
    }
}
```

---

## 8. Encapsulation
- Keep attributes **private** and expose them through getters/setters.
```java
public class Swan {
    private int numberEggs;

    public int getNumberEggs() {
        return numberEggs;
    }
    public void setNumberEggs(int eggs) {
        if (eggs >= 0)
            this.numberEggs = eggs;
    }
}
```
- **Immutable classes**: no setters, all fields `final`, and safe returns.

---

## 🔑 Key Takeaways
- A method = access modifier + optional specifiers + return type + name + parameters + exceptions + body.
- `varargs` allows flexible argument lists.
- Access modifiers control visibility (`private`, default, `protected`, `public`).
- Static = belongs to the class, instance = belongs to each object.
- Overloading = same name, different parameters.
- Constructors initialize objects; can chain with `this()`.
- Encapsulation hides fields and uses getters/setters.
- Immutable classes prevent modification of state.

# Chapter 7 – Class Design (Explained for Python Developers)

## 1. Inheritance Basics
- Java supports **single inheritance** (a class can only extend one direct parent).
- A subclass (child) automatically gets access to the parent’s public and protected members.
- Syntax:
```java
public class Animal {
    private int age;
    public int getAge() { return age; }
    public void setAge(int a) { age = a; }
}

public class Lion extends Animal {
    public void roar() {
        System.out.println("Roar! Age: " + getAge());
    }
}
```
- All classes inherit (directly or indirectly) from `java.lang.Object`.

---

## 2. Access Modifiers for Classes
- `public`: class can be used anywhere.
- *default* (no modifier): class is only accessible in the same package.
- Only **one public class per file**, and the filename must match it.

---

## 3. Constructors and Inheritance
- First line of a constructor is either:
  - `this()` (another constructor in the same class), or
  - `super()` (a constructor from the parent).
- If not written, Java inserts `super()` automatically.
```java
public class Zebra extends Animal {
    public Zebra() {
        super();   // calls Animal’s constructor
    }
}
```

---

## 4. Calling Parent Members
- A subclass can call parent methods/variables if they’re `public` or `protected`.
- Private variables are not accessible directly, only via getters/setters.

---

## 5. Method Inheritance and Overriding
- Methods can be **inherited** or **overridden**.
- To override: method must have the same signature and compatible return type.
```java
class Bird {
    public void fly() { System.out.println("Flying"); }
}
class Eagle extends Bird {
    @Override
    public void fly() { System.out.println("Flying high"); }
}
```

---

## 6. Abstract Classes
- Declared with `abstract`.
- Cannot be instantiated.
- May contain abstract methods (without body).
```java
abstract class Animal {
    abstract void makeSound();
}
class Dog extends Animal {
    void makeSound() { System.out.println("Woof"); }
}
```

---

## 7. Interfaces
- Define a contract: a list of methods without implementation.
- A class `implements` an interface.
```java
interface CanFly {
    void fly();
}
class Bird implements CanFly {
    public void fly() { System.out.println("Flap"); }
}
```
- Interfaces can also have:
  - **default methods** (with body).
  - **static methods**.
- A class can implement **multiple interfaces** (unlike class inheritance).

---

## 8. Polymorphism
- Ability to use a parent reference to point to a child object.
```java
Animal a = new Dog();
a.makeSound();   // "Woof"
```
- Rules:
  - Reference type determines what methods are visible at compile time.
  - Actual object type determines which method runs at runtime.

---

## 9. Casting
- Upcasting (child → parent) is automatic.
- Downcasting (parent → child) requires explicit cast.
```java
Animal a = new Dog();
Dog d = (Dog) a; // must cast back
```

---

## 10. Lambdas (Intro)
- Shortcut to create small implementations of interfaces with one method (functional interfaces).
```java
List<String> list = Arrays.asList("a","b","c");
list.forEach(s -> System.out.println(s));
```

---

## 🔑 Key Takeaways
- Java uses **single inheritance** + multiple interfaces.
- All classes extend `Object`.
- Constructors chain with `this()` or `super()`.
- Methods can be inherited, overridden, or abstract.
- Interfaces define contracts; classes implement them.
- Polymorphism lets you treat subclasses as parent references.
- Lambdas simplify functional code.

# Chapter 8 – Exceptions (Explained for Python Developers)

## 1. What are Exceptions?
- An **exception** is Java’s way of saying: *“Something went wrong, you handle it.”*
- Two options:
  - Handle it inside the method (`try`/`catch`).
  - Declare it so the caller must handle it (`throws`).
- Analogy: normal execution is a “happy path”, exceptions are when the flow breaks.

---

## 2. Throwing Exceptions
- Any code can throw an exception:
```java
throw new Exception("Something bad happened");
throw new RuntimeException("Unexpected error");
```
- `throw` = actually throw the exception.  
- `throws` = declare that a method *might* throw it.
```java
void fall() throws Exception {
    throw new Exception("Ow!");
}
```

---

## 3. Types of Exceptions
- All exceptions derive from `Throwable`.
- **Checked exceptions** (`Exception` but not `RuntimeException`):
  - Must be handled or declared.
  - Example: `IOException`, `FileNotFoundException`.
- **Unchecked exceptions** (`RuntimeException` and subclasses):
  - Don’t need to be declared.
  - Example: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `ClassCastException`.
- **Errors** (`Error` and subclasses):
  - Serious issues (e.g., `OutOfMemoryError`, `StackOverflowError`).
  - Should not be caught.

---

## 4. Common Runtime Exceptions
- `ArithmeticException` → division by zero.
- `ArrayIndexOutOfBoundsException` → invalid array index.
- `ClassCastException` → invalid type cast.
- `IllegalArgumentException` → invalid method argument.
- `NullPointerException` → accessing members on a `null` reference.
- `NumberFormatException` → invalid string to number conversion.

---

## 5. The `try-catch-finally` Statement
- Handle exceptions locally.
```java
try {
    riskyOperation();
} catch (IOException e) {
    System.out.println("Problem: " + e.getMessage());
} finally {
    System.out.println("Always runs");
}
```
- Rules:
  - At most **one catch** runs.
  - Order matters → catch subclasses first.
  - If both `catch` and `finally` throw, the `finally` one is kept.
  - `finally` is often used to close resources.

---

## 6. Multiple Catch Blocks
- You can catch different exception types.
```java
try {
    seeAnimal();
} catch (ExhibitClosedForLunch e) {   // subclass
    System.out.println("try back later");
} catch (ExhibitClosed e) {           // superclass
    System.out.println("not today");
}
```
- More specific exceptions must be caught **before** general ones.

---

## 7. Printing Exceptions
- Three common ways:
```java
try {
    hop();
} catch (Exception e) {
    System.out.println(e);              // type + message
    System.out.println(e.getMessage()); // message
    e.printStackTrace();                // full stack trace
}
```

---

## 8. Best Practices
- Don’t ignore exceptions — it can hide important problems.
- Print/log the exception or rethrow it.
- Only use exceptions for *exceptional situations*, not normal flow control.

---

## 🔑 Key Takeaways
- Java forces you to deal with exceptions → checked vs unchecked.
- Use `try-catch-finally` to handle them, `throw` to raise, `throws` to declare.
- Catch specific exceptions before general ones.
- Stack traces are essential for debugging.
- Don’t swallow exceptions silently.
