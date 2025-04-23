# [4th_End_Sem](2k24_End_Sem.pdf)

- ## JAVA
- ## Discrete Mathematics
- ## DCC
- ## Entrepreneurship
- ## Unix OS


## JAVA

<img src="Java_End_Sem_2024.png">

### **1. What is an abstract class?**
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

### **2. What is the difference between static and non-static variables?**

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

### **3. What do you mean by command line parameters?**
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

### **4. Explain the various uses of keyword `final`**
The **`final` keyword** in Java can be used in three main contexts:

#### a) Final variable
- Value **cannot be changed** once assigned.
```java
final int x = 10;
// x = 20; // Error!
```

#### b) Final method
- **Cannot be overridden** by subclasses.
```java
class A {
    final void show() {
        System.out.println("Final method");
    }
}
```

#### c) Final class
- **Cannot be extended** (inherited).
```java
final class MyClass { }
// class SubClass extends MyClass { } // Error!
```

---
