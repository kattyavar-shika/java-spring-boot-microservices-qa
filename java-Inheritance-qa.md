# Java Inheritance Questions & Answer

### Disclaimer

This content is created for educational purposes and aims to assist learners in preparing for Java, Spring Boot, and
Microservices-related interviews.

- The questions and answers are intended to provide insight into common interview topics and are based on publicly
  available knowledge, research, and common practices within the industry.
- This content is not directly copied from any specific sources and is the result of personal understanding, research,
  and synthesis.
- If any external content, text, or ideas have been used, they have been cited and attributed appropriately (where
  applicable).

If you are the owner of any content referenced or used in this document and believe that proper attribution has not been
provided, please contact the author so that the necessary changes can be made.

---

**Note**: By using this repository or document, you acknowledge that the information provided is for educational
purposes only, and you are responsible for verifying the accuracy of the content before relying on it for professional
purposes.

## What is inheritance in Java?
<details>
<summary>Answer</summary>

- Inheritance is a fundamental object-oriented programming concept where a new class (subclass or child class) acquires properties and behaviors (fields and methods) from an existing class (superclass or parent class). 
- It allows for code reusability and method overriding.

</details>

## Explain the difference between extends and implements in Java.
<details>
<summary>Answer</summary>

- **extends:** Used to inherit from a class (i.e., create a subclass).
- **implements:** Used by a class to implement an interface. A class can implement multiple interfaces but can extend only one class.

</details>

## Can a constructor be inherited in Java?
<details>
<summary>Answer</summary>

- No, constructors are not inherited by subclasses in Java. However, a subclass can invoke the constructor of the superclass using super().
- Explanation: The constructor of a subclass can call the constructor of the superclass, but the constructor itself is not inherited, and it cannot be overridden.

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    // No constructor inherited from Parent
    Child() {
        super();  // You must call the Parent constructor explicitly
        System.out.println("Child Constructor");
    }
}

public class Main {
    public static void main(String[] args) {
        Child c = new Child();
    }
}

```
</details>

## What is the significance of super keyword in Java inheritance?
<details>
<summary>Answer</summary>

- The super keyword is used to
  - Access superclass methods that have been overridden in the subclass.
  - Access superclass fields that are hidden by subclass fields.
  - Call the superclass constructor.

```java
class Parent {
    int x = 10;
    void display() {
        System.out.println("Parent display");
    }
}

class Child extends Parent {
    int x = 20;
    
    void display() {
        super.display();  // Calls Parent's display method
        System.out.println("Child display");
    }

    void show() {
        System.out.println("Parent's x: " + super.x);  // Access Parent's x
    }
}

public class Main {
    public static void main(String[] args) {
        Child c = new Child();
        c.display();
        c.show();
    }
}

```
</details>

## Can a class extend multiple classes in Java? Why or why not?
<details>
<summary>Answer</summary>

- No, Java does not support multiple inheritance for classes. A class can only extend one class. This is done to avoid complexities and ambiguities (like the diamond problem).
- However, a class can implement multiple interfaces, which allows the class to inherit method signatures from more than one source.

</details>

## Can a class inherit from more than one class in Java? Why or why not?
<details>
<summary>Answer</summary>

- **No**, Java does not support multiple inheritance through classes to avoid ambiguity. 
- A class can inherit from only one superclass, but it can implement multiple interfaces.

</details>

## What is method overriding in Java?
<details>
<summary>Answer</summary>

- Method overriding occurs when a subclass provides a specific implementation of a method that is already defined in its superclass. 
- The method signature (name, return type, and parameters) must remain the same in both the subclass and superclass.

</details>

## What is the difference between method overloading and method overriding in Java?
<details>
<summary>Answer</summary>

- **Method Overloading:** Occurs when two or more methods in the same class have the same name but different parameters (different type, number, or both).
- **Method Overriding:** Occurs when a subclass provides a specific implementation of a method that is already defined in its superclass with the same method signature.

</details>

## What is the use of the super keyword in Java?
<details>
<summary>Answer</summary>

- The super keyword is used to refer to the immediate parent class of the current object. 
- It is used to call superclass constructors, methods, or access superclass fields.

</details>

## Can we override a private or final method in Java?
<details>
<summary>Answer</summary>

- **No**, we cannot override a private or final method. private methods are not visible to subclasses, and final methods cannot be overridden because they are considered "locked."

</details>

## What is the difference between super() and this() in Java constructors?
<details>
<summary>Answer</summary>

- **super():** Calls the constructor of the parent class (superclass).
- **this():** Calls another constructor in the current class (same class) with a different number or type of parameters.

</details>

##  What is the significance of the Object class in Java inheritance?
<details>
<summary>Answer</summary>

- The Object class is the root of the class hierarchy in Java. 
- Every class in Java implicitly inherits from Object, unless it explicitly extends another class. 
- It provides fundamental methods such as toString(), equals(), hashCode(), and getClass().

</details>

## What will happen if a subclass does not call the superclass constructor?
<details>
<summary>Answer</summary>

-  If the subclass does not explicitly call the superclass constructor, Java automatically calls the no-argument constructor of the superclass. 
- If the superclass does not have a no-argument constructor, a compile-time error will occur unless the subclass explicitly calls a superclass constructor using super().

</details>

## Explain the concept of constructor chaining in Java.
<details>
<summary>Answer</summary>

- Constructor chaining refers to the process where a constructor in a subclass calls a constructor in its superclass (via super()). 
- It can also refer to the process of calling one constructor from another constructor in the same class using this().

- Example 
```java
class Employee {
    private String name;
    private int age;
    private double salary;

    // Constructor 1: Takes all properties as parameters
    public Employee(String name, int age, double salary) {
        this.name = name;
        this.age = age;
        this.salary = salary;
    }

    // Constructor 2: Calls Constructor 1 using 'this()'
    public Employee(String name, int age) {
        this(name, age, 50000.0);  // Default salary value
    }

