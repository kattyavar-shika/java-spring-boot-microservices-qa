# Java **static** Questions & Answer

### Disclaimer

This content is created for educational purposes and aims to assist learners in preparing for Java, Spring Boot, and Microservices-related interviews.

- The questions and answers are intended to provide insight into common interview topics and are based on publicly available knowledge, research, and common practices within the industry.
- This content is not directly copied from any specific sources and is the result of personal understanding, research, and synthesis.
- If any external content, text, or ideas have been used, they have been cited and attributed appropriately (where applicable).

If you are the owner of any content referenced or used in this document and believe that proper attribution has not been provided, please contact the author so that the necessary changes can be made.

---

**Note**: By using this repository or document, you acknowledge that the information provided is for educational purposes only, and you are responsible for verifying the accuracy of the content before relying on it for professional purposes.

## What is a static variable in Java?
<details>
<summary> Answer</summary>

- A **static variable** is a variable that belongs to the class rather than instances of the class. It is shared by all instances of that class. It is initialized only once when the class is loaded into memory, and it retains its value across method calls and object instances.
- **Declaration:** A static variable is declared using the static keyword.
- Example

```java
 class Example {
  static int count = 0;  // static variable

  Example() {
    count++;  // Increment count for each object created
  }

  void display() {
    System.out.println(count);
  }
}

public class Test {
  public static void main(String[] args) {
    Example obj1 = new Example();
    Example obj2 = new Example();
    obj1.display();  // Output: 2
    obj2.display();  // Output: 2
  }
}

```
- In this example, both obj1 and obj2 share the same count variable.

</details>

## What is a static method in Java?
<details>
<summary> Answer</summary>

- A static method belongs to the class rather than instances of the class. You can call a static method without creating an object of the class. Static methods can only directly access other static variables and static methods in the class. They cannot access instance variables or instance methods.
- Declaration: Static methods are declared using the static keyword.
- Example
```java
class Example {
    static void staticMethod() {
        System.out.println("This is a static method.");
    }
}

public class Test {
    public static void main(String[] args) {
        Example.staticMethod();  // Calling static method without creating an object
    }
}

```

</details>

## Can a static method access instance variables in Java?
<details>
<summary> Answer</summary>

- **No**, a static method cannot directly access instance variables or instance methods because static methods belong to the class itself, while instance variables belong to individual objects. However, you can access instance variables by creating an object inside the static method.
- Example
```java
class Example {
    int instanceVar = 5;  // instance variable

    static void staticMethod() {
        // Error: Cannot access instanceVar directly in static method
        // System.out.println(instanceVar);

        Example obj = new Example();
        System.out.println(obj.instanceVar);  // Accessing instance variable through an object
    }
}

public class Test {
    public static void main(String[] args) {
        Example.staticMethod();
    }
}

```
</details>

## What is a static block in Java?
<details>
<summary> Answer</summary>

- A **static block** (also known as a static initialization block) is used to initialize static variables. It is executed when the class is loaded into memory, before any instance of the class is created. Static blocks are typically used for complex initialization of static variables.
- Example
```java
class Example {
    static int staticVar;

    static {
        staticVar = 100;  // Static block to initialize static variables
        System.out.println("Static block executed");
    }

    static void display() {
        System.out.println("Static variable value: " + staticVar);
    }
}

public class Test {
    public static void main(String[] args) {
        Example.display();  // Static block is executed when the class is loaded
    }
}

```

- Output:
```cmd
Static block executed
Static variable value: 100
```
</details>

## What is the difference between a static and a non-static variable in Java?
<details>
<summary> Answer</summary>

- The main differences between static and non-static variables are as follows:

| **Aspect**               | **Static Variable**                               | **Non-static Variable**                       |
|--------------------------|--------------------------------------------------|----------------------------------------------|
| **Belongs to**            | The class itself                                 | Each instance of the class                   |
| **Memory Allocation**     | Allocated once when the class is loaded into memory | Allocated each time an object is created     |
| **Access**                | Can be accessed without creating an object       | Must be accessed via an instance of the class|
| **Sharing**               | Shared across all instances of the class         | Different for each instance of the class     |

