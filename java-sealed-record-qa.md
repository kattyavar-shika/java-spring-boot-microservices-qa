# Java Sealed & Record Questions & Answer

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

## What are Sealed Classes in Java?
<details>
<summary>Answer</summary>

- Sealed classes are a new feature introduced in Java 15 as a preview feature and became stable in Java 17. 
- A sealed class is a class that restricts which other classes or interfaces can extend or implement it. 
- You can specify which classes or interfaces are allowed to subclass a sealed class by using the permits keyword.

Example 

```java
public sealed class Vehicle permits Car, Bike { 
    // class definition
}

```

- Here, the Vehicle class is sealed and can only be extended by Car and Bike.

</details>

## How do you define a Sealed Class in Java?
<details>
<summary>Answer</summary>

- To define a sealed class, use the sealed modifier in the class declaration, and then specify which classes can extend it using the permits keyword.

Example 

```java
public sealed class Animal permits Dog, Cat { 
    // class definition
}

```

- In this case, only Dog and Cat can extend Animal. Any other class trying to extend Animal will result in a compilation error.

</details>

##  Can a Sealed Class be Abstract or Final?
<details>
<summary>Answer</summary>

- Yes, a sealed class can be abstract or final, but with some restrictions:
  - If a sealed class is abstract, then other classes can extend it (within the permitted set).
  - If a sealed class is final, it cannot have any subclasses at all, even within the permitted set. The class is essentially a leaf in the class hierarchy.

Example :

```java
public sealed class Shape permits Circle, Square { 
    // abstract or final is allowed
}

public final class Circle extends Shape {
    // Circle cannot be extended
}

```
</details>

## What is the benefit of using Sealed Classes?
<details>
<summary>Answer</summary>

Sealed classes provide several advantages:

- Control Over Inheritance: It allows the class author to control which classes can extend or implement the sealed class, making it useful in domain modeling where only specific subtypes are permitted.
- Exhaustiveness Checks: When used with switch statements (since Java 17), sealed classes allow the compiler to check exhaustiveness. If a switch expression does not cover all the permitted subclasses, the compiler will generate an error, ensuring all cases are handled.

```java
switch (shape) {
    case Circle c -> System.out.println("Circle");
    case Square s -> System.out.println("Square");
    // No need to add 'default' because the compiler knows all subclasses are handled
}

```

</details>

## Can Sealed Classes have Interfaces?
<details>
<summary>Answer</summary>

- Yes, a sealed class can implement interfaces in addition to restricting subclassing. 
- You can combine the functionality of sealing the class with the flexibility of interfaces.


```java
public sealed class Shape implements Drawable permits Circle, Square { 
    // class definition
}

```

- In this case, Shape implements the Drawable interface and can only be extended by Circle and Square.

</details>

## What is the relationship between Sealed Classes and Records in Java?
<details>
<summary>Answer</summary>

- A record in Java is a special kind of class designed for immutable data carriers, and it is implicitly final. 
- Sealed classes and records can be used together in some cases, 
- but there are differences:
  - A record is always implicitly final, so it cannot be subclassed.
  - A sealed class can allow specific classes to extend it, meaning you control which classes can extend it.

```java
public sealed interface Shape permits Circle, Square { }

public record Circle(double radius) implements Shape { }
public record Square(double sideLength) implements Shape { }

```

- Here, the Shape interface is sealed, but Circle and Square are records implementing it.

</details>

## Can a Sealed Class be Extended by Other Sealed Classes?
<details>
<summary>Answer</summary>

- Yes, a sealed class can be extended by another sealed class. This allows for a controlled inheritance chain.

Example 

```java
public sealed class Shape permits Circle, Square { }

public sealed class Circle extends Shape permits Oval { } // Circle is also sealed
public final class Oval extends Circle { }

```

- In this case, Circle is sealed and permits only Oval to extend it.

</details>

## What is the difference between a Sealed Class and an Abstract Class?
<details>
<summary>Answer</summary>

- **Abstract Class:** An abstract class can be extended by any other class unless the class is marked final. It provides no restrictions on which classes can inherit from it.
- **Sealed Class:** A sealed class restricts which classes can extend it. You explicitly specify allowed subclasses using the permits keyword. It allows better control over the class hierarchy and improves exhaustiveness checks during compilation.

</details>


## What is the permits keyword in Sealed Classes?
<details>
<summary>Answer</summary>