    // Constructor 3: Calls Constructor 2 using 'this()'
    public Employee(String name) {
        this(name, 30);  // Default age value
    }

    public void displayInfo() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
    }

    public static void main(String[] args) {
        Employee emp1 = new Employee("Alice", 28, 60000.0);
        Employee emp2 = new Employee("Bob", 35);  // Uses Constructor 2
        Employee emp3 = new Employee("Charlie");  // Uses Constructor 3

        emp1.displayInfo();
        System.out.println();
        emp2.displayInfo();
        System.out.println();
        emp3.displayInfo();
    }
}

```

- Note:
  - this() Must Be First: The this() call must always be the first statement in the constructor. No other code (like variable assignments or method calls) can appear before it.

Example:

```java
class Employee {
    private String name;
    private int age;

    // Constructor 1
    public Employee(String name, int age) {
        System.out.println("Before calling this constructor");  // Illegal, cannot be here!
        this.name = name;
        this.age = age;
    }
}

public class Main {
    public static void main(String[] args) {
        Employee emp = new Employee("Alice", 25);
    }
}

```
  - Cannot Mix this() with super(): If you are also calling a superclass constructor with super(), you can only use one of them (this() or super()) in a constructor. Both this() and super() cannot appear in the same constructor.

</details>

## Can you instantiate an abstract class in Java? Why or why not?
<details>
<summary>Answer</summary>

-  No, an abstract class cannot be instantiated directly because it may contain abstract methods that do not have a body. However, you can instantiate a subclass that provides implementations for all abstract methods.

</details>

## What is a final class in Java?
<details>
<summary>Answer</summary>

- A final class in Java cannot be subclassed. This is used to prevent inheritance and ensure that the class implementation remains unchanged.

</details>

## What is the use of the @Override annotation in Java?
<details>
<summary>Answer</summary>

- The @Override annotation is used to indicate that a method is intended to override a method in its superclass. It helps the compiler catch errors if the method signature does not match the one in the superclass.

</details>

## What will happen if a subclass does not override a method of its superclass?
<details>
<summary>Answer</summary>

- If a subclass does not override a method from its superclass, the subclass inherits the method from the superclass and uses that inherited method. 
- If the method is abstract in the superclass, the subclass must override it.

</details>

## Explain the concept of "dynamic method dispatch" in Java.
<details>
<summary>Answer</summary>

- Dynamic method dispatch is a process in Java where the method to be called is determined at runtime rather than compile time. 
- It occurs when a subclass overrides a method, and an object of the subclass is referred to by a superclass reference variable.

</details>

## What is the relationship between composition and inheritance?
<details>
<summary>Answer</summary>

- Both are object-oriented design principles, but they serve different purposes
  - **Inheritance** represents an "is-a" relationship. One class is a type of another.
  - **Composition** represents a "has-a" relationship. One class contains or is composed of other objects. Composition is often preferred over inheritance to avoid the pitfalls of tight coupling in class hierarchies.

</details>

## What is the instanceof operator used for in Java?
<details>
<summary>Answer</summary>

- The instanceof operator is used to test whether an object is an instance of a particular class or subclass. It helps avoid ClassCastException during type casting by ensuring that the object is of the correct type.

</details>

## What is multiple inheritance and how is it handled in Java?
<details>
<summary>Answer</summary>

- Java does not support multiple inheritance through classes to avoid ambiguity. However, multiple inheritance is supported through interfaces. 
- A class can implement multiple interfaces, which allows it to inherit behavior from multiple sources.

</details>

## What is an interface in Java, and how does it relate to inheritance?
<details>
<summary>Answer</summary>

- An interface is a reference type in Java, similar to a class, but it can only contain abstract methods (until Java 8, when default methods were introduced). A class implements an interface, inheriting the abstract methods defined in the interface, and it must provide implementations for those methods.

</details>

## How does Java handle method resolution when a method is overridden in multiple classes in the inheritance chain?
<details>
<summary>Answer</summary>

- Java uses dynamic method dispatch to resolve which method to call at runtime. 
- If a method is overridden in multiple classes in the inheritance chain, the method that gets invoked is the one in the most specific subclass, i.e., the class of the actual object being referred to.

</details>

## What is the Diamond Problem in Java, and how does Java handle it?
<details>
<summary>Answer</summary>

- The Diamond Problem occurs in languages that support multiple inheritance, where a class can inherit from two classes that both have a common ancestor, leading to ambiguity about which method to inherit. 
- In Java, this problem does not occur with classes because Java does not allow multiple inheritance with classes. However, the problem can arise when a class implements multiple interfaces that contain the same method signature.

- Example 

```java
interface A {
    void show();
}

interface B extends A {
    void display();
}

interface C extends A {
    void print();
}

class D implements B, C {
    @Override
    public void show() {
        System.out.println("Show method");
    }

    @Override
    public void display() {
        System.out.println("Display method");
    }

    @Override
    public void print() {
        System.out.println("Print method");
    }
}


```
- In this example, interfaces B and C both extend interface A and define their own methods. However, there is no conflict in the method signature of show() because Java handles this situation without ambiguity. 
- Each interface (B and C) has its own distinct methods, and the class D can implement both interfaces without problems. 
- Java allows the developer to explicitly provide implementations for the methods from both interfaces.

- However, if there were a conflict, for example, if both interfaces had the same default method with the same signature, Java would require the implementing class to override that method explicitly to resolve the ambiguity. 
- This is possible due to Java's support for default methods introduced in Java 8.

- Example : Example of potential conflict (with default methods):

```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {
    default void show() {
        System.out.println("B's show");
    }
}

interface C extends A {
    default void show() {
        System.out.println("C's show");
    }
}

class D implements B, C {
    @Override
    public void show() {
        System.out.println("D's show");
    }
}