- Static variable example:
```java
class Example {
    static int staticVar = 10;
}
```
- Non-static variable example:
```java
class Example {
    int nonStaticVar = 20;
}

```
</details>


## Can you override a static method in Java?

<details>
<summary> Answer</summary>

- **No**, you cannot **override** a static method in Java because static methods are associated with the class itself, not the instance. 
- However, you can **hide** a static method by defining a static method with the same signature in a subclass.
- Example
```java
class Parent {
    static void staticMethod() {
        System.out.println("Parent static method");
    }
}

class Child extends Parent {
    static void staticMethod() {
        System.out.println("Child static method");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent.staticMethod();  // Output: Parent static method
        Child.staticMethod();   // Output: Child static method
    }
}

```

Even though the method signature is the same, this is not overriding but rather method hiding because static methods are resolved at compile-time based on the reference type.

</details>

## What is the purpose of a static class in Java?
<details>
<summary> Answer</summary>

- A static class is a nested class that is associated with its outer class but does not require an instance of the outer class to be instantiated. Static nested classes can access only the static members of the outer class. They are useful when the nested class doesn't need access to instance-specific data of the outer class.
- Example
```java
class Outer {
    static int staticVar = 10;

    static class StaticNestedClass {
        void display() {
            System.out.println("Accessing static variable of outer class: " + staticVar);
        }
    }
}

public class Test {
    public static void main(String[] args) {
        Outer.StaticNestedClass obj = new Outer.StaticNestedClass();
        obj.display();  // Output: Accessing static variable of outer class: 10
    }
}

```

</details>

## Can a static method be synchronized in Java?
<details>
<summary> Answer</summary>

- Yes, a **static method** can be synchronized in Java. 
- Synchronizing a static method means that the method is locked on the **class-level monitor**, meaning only one thread can execute that static method for the entire class at any given time.
- Example
```java
class Example {
    static synchronized void staticMethod() {
        System.out.println("This method is synchronized.");
    }
}

public class Test {
    public static void main(String[] args) {
        Example.staticMethod();  // Accessing synchronized static method
    }
}

```

In this case, multiple threads will have to wait if they are attempting to call the staticMethod() concurrently, because the lock is on the class itself.

</details>


## What happens if we declare a static variable inside a method in Java?
<details>
<summary> Answer</summary>

- A **static variable** cannot be declared inside a method in Java because static variables are associated with the class and not with instances or method calls. 
- Declaring a static variable inside a method would violate the principle of static variables, which must exist as long as the class is loaded.
- Error example 
```java
class Example {
    void method() {
        static int x = 10;  // Error: 'static' modifier is not allowed here
    }
}

```
Static variables must be declared at the class level.

</details>

## What is the output of the following code?
```java
class Test {
    static int x = 5;

    public static void main(String[] args) {
        System.out.println(x);
        x = 10;
        System.out.println(x);
    }
}

```
<details>
<summary> Answer</summary>

- Output
```cmd
5
10

```
- Explanation: The static variable x is initialized to 5, then its value is changed to 10 and printed again. Since x is a static variable, it is shared across all instances, and the change affects the value globally.

</details>

##  What happens when a thread acquires a lock on a static synchronized method in Java? Will other threads be able to access other static or non-static methods in the same class while the lock is held?
<details>
<summary> Answer</summary>

- When a thread acquires a lock on a static synchronized method in Java, it locks the class-level monitor, meaning that no other thread can execute any static synchronized method of that class while the lock is held.
- However, the thread holding the lock on the static synchronized method does not block other threads from executing non-static methods of the same class. Non-static methods are not affected by the class-level lock because they are tied to instance-level locks.
- Here’s a detailed breakdown of the behavior:
- -  **Static Synchronized Methods:**
    - - When a thread enters a static synchronized method, it acquires the class-level lock.
    - - While the thread holds this lock, other threads are blocked from entering any other static synchronized method in the same class. This is because all static synchronized methods in the class are synchronized on the same class-level monitor.
