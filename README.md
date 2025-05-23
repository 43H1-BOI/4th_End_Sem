# 📘 4th_End_Sem Preparation

[📄 2k24 End Sem](2k24_End_Sem.pdf)

## 📚 Subjects

- [JAVA](#java)
- [Discrete Mathematics](#discrete-mathematics)
- [DCC](#dcc)
- [Entrepreneurship](#entrepreneurship)
- [Unix OS](#unix-os)

---

## JAVA

![Java Question Paper](Java_End_Sem_2024.png)

---

### Q1 (a) What is an abstract class?

An **abstract class** in object-oriented programming is a class that **cannot be instantiated directly**—it serves as a **blueprint for other classes**.

- It may contain **abstract methods** (no body) and **fully implemented methods**.
- Used to define a **base class** with some functionality and enforce implementation of key behavior in subclasses.

```java
abstract class Animal {
    abstract void makeSound();  // abstract method
    void sleep() {
        System.out.println("Sleeping...");
    }
}
```

---

### Q1 (b) What is the difference between static and non-static variables?

| Feature             | Static Variable                            | Non-static Variable                       |
|---------------------|---------------------------------------------|-------------------------------------------|
| Belongs to          | The **class**, not an instance              | A **specific instance** (object)          |
| Memory allocation   | Once, at the time of class loading          | Every time a new object is created        |
| Accessed by         | Class name or object                        | Only by object                            |
| Shared by           | All instances of the class                  | Unique for each object                    |

```java
class Counter {
    static int count = 0;
    int id;

    Counter() {
        count++;
        id = count;
    }
}
```

---

### Q1 (c) What do you mean by command line parameters?

**Command line parameters** are values passed to the `main()` method of a Java program during execution via terminal.

```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, " + args[0]);
    }
}
```

Example command:
```bash
java Hello Alice
```

Output:
```
Hello, Alice
```

---

### Q1 (d) Explain the various uses of keyword `final`

The `final` keyword is used in Java to restrict the user.

#### i) Final variable
Value **cannot be changed** once assigned.

```java
final int x = 10;
// x = 20; // Error!
```

#### ii) Final method
**Cannot be overridden** by subclasses.

```java
class A {
    final void show() {
        System.out.println("Final method");
    }
}
```

#### iii) Final class
**Cannot be extended** (no inheritance).

```java
final class MyClass { }
// class SubClass extends MyClass {} // Error!
```

---

### Q2 (a) What is an interface in Java? How does it differ from a class?

An **interface** defines a set of abstract methods (by default) that a class must implement.

```java
interface Animal {
    void eat();
    void sleep();
}
```

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

Interfaces can also have:
- Constants (implicitly `public static final`)
- `default` and `static` methods (Java 8+)

#### Differences Between Interface and Class

1. **Methods**: Class can have implemented methods; interface methods are abstract by default.
2. **Instantiation**: Classes can be instantiated; interfaces cannot.
3. **Inheritance**: A class can implement multiple interfaces, but extend only one class.
4. **Constructors**: Classes can have constructors; interfaces can't.
5. **Field Behavior**: Interface fields are always `public static final`.

> Use a class for defining structure and behavior.  
> Use an interface for defining rules or capabilities.

---

### Q2 (b) What are Packages?

A **package** is a namespace that organizes related classes and interfaces.

#### Benefits:
- Better organization
- Avoid naming conflicts
- Access control
- Easier to locate and reuse classes

#### How to Create and Use a Package

##### Step 1: Create a Package

```java
package mypack;

public class Message {
    public void show() {
        System.out.println("Hello from mypack!");
    }
}
```

📁 Save this in a folder named `mypack`.

##### Step 2: Use the Package

```java
import mypack.Message;

public class Test {
    public static void main(String[] args) {
        Message msg = new Message();
        msg.show();
    }
}
```

##### Step 3: Compile and Run

```bash
javac -d . mypack/Message.java
javac Test.java
java Test
```

> `-d .` creates the package folder structure.

---

### Q3 (a) What is an Exception in Java? How can you create custom exceptions?

An **exception** is an abnormal condition that disrupts program execution.

Java provides:
- `try`, `catch`, `finally`
- `throw`, `throws`

#### Creating a Custom Exception

##### Step 1: Define the custom exception

```java
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}
```

##### Step 2: Use it in your application

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
            checkAge(16);
        } catch (InvalidAgeException e) {
            System.out.println("Exception Caught: " + e.getMessage());
        }
    }
}
```

**Output**:
```
Exception Caught: Age must be 18 or older to register.
```

### Q4 (a) Explain following layout managers with appropriate example: FlowLayout, BorderLayout, and GridLayout.

In Java Swing and AWT, **layout managers** control how components are arranged within containers:  
- **FlowLayout** arranges components in a left-to-right flow, starting new rows as needed.  
- **BorderLayout** divides a container into five regions—North, South, East, West, and Center—for placing single components in each region.  
- **GridLayout** places components in a grid of equally sized cells determined by specified rows and columns.  

**Serialization** is the process of converting an object's state into a byte stream for storage or transmission, and **deserialization** is the reverse process of reconstructing the object from that byte stream.  

---

### a) Layout Managers

#### FlowLayout  
> The `FlowLayout` manager lays out components in a directional flow, much like text in a paragraph, wrapping to a new line when there is no more horizontal space. It is the default layout for every `JPanel` in Swing.  
##### Example
```java
import javax.swing.*;
import java.awt.*;

public class FlowLayoutExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("FlowLayout Demo");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new FlowLayout(FlowLayout.CENTER, 10, 10)); 
        frame.add(new JButton("Button 1"));
        frame.add(new JButton("Button 2"));
        frame.add(new JButton("Button 3"));
        frame.pack();
        frame.setVisible(true);
    }
}
```
- `FlowLayout.CENTER` centers components horizontally.  
- Gaps of 10 pixels are set between components and between rows .

#### BorderLayout  
>  `BorderLayout` arranges components in five regions: North, South, East, West, and Center. Each region can contain at most one component, and extra space is allocated to the center by default.  
##### Example
```java
import javax.swing.*;
import java.awt.*;