```

- In the above code, class D is implementing both B and C, which both have default show() methods. 
- Since Java cannot decide which default method to inherit, it requires the class D to explicitly override the show() method to resolve the conflict. 
- If D does not provide an implementation, a compile-time error will occur.

</details>

## How does Java resolve the ambiguity caused by the Diamond Problem when default methods are involved?
<details>
<summary>Answer</summary>

- ava resolves the ambiguity caused by the Diamond Problem with default methods using the rule of explicit overriding. 
- If a class implements multiple interfaces that define default methods with the same signature, the class must explicitly override the method to resolve the conflict. 
- If the class does not override the method, it will result in a compile-time error.

- In the case where a class inherits from multiple interfaces with default methods that have conflicting implementations, the compiler will generate an error, and the developer will need to provide a specific method implementation to resolve the ambiguity.

</details>

## In Java, when a class implements multiple interfaces that have conflicting default methods, how can you explicitly call the default methods from both interfaces in the implementing class? Please demonstrate with an example.
<details>
<summary>Answer</summary>

- In Java, if a class implements multiple interfaces that provide conflicting default methods, the class will need to resolve the ambiguity by explicitly overriding the method. 
- If you want to call both conflicting default methods from the interfaces, you can use the **InterfaceName.super.methodName()** syntax.

- Example 

```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {
    default void show() {
        System.out.println("B's show");
    }
}

interface C extends A {
    default void show() {
        System.out.println("C's show");
    }
}

class D implements B, C {
    @Override
    public void show() {
        // Call B's show if you want to do it..
        B.super.show();
        
        // Call C's show
        C.super.show();
        
        // Custom implementation in D
        System.out.println("D's show");
    }
}

```

</details>

## Consider the following interfaces and class in Java:
```java
interface A {
    default void show() {
        System.out.println("A's show");
    }
}

interface B extends A {
    default void show() {
        System.out.println("B's show");
    }
}

interface C extends A {
    default void show() {
        System.out.println("C's show");
    }
}

class D implements B, C {
    @Override
    public void show() {
        B.super.show(); // Calls B's default show()
        C.super.show(); // Calls C's default show()
        System.out.println("D's show"); // D's own implementation
    }
}
```

- You create an instance of class D and assign it to references of interface A, interface B, and interface C. 
- For each of the following assignments, explain the output when show() is called on the reference:

```java
A objA = new D();
B objB = new D();
C objC = new D();

```
<details>
<summary>Answer</summary>

- we will get output as below 

```java
B's show
C's show
D's show
```

-  Even though the reference type is A, B, C, the actual object is of type D. Since D overrides the show() method, D's overridden show() method is called.
- Inside D.show(), the B.super.show() and C.super.show() methods are invoked, printing:
</details>


## Consider the following code:

```java
class Parent {
    static void display() {
        System.out.println("Parent's static display");
    }
}

class Child extends Parent {
    static void display() {
        System.out.println("Child's static display");
    }
}

public class Main {
    public static void main(String[] args) {
        Parent parent = new Parent();
        Parent childAsParent = new Child();
        Child child = new Child();

        parent.display();            // What will this print?
        childAsParent.display();     // What will this print?
        child.display();             // What will this print?
    }
}

```

- What is the output when parent.display(), childAsParent.display(), and child.display() are called?
- Why does the output appear the way it does, even though childAsParent is an instance of Child?

<details>
<summary>Answer</summary>

- **parent.display()**
  - Output: "Parent's static display"
  - Explanation
    - Since parent is a reference of type Parent, and static methods are resolved based on the reference type (at compile time), it calls the static method from Parent, not Child. 
    - Static methods do not exhibit polymorphism.
- **childAsParent.display()**
  - Output: "Parent's static display"
  - Explanation
    -  Although childAsParent is actually pointing to an instance of Child, the reference type is still Parent. Static methods are resolved based on the reference type at compile time, so Parent's static method is called, not Child's.
- **child.display()**
  - Output: "Child's static display"
  - Explanation
    -  Since child is a reference of type Child, the static method from Child is called. Static methods are resolved based on the reference type, so here Child's static method is called.
  
- **Key Concepts**
  - Static Method Hiding: Static methods can be "hidden" in a subclass when a subclass defines a static method with the same signature. This is not the same as overriding.
  - Compile-time Resolution: Static methods are resolved at compile time based on the reference type, not the object type.
  - No Polymorphism for Static Methods: Static methods do not exhibit polymorphism, meaning they are not dynamically dispatched like instance methods are.
  - Polymorphism for Instance Methods: Instance methods, on the other hand, are resolved at runtime based on the actual object type, allowing for polymorphism.
</details>


## What is meant by the term "covariant return type"?
<details>
<summary>Answer</summary>

-  Covariant return type refers to the ability of a subclass to override a method from its superclass and return a type that is a subclass of the return type declared in the superclass method.
- In Java, this is allowed for methods that are overridden in subclasses, as long as the return type in the subclass is a more specific type (a subclass) than the one in the parent class.
- For example, if a parent class method returns Animal, a subclass method can return a more specific type like Dog or Cat (which are both subclasses of Animal).

- Example 

```java
class Animal {
    public Animal getAnimal() {
        return new Animal();
    }
}

class Dog extends Animal {
    @Override
    public Dog getAnimal() {
        return new Dog();
    }
}

```

- Here, Dog is a covariant return type because it’s a subclass of Animal, and it is allowed to override the method from Animal and return a Dog.

</details>


## Consider the following code:
```java
class Parent {
    public void display(final int x) {
        System.out.println("Parent: " + x);
    }
}

class Child extends Parent {
    @Override
    public void display(int x) {
        x = x + 1; // Modifying the parameter x
        System.out.println("Child: " + x);
    }
}

public class Main {
    public static void main(String[] args) {
        Parent p = new Child();
        p.display(10);  // What will be the output?
    }
}

