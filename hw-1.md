# HW - 1

## 1. Why Use OOP? What Are the Main OOP Languages?

### Why Use OOP?

Object-oriented programming helps organize code by grouping data and behavior into reusable classes. It makes code more maintainable and closer to how we model real-world systems.

- **Encapsulation** hides internal details of objects.
- **Inheritance** allows new classes to reuse existing code.
- **Polymorphism** makes methods behave differently depending on the object.
- **Abstraction** lets us focus on what an object does, not how.
- Improves **maintainability** and **scalability** in bigger applications.

### Major OOP Languages

- Java
- Python
- C++
- C#
- JavaScript
- Ruby
- Swift
- Kotlin
- PHP

---

## 2. Interface vs Abstract Class

### Abstract Class:

Abstract classes shine when you need partial implementation. In my banking application, we used an abstract `Account` class that handled common functionality while forcing specific account types to implement their own interest calculations.

- Can have both regular and abstract methods.
- May contain any type of variables.
- A class can only extend one abstract class.
- Constructors, static, and final methods are allowed.

### Interface:

Interfaces transformed how to design systems, they are perfect for defining capabilities without dictating implementation.

- Before Java 8: only abstract methods.
- Since Java 8: can have default and static methods.
- Since Java 9: supports private methods.
- Variables are always `public static final`.
- Allows multiple inheritance (a class can implement several interfaces).
- No constructors or instance variables.

### When to Use:

- **Abstract Class**: Can be used when you want to share basic logic and also when you want to share the content of basic functions.
- **Interface**: Can be used when you want to create a contract and have different classes follow the same structure

---

## 3. Why wee need equals and hashcode ? When to override ?

### Purpose:

- `equals()` checks logical equality between objects.
- `hashCode()` helps store objects efficiently in hash-based collections like `HashSet` or `HashMap`.

### Override When:

- You create custom classes that are used in collections.
- You want to compare not only references but also object content.
- Equal objects should always return the same hash code.

---

## 4. Diamond problem in Java ? How to fix it?

### Diamond Problem:

It occurs when a class inherits from two classes that both inherit from the same parent, causing ambiguity.

```
      A
     / \
    B   C
     \ /
      D
```

### Java’s Solution:

- Java does not support multiple inheritance with classes.
- Multiple interfaces can be implemented.
- If two interfaces have conflicting default methods, the class must override them to resolve the conflict.

---

## 5. Why we need Garbagge Collector ? How does it run ?

### Purpose:

- Frees up memory by removing objects no longer used.
- Prevents memory leaks.
- Eases memory management in large or complex apps.

### How It Works:

1. **Mark** unused objects.
2. **Sweep** or delete them.
3. (Optional) **Compress memory** to optimize space.

Basically, it uses memory efficiently by moving objects around by categorizing them and optimizes the memory used.

### Common GC Algorithms:

Through painful production tuning, I've learned the strengths of each:
- **Serial GC**: Simple but surprisingly effective for small applications
- **Parallel GC**: Our go-to for batch processing applications
- **CMS**: Saved us from pause-time issues in our customer-facing applications
- **G1 GC**: The best balance I've found for most modern applications
- **ZGC**: A game-changer for our low-latency trading platform

---

## 6. Usage of the `static` Keyword in Java

### Where It’s Used:

They are used for different purposes in different programming structures.

- **Variables**: Create class-level constants or shared state (though be careful with the latter!)
- **Methods**: Define utility functions that don't need object context
- **Nested Classes**: Create helper classes that don't need access to outer instance state

### Examples:

```java
public static final int MAX_USERS = 100; // Example on a variable
Math.random(); // Example on a method
```

- Also used in **Singleton** (mostly) and **Factory** (sometimes) patterns.

---

## 7. Immutability means ? Where, How and Why to use it ?

### What:

Immutable objects cannot change after they’re created.

### How to Make a Class Immutable:

- Use `final` for the class.
- Make fields `private final`.
- Avoid setters.
- Return copies of mutable objects.
- Use deep copies in constructors if needed.

### Why:

- Thread safety
- Predictable behavior
- Better for use in collections like keys

### Where:

- Value objects (e.g., `Money`, `Date`)
- Configurations
- Caching
- Unmodifiable collections