- The permits keyword is used to define which classes or interfaces are allowed to extend or implement a sealed class or interface. 
- It follows the sealed class definition.

Example 

```java
public sealed class Vehicle permits Car, Bike { 
    // only Car and Bike can extend Vehicle
}

```
</details>


## Can a Sealed Class be extended by a Non-Sealed Class?
<details>
<summary>Answer</summary>

- Yes, a sealed class can be extended by a non-sealed class. 
- A non-sealed class can extend a sealed class, but it is no longer restricted to a specific set of subclasses. 
- It can be further subclassed by any class.

- **Sealed Class:** Restricts the set of allowed subclasses.
- **Non-Sealed Class:** Removes the restriction, allowing the class to be subclassed freely.

```java
public sealed class Vehicle permits Car, Bike { }

public non-sealed class Car extends Vehicle { }  // This is allowed

public class Sedan extends Car { }  // Sedan can extend Car because Car is non-sealed

```

In this example:

- Car is marked as non-sealed, so it can be extended by Sedan.
- Bike is restricted and cannot have subclasses outside the permits list.

</details>


##  Can a Sealed Class implement multiple interfaces?
<details>
<summary>Answer</summary>

- Yes, a sealed class can implement multiple interfaces. 
- There is no restriction on the number of interfaces a sealed class can implement, just like any regular class.

```java
public sealed class Shape implements Drawable, Movable permits Circle, Square { }

public final class Circle extends Shape {
    public void draw() { /* Drawing logic */ }
    public void move() { /* Move logic */ }
}

```
</details>

##  Can a Sealed Class be Subclassed by an Anonymous Class?
<details>
<summary>Answer</summary>

- No, anonymous classes cannot subclass a sealed class because an anonymous class does not declare its type explicitly, which would violate the restrictions placed by the permits clause of the sealed class.

Example 
```java
public sealed class Animal permits Dog, Cat { }

public class Test {
    public static void main(String[] args) {
        Animal myAnimal = new Animal() {}; // Error: Cannot subclass a sealed class with an anonymous class
    }
}

```

- The attempt to create an anonymous subclass of Animal would result in a compilation error because Animal is sealed and does not permit anonymous subclassing.


</details>

## Can Sealed Classes Have Constructors?
<details>
<summary>Answer</summary>

- Yes, sealed classes can have constructors, just like any other class. 
- The constructor is typically used to initialize fields or control how instances of the class (or its subclasses) are created. 
- In the case of sealed classes, the constructor is often **protected or private** to restrict instantiation to the permitted subclasses.
 
- A sealed class can have a constructor, but only the classes listed in the permits clause can extend or instantiate the sealed class, and other classes are prevented from subclassing it.

```java
public sealed class Shape permits Circle, Square {  // permits clause included
    private final String color;

    // Constructor for the sealed class
    public Shape(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }
}

// Permitted subclass 1
public final class Circle extends Shape {
    public Circle(String color) {
        super(color);  // Calling the constructor of the sealed class
    }
}

// Permitted subclass 2
public final class Square extends Shape {
    public Square(String color) {
        super(color);  // Calling the constructor of the sealed class
    }
}

```

</details>

## Can you instantiate a sealed class directly in Java? If not, why?
<details>
<summary>Answer</summary>

- No, you cannot instantiate a sealed class directly in Java.

- You cannot instantiate a sealed class directly in Java because sealed classes are designed to have a closed inheritance hierarchy. 
- Only the classes or interfaces listed in the permits clause can extend or implement the sealed class. 
- Therefore, to create an instance, you must use one of the permitted subclasses.


```java
// Sealed class definition
public sealed class Shape permits Circle, Square {
    private final String color;

    public Shape(String color) {
        this.color = color;
    }

    public String getColor() {
        return color;
    }
}

// Permitted subclasses
public final class Circle extends Shape {
    public Circle(String color) {
        super(color);
    }
}

public final class Square extends Shape {
    public Square(String color) {
        super(color);
    }
}

```

- In the example above, the class Shape is a sealed class, and it permits Circle and Square as subclasses. You cannot instantiate Shape directly.

```java
// Invalid instantiation of the sealed class directly
Shape sh = new Shape("blue");  // Compilation error: Cannot instantiate the sealed class Shape directly

```

**Correct Usage:**
- Instead, you can instantiate one of the permitted subclasses:

```java
// Valid instantiation
Shape sh = new Circle("blue");  // This is allowed because Circle is a permitted subclass

```
</details>