```

- What will the output be when p.display(10) is called?
- Can you modify the parameter x in the Child class's display() method? Why or why not?
- Is it necessary to declare x as final in the Child class method? Explain why.

<details>
<summary>Answer</summary>

- What will the output be when p.display(10) is called?
  - ans = Child: 11
  - Explanation:
    - Even though the reference is of type Parent, the object is of type Child, so the display() method from the Child class is called. The parameter x is passed as 10, and within the Child class, it is incremented (x = x + 1). 
    - The final value of x is 11, and the output is "Child: 11".
-  Can you modify the parameter x in the Child class's display() method? Why or why not?
  - Answer: Yes, you can modify x in the Child class.
    - In the Parent class, the parameter x is marked final, which means it cannot be modified inside the Parent class method. However, in the Child class, the final modifier does not carry over to the overridden method. This allows you to modify the parameter x in the Child class.
- Is it necessary to declare x as final in the Child class method? Explain why.
  - Answer: No, it is not necessary to declare x as final in the Child class.
    - The final modifier on method parameters only applies to the method in the class where it is declared. When overriding the method in the Child class, you are free to omit the final keyword. The parameter x is local to the method, and final does not need to be repeated in the child method.

</details>


## Consider the following code:

```java
class Parent {
    public void doSomething() throws IOException {
        System.out.println("Parent: Doing something with an IO operation.");
    }
}

class Child extends Parent {
    @Override
    public void doSomething() throws FileNotFoundException {
        System.out.println("Child: Doing something specific.");
    }
}

public class Main {
    public static void main(String[] args) throws IOException {
        Parent p = new Child();
        p.doSomething();
    }
}
```

- **Questions**
  - 1 . What will be the output of the program when p.doSomething() is called?
  - 2 . In the Child class, can you change the exception thrown from IOException to FileNotFoundException? Why or why not?
  - 3 . What would happen if you try to change the exception thrown in Child to a broader exception (for example, Exception)?
  - 4 . What would happen if you remove the throws declaration from the Child class method?
  - 5 . Can you change the checked exception IOException to an unchecked exception like NullPointerException in the Child class? Why or why not?


<details>
<summary>Answer</summary>

- 1 What will be the output of the program when p.doSomething() is called?
  - Output : Child: Doing something specific.
  - Explanation:
    - Although the reference p is of type Parent, the actual object is of type Child. This results in method overriding: the doSomething() method in the Child class is invoked. The output is "Child: Doing something specific.", as the method in the Child class is executed.

-  2 In the Child class, can you change the exception thrown from IOException to FileNotFoundException? Why or why not?
  - Answer: Yes, you can change the exception thrown from IOException to FileNotFoundException.
    - Why? FileNotFoundException is a subclass of IOException. Java allows you to throw more specific exceptions (subtypes of the parent exception) in the overridden method, which is known as **covariant exception handling**.
    - Since FileNotFoundException is a more specific exception than IOException, this is allowed, and the Child class can narrow the exception type.

-  3 What would happen if you try to change the exception thrown in Child to a broader exception (for example, Exception)?
  - Answer: You cannot change the exception to a broader exception (e.g., Exception)
    - Why? Java’s method overriding rules do not allow the subclass method to throw a broader checked exception than the parent method. If the superclass method declares a checked exception (e.g., IOException), the subclass method can only throw that same exception or one of its subtypes, not a superclass of that exception.
    - If you try to change the exception to a broader exception, such as Exception, it will result in a compilation error

- 4 What would happen if you remove the throws declaration from the Child class method?
  - If you remove the throws declaration in the Child class method, it will compile and run without an error only if the Child class method does not actually throw the checked exception.
  - However, if the method in Child throws an exception (like FileNotFoundException), and you remove the throws declaration, it will result in a compilation error because the subclass method must declare the exceptions that it throws if they are checked exceptions.
  - In Java, if the method signature of the superclass includes a throws clause, the subclass must also include the appropriate throws clause unless the exception is handled inside the subclass method.

- 5 Can you change the checked exception IOException to an unchecked exception like NullPointerException in the Child class? Why or why not?
  - Answer: Yes, you can change a checked exception (like IOException) to an unchecked exception (like NullPointerException) in the Child class.
    - Why? Java allows a subclass to throw a more specific unchecked exception when overriding a method. Since NullPointerException is an unchecked exception (a subclass of RuntimeException), you are allowed to throw it even though the Parent class method throws a checked exception (IOException).
    - This is legal because unchecked exceptions are not subject to the same rules as checked exceptions. You don’t need to declare them in the throws clause, nor do you need to handle them with try-catch.
    

- Summary : 

| **Case** | **Super Class Method** | **Sub Class Method** | **Allowed or Not Allowed** | **Explanation** |
|----------|------------------------|----------------------|---------------------------|-----------------|
| **1. Throwing the same checked exception** | `throws IOException` | `throws IOException` | Allowed | The subclass can throw the same checked exception as the superclass. |
| **2. Throwing a more specific checked exception (covariant exceptions)** | `throws IOException` | `throws FileNotFoundException` | Allowed | The subclass can throw a subclass of the checked exception. |
| **3. Throwing an unchecked exception (RuntimeException)** | `throws IOException` | `throws NullPointerException` | Allowed | The subclass can throw an unchecked exception (a subclass of `RuntimeException`) even if the superclass throws a checked exception. |
| **4. Throwing a broader checked exception** | `throws IOException` | `throws Exception` | Not Allowed | The subclass cannot throw a broader checked exception than the superclass. If the superclass throws `IOException`, the subclass cannot throw `Exception`. |
| **5. Removing the throws declaration** | `throws IOException` | (No `throws` declaration) | Allowed (if no exception is thrown) | The subclass method can omit the `throws` declaration, but only if it does not throw any exception (checked or unchecked). If the method throws a checked exception, the `throws` declaration must be included. |
| **6. Throwing a new checked exception** | `throws IOException` | `throws SQLException` | Allowed (if the new exception is a subclass) | The subclass can throw a different checked exception only if it is a **subclass** of the one declared in the superclass method's `throws` clause. |
| **7. Throwing multiple exceptions** | `throws IOException` | `throws IOException, SQLException` | Allowed | The subclass can throw multiple exceptions, as long as they are valid (i.e., checked exceptions are listed in the `throws` clause). |
| **8. Throwing an unchecked exception when superclass throws nothing** | No `throws` declaration | `throws ArithmeticException` | Allowed | The subclass can throw any unchecked exception even if the superclass method does not declare any exceptions. |
| **9. Throwing a checked exception when superclass throws nothing** | No `throws` declaration | `throws IOException` | Not Allowed | The subclass cannot throw a checked exception if the superclass method does not throw any. This would cause a compilation error. |

</details>

##  What is the contract between equals() and hashCode() in Java?
<details>
<summary>Answer</summary>

- The equals() and hashCode() methods in Java have the following contract:
  - **Consistency:** If two objects are considered equal by the equals() method, their hashCode() values must be equal. This is essential for objects stored in hash-based collections like HashSet or HashMap.
  - **Reflexive:** An object must be equal to itself. That is, a.equals(a) should return true.
  - **Symmetric:** If a.equals(b) returns true, then b.equals(a) must also return true.
  - **Transitive:** If a.equals(b) is true and b.equals(c) is true, then a.equals(c) should also be true.
  - **Consistent:** Multiple invocations of a.equals(b) should consistently return the same result, provided no properties used in the comparison have been modified.

</details>

## What happens if you override equals() but not hashCode()?
<details>
<summary>Answer</summary>

- If you override equals() but not hashCode(), your objects may behave incorrectly when used in hash-based collections like HashMap, HashSet, or Hashtable.
- Hash-based collections rely on both equals() and hashCode() for correct functionality. If two objects are considered equal by equals(), they must have the same hash code. If this contract is violated, the collection may not behave as expected.

- Example of incorrect behavior:

```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Person person = (Person) obj;
        return age == person.age && name.equals(person.name);
    }
}

