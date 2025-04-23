# [4th_End_Sem](2k24_End_Sem.pdf)

- ## JAVA
- ## Discrete Mathematics
- ## DCC
- ## Entrepreneurship
- ## Unix OS


## JAVA

<img src="Java_End_Sem_2024.png">

### Q 1 **(a) What is an abstract class?**
> An **abstract class** in object-oriented programming is a class that **cannot be instantiated directly**—it serves as a **blueprint for other classes**.

Key points:
- It **may contain abstract methods** (methods without implementation) as well as fully implemented methods.
- Used when you want to **define a base class** with some common functionality and leave the implementation of certain methods to **subclasses**.
- In Java, you declare it with the keyword `abstract`:
  
  ```java
  abstract class Animal {
      abstract void makeSound();  // abstract method
      void sleep() {
          System.out.println("Sleeping...");
      }
  }
  ```

---

### Q 1 **(b) What is the difference between static and non-static variables?**

| Feature           | Static Variable                            | Non-static Variable                       |
|------------------|---------------------------------------------|-------------------------------------------|
| Belongs to       | The **class**, not an instance              | A **specific instance** (object)          |
| Memory allocation| Once, at the time of class loading          | Every time a new object is created        |
| Accessed by      | Class name or object                        | Only by object                            |
| Shared by        | All instances of the class                  | Unique for each object                    |

Example:
```java
class Counter {
    static int count = 0; // static
    int id;               // non-static

    Counter() {
        count++;
        id = count;
    }
}
```

---

### Q 1 **(c) What do you mean by command line parameters?**
> **Command line parameters** are values passed to the `main()` method of a Java program **at runtime** through the terminal or command prompt.

Example:
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, " + args[0]);
    }
}
```

If you run the program with:  
`java Hello Alice`  
Output: `Hello, Alice`

---

### Q 1 **(d) Explain the various uses of keyword `final`**
The **`final` keyword** in Java can be used in three main contexts:

#### i) Final variable
- Value **cannot be changed** once assigned.
```java
final int x = 10;
// x = 20; // Error!
```

#### ii) Final method
- **Cannot be overridden** by subclasses.
```java
class A {
    final void show() {
        System.out.println("Final method");
    }
}
```

#### iii) Final class
- **Cannot be extended** (inherited).
```java
final class MyClass { }
// class SubClass extends MyClass { } // Error!
```

---

### Q 2 (a) What is an interface in Java? How does it differ from a class? 
> An **interface** in Java is like a contract that defines a set of methods that a class must implement. It doesn’t contain any implementation itself (except for default or static methods, introduced in later versions of Java). Instead, it only declares method signatures.

For example:
```java
interface Animal {
    void eat();
    void sleep();
}
```

> Any class that wants to be considered an `Animal` must implement these methods:
```java
class Dog implements Animal {
    public void eat() {
        System.out.println("Dog eats.");
    }

    public void sleep() {
        System.out.println("Dog sleeps.");
    }
}
```

Interfaces can also include constants (which are implicitly `public`, `static`, and `final`) and, from Java 8 onwards, default and static methods with implementations.

---

#### Here are the main differences:

1. **Implementation vs. Declaration**:
   - A class can provide full implementation (i.e., method bodies).
   - An interface only declares methods by default—no bodies (unless using `default` or `static` methods).

2. **Instantiation**:
   - You can create objects from a class.
   - You cannot create objects directly from an interface.

3. **Multiple Inheritance**:
   - Java classes cannot extend more than one class (no multiple inheritance of classes).
   - But a class **can implement multiple interfaces**, making interfaces a way to achieve multiple inheritance.

4. **Constructors**:
   - Classes can have constructors.
   - Interfaces **cannot** have constructors.

5. **Field Behavior**:
   - Fields in a class can be anything: static, final, instance-based, etc.
   - Fields in an interface are always `public static final`.

---

> In short, use a **class** when you want to create reusable code with both data and behavior. Use an **interface** when you want to define a set of rules or capabilities that multiple unrelated classes can implement.

---

### Q 2 (b) What are Packages?
> In Java, **packages** are used to group related classes, interfaces, and sub-packages together. Think of a package as a folder in your file system — it helps organize your code and avoid class name conflicts.
- A **package** is a namespace that organizes a set of related classes and interfaces.
- Java has built-in packages like `java.util`, `java.io`, etc.
- You can also **create your own packages**.

#### Benefits of using packages:
- Better organization of code.
- Avoids naming conflicts.
- Provides access protection (using `public`, `protected`, etc.).
- Makes it easier to locate and use classes.

---

###  How to Create and Use a Package

#### 1. **Create a Package**

Let’s say we want to create a package called `mypack`.

Create a file named `Message.java`:
```java
package mypack;

public class Message {
    public void show() {
        System.out.println("Hello from mypack!");
    }
}
```

> The **first line** must be `package mypack;` and the file must be saved inside a folder named `mypack`.

#### 2. **Use the Package**

Create another file in a different folder (or same level) named `Test.java`:
```java
import mypack.Message;

public class Test {
    public static void main(String[] args) {
        Message msg = new Message();
        msg.show();
    }
}
```

#### 3. **Compile and Run**

```bash
# Compile the package class
javac -d . Message.java

# Compile the class using the package
javac Test.java

# Run the program
java Test
```

> `-d .` tells the compiler to place the package in the correct folder structure.

---

Great question! Let’s break this down step by step.

---

### ✅ **What is an Exception in Java?**

An **exception** in Java is an event that disrupts the normal flow of a program. It usually occurs when something goes wrong during program execution, like dividing by zero, accessing a null reference, or trying to read a file that doesn’t exist.

Java provides a powerful **exception handling mechanism** using:

- `try` - block of code to monitor for exceptions
- `catch` - block that handles the exception
- `finally` - block that always executes (used for cleanup)
- `throw` - used to explicitly throw an exception
- `throws` - declares an exception in method signature

---

### ✅ **Custom Exceptions in Java**

Sometimes the built-in exceptions aren't enough. You can create your own **custom exceptions** by extending the `Exception` class (for checked exceptions) or `RuntimeException` (for unchecked exceptions).

---

### 🧪 Sample Code: Custom Exception

Let's create a custom exception called `InvalidAgeException` to handle invalid age input.

#### Step 1: Create the custom exception
```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

#### Step 2: Use it in application logic
```java
public class VoterRegistration {
    
    public static void checkAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or older to register.");
        } else {
            System.out.println("You are eligible to register to vote.");
        }
    }

    public static void main(String[] args) {
        try {
            checkAge(16);  // Try with different ages to test
        } catch (InvalidAgeException e) {
            System.out.println("Exception Caught: " + e.getMessage());
        }
    }
}
```

#### Output:
```
Exception Caught: Age must be 18 or older to register.
```

---

#### 🔍 Summary

- **Exceptions** are runtime errors you can catch and handle.
- You can create **custom exceptions** by extending `Exception` or `RuntimeException`.
- This is useful for handling **domain-specific errors** in a clear and controlled way.

Let me know if you want an example with multiple custom exceptions or exception chaining!