- - **Other Static Methods:**
    - - Even if other static methods exist in the same class, they are locked by the same monitor and hence cannot be executed concurrently with the synchronized static method.
    - - If Thread 1 holds the lock on staticMethod1(), Thread 2 cannot enter staticMethod2() (even if it is another static method) until Thread 1 exits the synchronized static method.
- - **Non-Static Methods:**
  - - Non-static methods are tied to the instance-level lock of the object on which they are invoked.
  - - These methods are not blocked by the lock on the static synchronized method, as non-static methods do not share the same lock. This means that while a thread is executing a static synchronized method, other threads can still execute non-static methods on different or the same instances of the class.

- Example
```java
class Example {
    static synchronized void staticMethod() {
        System.out.println("Static synchronized method started.");
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
        System.out.println("Static synchronized method finished.");
    }

    static synchronized void staticMethod2() {
        System.out.println("Another static synchronized method.");
    }

    void nonStaticMethod() {
        System.out.println("Non-static method.");
    }
}

public class Test {
    public static void main(String[] args) {
        Example obj1 = new Example();
        Example obj2 = new Example();

        // Thread 1 calls staticMethod
        new Thread(() -> obj1.staticMethod()).start();

        // Thread 2 tries to call staticMethod2 (but it will wait until Thread 1 exits staticMethod)
        new Thread(() -> obj2.staticMethod2()).start();

        // Thread 3 can still call nonStaticMethod since it is not blocked by static synchronization
        new Thread(() -> obj1.nonStaticMethod()).start();
    }
}

```

- **Key points**
  - A static synchronized method locks the class-level monitor.
  - Other static synchronized methods are blocked until the first thread releases the lock.
  - Non-static methods can still be accessed concurrently by other threads, even when a static synchronized method is being executed by a thread.

</details>

## What is a static import in Java, and how does it work?
<details>
<summary> Answer</summary>

- In Java, static import allows you to access static members (fields and methods) of a class without needing to use the class name to qualify them.
- This feature helps in making the code more concise and readable, especially when you are dealing with frequently used static members like constants or utility methods.

- **Syntax**
  - To import a static member, you use the import static keyword followed by the class name and the static member.

```java
import static packageName.ClassName.memberName;

// Alternatively, you can import all static members of a class:
import static packageName.ClassName.*;

```

- Example
```java
import static java.lang.Math.PI;
import static java.lang.Math.pow;

public class StaticImportExample {
    public static void main(String[] args) {
        // Using static imported constants and methods
        System.out.println("Value of PI: " + PI);  // No need to write Math.PI
        System.out.println("2^3: " + pow(2, 3));  // No need to write Math.pow(2, 3)
    }
}

```
- Explanation
  - In the above example, we imported the static members PI and pow() from the Math class.

- **Key Points:**
  - Static import can only be used for static fields and static methods.
  - It improves readability when you have commonly used static methods or constants.
  - Overusing static import can lead to name conflicts, especially when you import static members from multiple classes that have methods or fields with the same name. It can also make code harder to read if not used carefully.
- **When to Use Static Import?**
  - It's best used when you are dealing with constants (e.g., Math.PI, Integer.MAX_VALUE) or utility methods (e.g., Collections.sort(), Math.pow()) where adding the class name every time would be cumbersome.
- **Potential Pitfalls:**
  - Name Conflicts: If two classes have the same static method or variable names, static import can lead to ambiguity.

```java
import static java.util.Collections.*;  // static import for all methods in Collections
import static java.util.Arrays.*;        // static import for all methods in Arrays

// If both Arrays and Collections have methods with the same name, like `sort()`, there can be a conflict.

```


</details>