public class Main {
    public static void main(String[] args) {
        Person p1 = new Person("John", 30);
        Person p2 = new Person("John", 30);

        HashSet<Person> set = new HashSet<>();
        set.add(p1);
        set.add(p2);
        
        System.out.println(set.size());  // Output: 2, despite p1 and p2 being equal
    }
}

```

- In this example, even though p1 and p2 are logically equal (based on the equals() method), they have different hash codes (since hashCode() was not overridden). As a result, they are stored in different buckets in HashSet, and the size is incorrectly reported as 2.

</details>
 
## What is the difference between Composition and Inheritance in Java?
<details>
<summary>Answer</summary>

- Inheritance is an IS-A relationship. It allows a class (subclass) to inherit properties and behaviors (methods) from another class (superclass). It's a mechanism for code reuse, where a subclass can extend a superclass, inheriting all or some of its properties and behaviors.

- Example of Inheritance:

```java
class Animal {
    void eat() {
        System.out.println("Eating...");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Barking...");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherited method
        dog.bark(); // Dog's own method
    }
}

```

- **Composition** is a HAS-A relationship. It refers to the design principle where one class contains instances of other classes, effectively "composing" behavior by delegating tasks to objects of other classes. In composition, a class doesn't inherit the behavior from another class; instead, it contains an instance of another class and uses it to perform the required actions.

- Example of Composition:


```java
class Engine {
    void start() {
        System.out.println("Engine starting...");
    }
}

class Car {
    private Engine engine;  // Composition (Car has an Engine)

    Car(Engine engine) {
        this.engine = engine;
    }

    void drive() {
        engine.start(); // Delegating the start functionality to the Engine class
        System.out.println("Driving...");
    }
}

public class Main {
    public static void main(String[] args) {
        Engine engine = new Engine();
        Car car = new Car(engine);
        car.drive();
    }
}

```
- **In summary:**
  - Inheritance is best when the relationship between the two classes is "IS-A".
  - Composition is preferred when the relationship is "HAS-A".

</details>

## Can you provide an example where composition is better than inheritance?
<details>
<summary>Answer</summary>

- Example: A Car and an Engine
  - Let’s consider a scenario where we model a Car class. The Car class HAS-A Engine. Using inheritance would make less sense because a Car IS NOT A Engine.
  - Using composition is a better design choice because it allows the Car class to have different types of engines without needing to extend multiple classes, which could become unwieldy.

```java
class Engine {
    void start() {
        System.out.println("Engine starting...");
    }
}

class ElectricEngine extends Engine {
    void start() {
        System.out.println("Electric engine starting silently...");
    }
}

class Car {
    private Engine engine;  // Composition

    Car(Engine engine) {
        this.engine = engine;
    }

    void drive() {
        engine.start(); // Delegate to the engine
        System.out.println("Car is driving...");
    }
}

public class Main {
    public static void main(String[] args) {
        Engine electricEngine = new ElectricEngine();
        Car electricCar = new Car(electricEngine);
        electricCar.drive();
    }
}