##  What is the main advantage of using sealed classes in Java?
<details>
<summary>Answer</summary>

The main advantage of using sealed classes in Java is to control the inheritance hierarchy and restrict which classes can extend or implement a particular class or interface. This helps to:

- Enforce a closed set of subclasses: You can ensure that only a predefined set of classes are allowed to subclass the sealed class, making the code more predictable and easier to maintain.
- Improve type safety: By restricting inheritance, sealed classes can be used to create more controlled and safer class hierarchies.
- Exhaustive checks in switch statements: When used in switch expressions, the compiler can perform exhaustiveness checks, ensuring all subclasses are covered.

</details>

## Can you use a sealed class in a switch expression in Java?
<details>
<summary>Answer</summary>

- Yes, you can use a sealed class in a switch expression. 
- One of the key advantages of using sealed classes is that they work well with switch expressions because the compiler can check whether all permitted subclasses are handled. 
- If any subclass is missing in the switch expression, the compiler will throw an error, ensuring exhaustiveness.

Example 
```java
public sealed class Shape permits Circle, Square {}

public final class Circle extends Shape {}
public final class Square extends Shape {}

public class ShapePrinter {
    public static void printShape(Shape shape) {
        switch (shape) {
            case Circle c -> System.out.println("It's a Circle");
            case Square s -> System.out.println("It's a Square");
            // No default needed, compiler ensures all cases are handled
        }
    }
}

```

- In this example, you don’t need a default case in the switch, and the compiler will check that all permitted subclasses (Circle and Square) are handled.

</details>

## What is a Record in Java?
<details>
<summary>Answer</summary>

- A Record in Java is a special kind of class introduced in Java 14 as a preview feature and officially part of Java in Java 16. 
- Records are designed to be a concise way to create data-carrying classes. 
- They implicitly provide the following:
  - Final fields for each component.
  - A constructor to initialize those fields.
  - Getter methods for each component.
  - equals(), hashCode(), and toString() methods are automatically generated based on the record components.

syntax:

```java
public record Person(String name, int age) {}

```

- In the example above, Person is a record class that automatically creates a constructor, getters, equals(), hashCode(), and toString() methods.

</details>

## What is the purpose of the record keyword in Java?
<details>
<summary>Answer</summary>

- The record keyword in Java is used to define a data class that is immutable by default. 
- The main purpose of records is to simplify the creation of classes that are primarily used to store immutable data.
- When you define a class as a record, Java automatically generates essential methods like:
  - equals(): Compares instances based on their data.
  - hashCode(): Computes a hash code based on the data.
  - toString(): Provides a string representation of the record.
  - Getter methods for all fields (implicitly).

This reduces boilerplate code and improves readability.

</details>

## Can a record have methods other than the equals(), hashCode(), and toString() methods?
<details>
<summary>Answer</summary>

- Yes, a record can have additional methods beyond the automatically generated ones. 
- You can define your own methods in a record, including static methods and instance methods.

```java
public record Person(String name, int age) {

    // A custom method in the record
    public String greet() {
        return "Hello, my name is " + name + " and I am " + age + " years old.";
    }
}

```
- Here, the Person record has an additional method greet() that is not generated automatically but can be added to a record like any regular class.

</details>

## Can a Record extend another class?
<details>
<summary>Answer</summary>

- No, records cannot extend other classes. A record is implicitly final, which means it cannot be subclassed.

- However, records can implement interfaces. This allows them to be used in a polymorphic context, just like other classes.

```java
public interface Describable {
    String describe();
}

public record Person(String name, int age) implements Describable {
    public String describe() {
        return name + " is " + age + " years old.";
    }
}

```
</details>

## Can a Record have mutable fields?
<details>
<summary>Answer</summary>

- No, records in Java are immutable by default. 
- Once a record is created, its fields cannot be modified. 
- The fields of a record are implicitly final and cannot be changed after the object is created.

```java
public record Person(String name, int age) {}

```

- In the above example, both name and age are implicitly final. You cannot change the values of these fields after the object is created:

```java
Person person = new Person("Alice", 30);
person.name = "Bob"; // Compilation error: cannot assign a value to final variable 'name'

```
</details>

##  How are equals(), hashCode(), and toString() methods generated for records?
<details>
<summary>Answer</summary>

For records, Java automatically generates the following methods based on the components (fields) of the record:

- equals(): Compares the fields of the record for equality.
- hashCode(): Generates a hash code based on the fields of the record.
- toString(): Generates a string representation of the record that includes the record name and the values of its components.

```java
public record Person(String name, int age) {}

Person p1 = new Person("Alice", 30);
Person p2 = new Person("Alice", 30);
Person p3 = new Person("Bob", 25);

System.out.println(p1.equals(p2));  // true
System.out.println(p1.hashCode());  // hashCode value based on name and age
System.out.println(p1);             // Person[name=Alice, age=30]

```

- These methods are automatically generated based on the record's fields.

</details>

## Can a record be abstract?
<details>
<summary>Answer</summary>

- No, a record cannot be abstract. 
- A record is implicitly final because it is designed to be a simple data carrier class that does not allow subclassing.
- Records are meant to be immutable data classes, and making them abstract would conflict with this design. 
- You cannot subclass a record or define an abstract record.

</details>


## Can a record have constructors?
<details>
<summary>Answer</summary>
 
- Yes, a record can have custom constructors in addition to the automatically generated canonical constructor. 
- The **canonical constructor** is the one that is generated from the record's components, but you can define additional constructors if needed.

```java
public record Person(String name, int age) {

    // Custom constructor with additional logic
    public Person {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }

    // Another custom constructor
    public Person(String name) {
        this(name, 0);  // Default age to 0
    }
}

```

- In this example, the custom constructor adds validation to the age and provides an overload for cases where only the name is provided.

</details>

## Can a record be used with var in Java?
<details>
<summary>Answer</summary>

- Yes, you can use var with records in Java. 
- Since the record's type is inferred from its declaration, var can be used to hold a reference to a record instance, just like any other class.

```java
var person = new Person("Alice", 30);  // Using 'var' for a record instance
System.out.println(person);  // Person[name=Alice, age=30]

```

</details>


## What is a canonical constructor in Java records?
<details>
<summary>Answer</summary>

- The canonical constructor in a Java record is the automatically generated constructor that is created by the compiler based on the components (fields) declared in the record header. 
- This constructor allows you to initialize the record's fields and is the primary constructor used for creating record instances.

```java
public record Person(String name, int age) {}

```

In this example, Java automatically generates the following canonical constructor:

```java
public Person(String name, int age) {
    this.name = name;
    this.age = age;
}

```

- This constructor is automatically provided by the Java compiler, and it allows you to create instances of the Person record, like so:

```java
Person person = new Person("Alice", 30);

```

</details>

## Can you override the canonical constructor in a Java record?
<details>
<summary>Answer</summary>

- No, you cannot override the canonical constructor of a Java record. 
- The canonical constructor is automatically generated based on the components defined in the record's header, and it cannot be explicitly modified or overridden.
- However, you can define custom constructors to provide additional logic or validation. The custom constructor can be used to call the canonical constructor with specific values or to handle edge cases.


```java
public record Person(String name, int age) {

    // Custom constructor with validation logic
    public Person {
        if (age < 0) {
            throw new IllegalArgumentException("Age cannot be negative");
        }
    }
}

```

- In this example, the canonical constructor is implicitly present, and the custom constructor adds validation logic. The custom constructor calls the canonical constructor and adds extra checks.

</details>

##  Can you define multiple constructors in a Java record?
<details>
<summary>Answer</summary>

- Yes, you can define multiple constructors in a Java record.
- While the canonical constructor is automatically provided by the compiler, you can define additional constructors to provide more flexibility or add validation logic.

- However, these custom constructors cannot change the record's components (i.e., they must match the component types and names in the record header).

```java
public record Person(String name, int age) {

    // Custom constructor to set a default age if not provided
    public Person(String name) {
        this(name, 0);  // Default age to 0
    }
}

```

- In this case, the canonical constructor is still present, and an additional constructor is defined to handle cases where only the name is provided, defaulting the age to 0.

</details>

## What is the order of execution when a Java record has both a canonical constructor and custom constructors?
<details>
<summary>Answer</summary>

- When a custom constructor is defined in a Java record, the canonical constructor is still implicitly present. 
- The order of execution in such a scenario follows these steps:
  - Custom constructor logic runs first (if defined).
  - The canonical constructor is called next, either implicitly or explicitly, to initialize the fields of the record.

**Steps of Execution:**
- The custom constructor runs its logic, such as validation or other actions, before any field initialization.
- The canonical constructor is then invoked, which initializes the fields with the values passed to the constructor.

</details>