Immutability plays a huge role to ensure both security and consistency in software. 
For example, consider an application that authenticates users; if passwords stored as strings are mutable, they can be inadvertently changed during processing, leading to security vulnerabilities. 
By keeping such sensitive data immutable, you guarantee that once a password is set, it remains unchanged throughout the application's lifecycle.
---

## 8. Composition vs Aggregation

### Composition:

- Strong ownership.
- Child cannot exist without the parent.
- Example: A `House` has `Rooms`.

### Aggregation:

- Weak ownership.
- Child can live independently.
- Example: A `Department` has `Professors`.

### Key Difference:

- **Composition**: Parent controls the child’s lifecycle.
- **Aggregation**: Child exists on its own.

---

## 9. Cohesion vs Coupling

### Cohesion:

This relates to how tightly the responsibilities in a module are linked together.

- **High cohesion**: When your code is smooth, focused and each piece does one thing really well.
- **Low cohesion**: When your code is a mess trying to perform too many unrelated tasks.


### Coupling:

This shows how connected one class or module is to another.

- **Loose coupling**: Each piece of your code works independently; changes to one don't break the others.
- **Tight coupling**: When one class changes, the whole system can be out of balance.

### Ideal:

High cohesion, low coupling.

---

## 10. Heap vs Stack

### Stack
- Holds local variables and method calls.
- Works on a Last-In-First-Out (LIFO) basis.
- Each thread gets its own private stack—eliminating concurrency concerns
- Stack allocation is blazingly fast but size-limited—I once crashed an app with excessive recursion!

### Heap
- All objects created with `new` live here
- It's shared across all threads—requiring careful concurrency handling
- Memory allocation is more complex and slightly slower
- The heap can grow dynamically—though I've hit OOM errors in memory-intensive applications

---

## 11. Exception Types and Hierarchy

### What exception means?

An exception is a fancy way of saying “something went wrong” during program execution. It throws an exception when your code encounters a problem that it can't handle immediately. 
You can then catch that exception to gracefully deal with the error instead of letting the whole program crash.

### Exception Hierarchy:

```
Throwable
├── Error (serious problems, don't catch these!)
└── Exception
    ├── Checked Exceptions
    └── RuntimeException (Unchecked)
```

### Types:

- **Checked**: For recoverable conditions the caller should handle (e.g., FileNotFoundException when the user can select another file)
- **Unchecked**: For programming errors that shouldn't happen with proper code (e.g., NullPointerException)
- **Error**: For serious system-level issues beyond application recovery (e.g., OutOfMemoryError)

My rule of thumb: If the caller can reasonably recover, use a checked exception. Otherwise, use unchecked.

---

## 12. What Is Clean Code?

Clean code is:

- **Readable**: It should be understood what it does without deciphering it
- **Structured**: Following SOLID principles keeps responsibilities clear
- **DRY**: Avoids repeating code.
- **Testable**: Easy to write tests for especially for unit tests.
- **Consistent**: Using the same patterns and naming conventions throughout.
- **Simple**: Solving problems directly without unnecessary complexity: Not over-complicated.

---

## 13. What Is Method Hiding in Java?

If a subclass defines a `static` method with the same signature as its parent class, it hides the method — it doesn’t override it.

When a subclass defines a static method with the same signature as a static method in the parent, it hides the parent's method rather than overriding it.

### Example:

```java
class Parent {
    static void show() {
        System.out.println("Parent's static method");
    }
}

class Child extends Parent {
    static void show() {
        System.out.println("Child's static method");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent p = new Child();
        p.show();  // Calls Parent's method

        Child c = new Child();
        c.show();  // Calls Child's method
    }
}
```

---

## 14. Abstraction vs Polymorphism

### Abstraction:

### Abstraction:

Abstraction is about hiding unnecessary details to manage complexity. It's what lets me design interfaces before implementation details.

- Abstract classes and interfaces to define what matters conceptually. Done using abstract classes and interfaces.
- Example: Our payment processing system abstracts away the details of different payment providers behind a simple `process()` method

### Polymorphism:

Polymorphism lets treat different object types through a common interface. It's the practical manifestation of abstraction.

- Achieved through method overriding and overloading.
- Example: `Shape` can point to a `Circle`, `Rectangle`, etc.

### Relationship:

Abstraction provides the foundation for polymorphism to work effectively. Without good abstractions, polymorphism becomes messy and brittle.

---
Note: AI tools were used to convert to .md format and to correct grammatical errors in general.
---