```

- The Car class HAS-A Engine.
- We can easily switch the Car's engine type from ElectricEngine to GasolineEngine without modifying the Car class. This promotes loose coupling.

</details>

##  What are the disadvantages of using inheritance?
<details>
<summary>Answer</summary>

- While inheritance is a powerful feature in Java, it has several disadvantages:
  - **Tight coupling:** Inheritance creates a tight coupling between the parent and child classes. Any change in the parent class may impact all child classes, making the system more difficult to maintain.
  - **Fragile base class:** As the codebase evolves, changes in the superclass can inadvertently break the subclasses. For instance, if a superclass method is modified or removed, all subclasses that override or depend on that method may break.
  - **Inflexibility:** A class can inherit from only one parent class (single inheritance), which limits the ability to inherit behavior from multiple sources. This is less flexible compared to composition, where an object can use multiple components with different behaviors.
  - **Difficult to modify:** Inheritance hierarchies can become deep and complex, making it difficult to modify or extend functionality without impacting many parts of the codebase.

</details>

## What are the advantages of composition over inheritance?
<details>
<summary>Answer</summary>

- Composition offers several advantages over inheritance:
  - **Loose coupling:** Composition allows for a loose coupling between classes. You can change the behavior of a class by changing its components without altering the class itself. This is easier to maintain and extend.
  - **Flexibility:** Composition allows an object to dynamically change the behavior of its components at runtime. For instance, a Car can have its engine swapped for a different engine type without affecting the Car class itself.
  - **Reuse:** You can reuse components in multiple classes. For example, the Engine class can be used in both Car and Boat classes, promoting better code reuse.

</details>

## Can you mix Inheritance and Composition in your design?
<details>
<summary>Answer</summary>

- Yes, you can combine inheritance and composition in your design, and often, this is a good practice. While inheritance is used to model "IS-A" relationships (e.g., a Dog IS A Animal), composition is used for "HAS-A" relationships (e.g., a Car HAS A Engine).

```java
class Animal {
    void sleep() {
        System.out.println("Animal sleeping...");
    }
}

class Dog extends Animal {
    private Engine engine;  // Composition (Dog has an Engine)

    Dog(Engine engine) {
        this.engine = engine;
    }

    void bark() {
        System.out.println("Dog barking...");
    }

    void startEngine() {
        engine.start();  // Delegating to the Engine object
    }
}

```

</details>

## Can you provide a scenario where inheritance is the best option?
<details>
<summary>Answer</summary>

- Inheritance is the best option when there is a strong "IS-A" relationship between the parent and the child classes. This is useful when the subclass represents a more specific version of the superclass.

```java
class Shape {
    void draw() {
        System.out.println("Drawing a shape");
    }
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing a circle");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape shape = new Shape();
        shape.draw();  // Drawing a shape

        Shape circle = new Circle();
        circle.draw();  // Drawing a circle
    }
}

```

- Here, Circle IS A Shape. Inheritance works well because the relationship between the two is clearly an IS-A relationship, and it allows for code reuse and polymorphism.

</details>

## What is the difference between Composition and Aggregation in Java?
<details>
<summary>Answer</summary>

- **Composition**
  - Strong "HAS-A" relationship.
  - The child object cannot exist without the parent object.
  - The parent object owns the child object, and the child object’s lifecycle is managed by the parent.
  - If the parent is destroyed, the child objects are also destroyed.

Example : A House HAS-A Room. The Room cannot exist without the House, so when the House is destroyed, the Room will also be destroyed.

```java
class Room {
    // Room-specific attributes and behaviors
}

class House {
    private Room room; // Composition (House owns Room)

    public House() {
        room = new Room();
    }

    // House-specific behaviors
}

```

- **Aggregation**
  - Weaker "HAS-A" relationship.
  - The child object can exist independently of the parent object.
  - The parent class does not own the child object. The child object may belong to multiple parents or exist independently.
  - If the parent is destroyed, the child object can continue to exist.

Example :  A Department HAS-A Employee. The Employee can exist independently and can belong to multiple departments.

```java
class Employee {
    private String name;
    
    // Employee-specific behaviors
}

class Department {
    private Employee employee; // Aggregation (Department does not own Employee)

    // Department-specific behaviors
}

```

</details>


## What is an Interface in Java?
<details>
<summary>Answer</summary>

- An interface in Java is a reference type, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces cannot have instance fields, and all methods in an interface are implicitly abstract (unless they are default or static methods). 
- A class implements an interface, providing concrete implementations for the interface's methods.

```java
interface Animal {
    void sound();  // abstract method
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}

```

</details>

## What is the difference between an interface and an abstract class?
<details>
<summary>Answer</summary>

- **Abstract class** can have both abstract (no body) and concrete methods (with body), while an **interface** can have abstract methods (except for default, static methods, private method (java 9 onwards.)).
- A class can extend only one abstract class, but it can implement multiple interfaces.
- Abstract classes can have member variables, while interfaces can only have constants (public, static, final variables).
- Interfaces are ideal for defining a contract, whereas abstract classes are useful when some shared functionality needs to be provided.

</details>

## Can an interface have a constructor?
<details>
<summary>Answer</summary>

- No, interfaces cannot have constructors. Constructors are used to initialize objects, but interfaces cannot be instantiated directly. 
- They are meant to be implemented by classes, which can provide their own constructors.

</details>

## What is the purpose of default methods in interfaces?
<details>
<summary>Answer</summary>

- Default methods, introduced in Java 8, allow interfaces to have methods with an implementation. This helps maintain backward compatibility when adding new methods to an interface. 
- Classes that implement the interface can use the default method or override it if necessary.

```java
interface Animal {
    default void eat() {
        System.out.println("Eating...");
    }
}

class Dog implements Animal {
    // Can override eat() or use the default method
}

```
</details>

##  What happens if a class implements two interfaces with the same default method?
<details>
<summary>Answer</summary>

- If a class implements two interfaces that both have the same default method, the class will encounter a conflict and need to provide its own implementation to resolve the ambiguity.

Example 

```java
interface Animal {
  default void sound() {
    System.out.println("Animal sound");
  }
}

interface Dog {
  default void sound() {
    System.out.println("Bark");
  }
}

class MixedBreed implements Animal, Dog {
  public void sound() {
    System.out.println("Mixed breed sound");
  }
}

```

</details>

## Can an interface extend another interface?
<details>
<summary>Answer</summary>

- Yes, an interface can extend another interface. The extending interface inherits the abstract methods from the parent interface. A class that implements the child interface must provide implementations for all methods of the parent and child interfaces.
- Example

```java
interface Animal {
    void sound();
}