public class BorderLayoutExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("BorderLayout Demo");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new BorderLayout(5, 5)); // hgap=5, vgap=5
        frame.add(new JButton("North"), BorderLayout.NORTH);
        frame.add(new JButton("South"), BorderLayout.SOUTH);
        frame.add(new JButton("East"),  BorderLayout.EAST);
        frame.add(new JButton("West"),  BorderLayout.WEST);
        frame.add(new JButton("Center"),BorderLayout.CENTER);
        frame.setSize(400, 200);
        frame.setVisible(true);
    }
}
```
- The two-parameter constructor `BorderLayout(int hgap, int vgap)` specifies horizontal and vertical gaps.  

#### GridLayout  
> `GridLayout` divides the container into a grid of equal-sized cells specified by row and column counts . Each component occupies exactly one cell, and resizing the container adjusts all cells proportionally.  
##### Example
```java
import javax.swing.*;
import java.awt.*;

public class GridLayoutExample {
    public static void main(String[] args) {
        JFrame frame = new JFrame("GridLayout Demo");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new GridLayout(2, 3, 5, 5)); // 2 rows, 3 cols, gaps=5
        for (int i = 1; i <= 6; i++) {
            frame.add(new JButton("Button " + i));
        }
        frame.pack();
        frame.setVisible(true);
    }
}
```
- The constructor `GridLayout(rows, cols, hgap, vgap)` specifies gaps between cells citeturn3search0.

---

### Q2 (b) What is Object Seriali>ation and Deserialization? How can you read and write objeets to a file in Java (Give Complete Example)?
#### Definitions  
- **Serialization** converts an object's state (its non-transient, non-static fields) into a platform-independent byte stream for persistence or network transfer citeturn2search0.  
- **Deserialization** reconstructs the object from its byte stream, restoring it in memory with the original state citeturn2search0.

#### Implementing Serialization  
1. **Implement `Serializable`**: Mark the class with `implements Serializable`.  
2. **(Optional) `serialVersionUID`**: Declare a `private static final long serialVersionUID` to ensure version compatibility.  
3. **Use `ObjectOutputStream`**: Wrap a `FileOutputStream` to call `writeObject()`.

#### Implementing Deserialization  
1. **Use `ObjectInputStream`**: Wrap a `FileInputStream` to call `readObject()`.  
2. **Cast returned `Object`**: Cast the result of `readObject()` back to the original class type.

#### Complete Example

```java
import java.io.*;

// 1. Define a serializable class
class Person implements Serializable {
    private static final long serialVersionUID = 1L;
    String name;
    int age;
    
    Person(String name, int age) {
        this.name = name;
        this.age  = age;
    }
    
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class SerializeDemo {
    public static void main(String[] args) {
        Person p = new Person("Alice", 30);
        
        // 2. Serialize to file
        try (FileOutputStream fos = new FileOutputStream("person.ser");
             ObjectOutputStream oos = new ObjectOutputStream(fos)) {
             
            oos.writeObject(p);
            System.out.println("Object serialized to person.ser");
            
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // 3. Deserialize from file
        try (FileInputStream fis = new FileInputStream("person.ser");
             ObjectInputStream ois = new ObjectInputStream(fis)) {
             
            Person p2 = (Person) ois.readObject();
            System.out.println("Deserialized object: " + p2);
            
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

- The `transient` field `password` is not serialized and thus becomes `null` upon deserialization.  
- Exceptions `IOException` and `ClassNotFoundException` must be handled when reading objects citeturn2search0.

---

## Discrete Mathematics
*Coming soon...*

---

## DCC
*Coming soon...*

---

## Entrepreneurship
*Coming soon...*

---

## Unix OS
*Coming soon...*

---