interface Dog extends Animal {
    void bark();
}

class Labrador implements Dog {
    public void sound() {
        System.out.println("Animal sound");
    }

    public void bark() {
        System.out.println("Woof");
    }
}

```

</details>

## Can an interface extend multiple interfaces?
<details>
<summary>Answer</summary>

- Yes, an interface can extend multiple interfaces, thereby inheriting their abstract methods.

```java
// A class can implement multiple interfaces
interface Animal {
    void sound();
}

interface Swimmer {
    void swim();
}

class Dog implements Animal, Swimmer {
    public void sound() {
        System.out.println("Bark");
    }

    public void swim() {
        System.out.println("Dog is swimming");
    }
}

// An interface can extend multiple interfaces
interface DogBehavior extends Animal, Swimmer {
    void fetch();
}

```
</details>

## Can we implement an interface in another interface?
<details>
<summary>Answer</summary>

- An interface cannot be implemented by another interface, but it can be extended by another interface. A class is responsible for implementing the methods defined in an interface, whereas an interface can inherit methods from another interface using the extends keyword.

Example

```java
interface Animal {
    void sound();
}

// Correct: An interface can extend another interface
interface Dog extends Animal {
    void bark();
}

```

</details>

## How many interfaces can a class implement, and how many interfaces can an interface extend?
<details>
<summary>Answer</summary>

- A class can implement multiple interfaces (Java allows multiple inheritance for interfaces, unlike classes).
- An interface can also extend multiple interfaces. An interface is allowed to inherit the abstract methods of multiple other interfaces.

```java
// A class can implement multiple interfaces
interface Animal {
    void sound();
}

interface Swimmer {
    void swim();
}

class Dog implements Animal, Swimmer {
    public void sound() {
        System.out.println("Bark");
    }

    public void swim() {
        System.out.println("Dog is swimming");
    }
}

// An interface can extend multiple interfaces
interface DogBehavior extends Animal, Swimmer {
    void fetch();
}

```
</details>

## Can an Interface have a main method in Java?
<details>
<summary>Answer</summary>

- Yes, an interface can have a main method in Java, just like any other class. 
- The main method in an interface can be used for testing purposes or to provide a default behavior for the interface.

Example

```java
interface MyInterface {
    static void main(String[] args) {
        System.out.println("Main method in an interface");
    }
}

```

- However, to run the program, you would need to call the interface's main method directly, not through an instance or implementation.

</details>

## What is a Marker Interface in Java?
<details>
<summary>Answer</summary>

-  A marker interface is an interface with no methods or fields.
- It serves as a "tag" to indicate that a class possesses some special behavior or should be treated in a particular way by the JVM or other frameworks. 
- Examples include Serializable and Cloneable.

```java
interface MyMarkerInterface {
    // No methods
}

class MyClass implements MyMarkerInterface {
    // Class with no additional behavior
}

```

- Use case: A marker interface is often used to indicate that a class has certain properties or capabilities, such as being serializable or clonable.

</details>

## Can an Interface have static methods?
<details>
<summary>Answer</summary>

- Yes, starting from Java 8, interfaces can have static methods. These methods must have a body, and they cannot be overridden by implementing classes. 
- Static methods in interfaces are typically used to provide utility methods related to the interface.

```java
interface MyInterface {
    static void staticMethod() {
        System.out.println("This is a static method in an interface.");
    }
}

class MyClass implements MyInterface {
    // Cannot override static methods.
}

public class Main {
    public static void main(String[] args) {
        MyInterface.staticMethod(); // Calling static method directly on the interface.
    }
}

```
</details>

## Can we instantiate an interface in Java?
<details>
<summary>Answer</summary>

-  No, you cannot instantiate an interface directly in Java. 
- Interfaces are abstract by nature and cannot be directly instantiated. 
- However, you can create an instance of a class that implements the interface.

```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() {
        System.out.println("Bark");
    }
}

public class Test {
    public static void main(String[] args) {
        // Animal a = new Animal(); // This will throw an error because you cannot instantiate an interface
        Animal dog = new Dog();  // Valid: Dog implements Animal
        dog.sound();  // Output: Bark
    }
}

```
</details>

##  What is the purpose of the @FunctionalInterface annotation in Java?
<details>
<summary>Answer</summary>

- The @FunctionalInterface annotation is used to indicate that an interface is intended to be a functional interface. 
- A functional interface is an interface with exactly one abstract method. 
- It can optionally have multiple default or static methods.

- The annotation is not mandatory but serves as a marker to tell the compiler that the interface should have a single abstract method, making it suitable for lambda expressions and method references.

```java
@FunctionalInterface
interface MyFunctionalInterface {
    void doSomething();  // Exactly one abstract method
    
    // Optional default method
    default void defaultMethod() {
        System.out.println("This is a default method.");
    }
}

```
</details>

## Is it possible to override a default method in an interface?
<details>
<summary>Answer</summary>

- Yes, it is possible to override a default method in an interface. 
- When a class implements an interface and provides its own implementation for a default method, it overrides the default method.

- However, overriding a default method is optional, and if the class doesn't override it, the default implementation from the interface will be used.


```java
interface Animal {
    default void sound() {
        System.out.println("Some animal sound");
    }
}

class Dog implements Animal {
    // Override default method
    public void sound() {
        System.out.println("Bark");
    }
}

class Cat implements Animal {
    // No override, uses default method
}

public class Test {
    public static void main(String[] args) {
        Animal dog = new Dog();
        dog.sound();  // Output: Bark
        
        Animal cat = new Cat();
        cat.sound();  // Output: Some animal sound (default method)
    }
}

```

</details>

## Can an interface be generic in Java?
<details>
<summary>Answer</summary>

- Yes, interfaces can be generic in Java. 
- A generic interface allows you to define methods with type parameters, making it possible to use different types when implementing the interface.

```java
interface Box<T> {
    void setItem(T item);
    T getItem();
}

class StringBox implements Box<String> {
    private String item;

    public void setItem(String item) {
        this.item = item;
    }

    public String getItem() {
        return item;
    }
}

public class Test {
    public static void main(String[] args) {
        Box<String> stringBox = new StringBox();
        stringBox.setItem("Hello");
        System.out.println(stringBox.getItem());  // Output: Hello
    }
}

```
</details>


## What are the different types of inner classes in Java?
<details>
<summary>Answer</summary>

**There are four types of inner classes in Java:**
- **Member Inner Class:** A class defined within another class, but outside any method or constructor. It can access the members (including private members) of the outer class.

```java
class Outer {
    private int x = 10;
    
    class Inner {
        void display() {
            System.out.println(x);  // Can access outer class member x
        }
    }
}

```

- **Local Inner Class:** A class defined within a method or a block of code. It can access local variables and parameters of the method if they are declared final or effectively final.

```java
class Outer {
    void myMethod() {
        final int y = 5;
        class LocalInner {
            void display() {
                System.out.println(y);  // Can access final local variable y
            }
        }
        LocalInner li = new LocalInner();
        li.display();
    }
}

```

- **Anonymous Inner Class:** A class without a name, defined at the point of instantiation. Typically used to implement interfaces or extend a class for a one-time use.
```java
interface Hello {
    void greet();
}

public class Outer {
    public static void main(String[] args) {
        Hello hello = new Hello() {  // Anonymous inner class implementing Hello interface
            public void greet() {
                System.out.println("Hello, World!");
            }
        };
        hello.greet();
    }
}

```

- **Static Nested Class:** A static class defined within another class. It does not have access to the instance variables and methods of the outer class, but it can access static members of the outer class.

```java
class Outer {
    static int x = 10;
    
    static class StaticNested {
        void display() {
            System.out.println(x);  // Can access static member x of outer class
        }
    }
}

```

</details>

## What is the difference between a static nested class and a regular inner class?
<details>
<summary>Answer</summary>

**Static Nested Class:**
- Defined with the static keyword.
- It does not have access to the instance variables and methods of the outer class.
- Can be instantiated without creating an instance of the outer class.
- Can access only static members of the outer class.

**Regular Inner Class (Non-static):**
- Can access both static and non-static members (including private) of the outer class.
- Requires an instance of the outer class to be instantiated.
- Has an implicit reference to the outer class instance.

```java
class Outer {
    static int staticVar = 10;
    int instanceVar = 20;
    
    static class StaticNested {
        void display() {
            System.out.println(staticVar);  // Can access staticVar, but not instanceVar
        }
    }
    
    class Inner {
        void display() {
            System.out.println(instanceVar);  // Can access both static and instance variables
        }
    }
}

```

</details>

## Can an inner class access the members of the outer class?
<details>
<summary>Answer</summary>

- Yes, an inner class can access both instance and static members of the outer class. 
- However, the level of access depends on whether the inner class is static or non-static.
- Non-static inner class can access all members (including private) of the outer class because it has a reference to the outer class instance.
- Static inner class can only access static members of the outer class.

</details>

## What is the purpose of using anonymous inner classes?
<details>
<summary>Answer</summary>

-  Anonymous inner classes are used when you need to implement an interface or extend a class just once and don't want to create a separate named class. 
- They provide a concise way to implement methods of interfaces or abstract classes in place, which helps reduce boilerplate code.
- Commonly used for event handling in GUI programming (e.g., ActionListener in Swing).
- Often used with functional interfaces (lambdas can be a more modern alternative).

```java
interface MyInterface {
    void display();
}

public class Test {
    public static void main(String[] args) {
        MyInterface obj = new MyInterface() {
            public void display() {
                System.out.println("Anonymous Inner Class!");
            }
        };
        obj.display();
    }
}

```

</details>

##  How can you instantiate a non-static inner class?
<details>
<summary>Answer</summary>

- To instantiate a non-static inner class, you need to first create an instance of the outer class. 
- Once the outer class instance is created, you can instantiate the inner class using the outer class instance.

Example 

```java
class Outer {
    private String message = "Hello from Outer class";

    class Inner {
        void display() {
            System.out.println(message);  // Accesses outer class's private field
        }
    }

    public static void main(String[] args) {
        Outer outer = new Outer();  // Create instance of Outer class
        Outer.Inner inner = outer.new Inner();  // Create instance of Inner class
        inner.display();  // Call inner class method
    }
}

```
</details>

## What is the significance of this keyword inside an inner class?
<details>
<summary>Answer</summary>

- The this keyword inside an inner class refers to the current instance of the inner class itself, not the outer class. 
- However, you can refer to the outer class’s instance using OuterClassName.this.

- this: Refers to the instance of the inner class.
- OuterClassName.this: Refers to the instance of the outer class.


```java
class Outer {
    private String outerMessage = "Outer class message";

    class Inner {
        private String innerMessage = "Inner class message";

        void showMessages() {
            // Refers to the inner class instance
            System.out.println("Inner: " + this.innerMessage);  
            // Refers to the outer class instance
            System.out.println("Outer: " + Outer.this.outerMessage); 
        }
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.showMessages();
    }
}

```

</details>

## Can an interface extend a class?
<details>
<summary>Answer</summary>

- **No**, an interface cannot extend a class. An interface can only extend another interface. In Java, interfaces support multiple inheritance, whereas classes support single inheritance.
- An interface cannot implement methods from a class, but it can implement default methods.

- However, a class can implement multiple interfaces, and an interface can extend multiple interfaces.

```java
interface A {
    void methodA();
}

interface B extends A {
    void methodB();
}

class C implements B {
    public void methodA() {
        System.out.println("Method A");
    }
    
    public void methodB() {
        System.out.println("Method B");
    }
}

```

</details>