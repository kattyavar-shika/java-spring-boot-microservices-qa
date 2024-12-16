# Java common Questions & Answer

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

# Covered topic

## Upcasting and Down casting.
## Wrapper Classes
## Enum Classes
## Annotations
## Java ref types.

===============================================================


## What is upcasting in Java? Can you provide an example?
<details>
<summary>Answer</summary>

- Upcasting is the process of casting a subclass object to a superclass reference.
- This is safe and does not require explicit casting, as every subclass object is also an instance of its superclass.
- Upcasting is implicitly done by the compiler.

Example

```java
class Animal {
  void speak() {
    System.out.println("Animal speaks");
  }
}

class Dog extends Animal {
  void speak() {
    System.out.println("Dog barks");
  }
}

public class Main {
  public static void main(String[] args) {
    Animal myAnimal = new Dog(); // Upcasting
    myAnimal.speak(); // Outputs "Dog barks"
  }
}

```

</details>

## What is downcasting in Java? How is it different from upcasting?

<details>
<summary>Answer</summary>

- Downcasting is the process of casting a superclass reference back to a subclass type.
- Unlike upcasting, downcasting can be unsafe, as it may lead to a ClassCastException if the object is not actually an
  instance of the subclass.
- Downcasting requires explicit casting.

```java
Animal myAnimal = new Dog();
Dog myDog = (Dog) myAnimal; // Downcasting
myDog.

speak(); // Outputs "Dog barks"

```

- If the object is not actually of the subclass type, the following would throw a ClassCastException:

```java
Animal myAnimal = new Animal();
Dog myDog = (Dog) myAnimal; // Throws ClassCastException

```

</details>

## What is the difference between instanceof and downcasting?
<details>
<summary>Answer</summary>

- The instanceof operator checks whether an object is an instance of a specific class or any of its subclasses. 
- It does not change the type of the object; it only performs a type check. Downcasting, on the other hand, actually changes the reference type of an object.


```java
if (animal instanceof Dog) { // instanceof checks the type
    Dog dog = (Dog) animal;  // downcasting to Dog
    dog.bark();
}

```
- instanceof is a safety mechanism to ensure that downcasting does not result in a ClassCastException.

</details>

## What is the difference between Integer.parseInt() and Integer.valueOf()?
<details>
<summary>Answer</summary>

- Integer.parseInt() is used to convert a string to a primitive int, while Integer.valueOf() returns an Integer object (the wrapper class for int).

```java
String str = "123";
int num1 = Integer.parseInt(str); // Converts to primitive int
Integer num2 = Integer.valueOf(str); // Converts to Integer object

```

</details>

## What are wrapper classes in Java, and why do we use them?

<details>
<summary>Answer</summary>

- Wrapper classes in Java are the object representations of the primitive data types (e.g., int, char, double).
- Each primitive type has a corresponding wrapper class,
- such as:
    - int → Integer
    - char → Character
    - double → Double

Wrapper classes are used for:

- `Storing primitive values in collections (e.g., ArrayList<Integer>)`
- Autoboxing and unboxing (automatic conversion between primitive types and their wrapper objects)
- Providing utility methods (e.g., parsing strings into numbers, checking whether a value is a valid number)

```java
int num = 10;
Integer wrapper = Integer.valueOf(num); // Boxing
int unboxed = wrapper.intValue(); // Unboxing

```
</details>

## Can you explain autoboxing and unboxing in Java?
<details>
<summary>Answer</summary>

- Autoboxing is the automatic conversion of a primitive type into its corresponding wrapper class, and unboxing is the reverse operation. 
- This happens implicitly in Java, and you don't need to manually convert between primitives and wrapper classes.

```java
Integer num = 10; // Autoboxing from int to Integer
int result = num; // Unboxing from Integer to int

```
- This automatic conversion makes working with collections (which only accept objects) and primitives easier.

</details>

## What are enum classes in Java, and how do they work?
<details>
<summary>Answer</summary>

- Enum classes in Java represent a set of named constants. 
- Enums are more powerful than simple public static final constants because they are full-fledged classes and can have fields, methods, and constructors.

Example 
```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
}

```
- Enums are type-safe, meaning that only the defined constants can be used, and they can be iterated over, compared, and used in switch statements.

</details>

##  How can you add behavior to an enum in Java?
<details>
<summary>Answer</summary>

- You can add fields, constructors, and methods to an enum to give it more functionality. 
- Each enum constant can have its own implementation for a method as well.

Example 

```java
public enum Day {
    MONDAY("Start of the week"),
    FRIDAY("End of the workweek");

    private String description;

    Day(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }
}

```
- In this example, each enum constant has a description, and you can call the getDescription() method to retrieve it.

</details>

## Can you modify the order of enum constants in Java?
<details>
<summary>Answer</summary>

- No, the order of enum constants cannot be changed once the enum is defined. 
- The order in which enum constants are declared is the order in which they are processed in methods like values(), ordinal(), etc. 
- Modifying the order could change the behavior of code that depends on the enum's order.

```java
public enum Direction {
    NORTH, EAST, SOUTH, WEST;
}

```
- In this case, the ordinal values will be assigned automatically (NORTH=0, EAST=1, SOUTH=2, WEST=3) and cannot be re-ordered dynamically.

</details>

## Can you associate methods with enum constants in Java?
<details>
<summary>Answer</summary>

- Yes, you can associate methods with enum constants. 
- Enums in Java can have methods and fields, allowing you to add behavior to each enum constant.

```java
public enum Day {
    MONDAY("Start of the week") {
        @Override
        public String activity() {
            return "Go to work";
        }
    },
    FRIDAY("Almost weekend") {
        @Override
        public String activity() {
            return "Relax after work";
        }
    };

    private String description;

    Day(String description) {
        this.description = description;
    }

    public String getDescription() {
        return description;
    }

    public abstract String activity();  // Abstract method to be implemented by each constant
}

```

- In this example, each Day constant has a custom activity() method that provides a specific action for that day.

</details>


## How do you iterate through an enum in Java?
<details>
<summary>Answer</summary>

- You can iterate over the constants of an enum using the values() method, which returns an array of all the enum constants.

```java
for (Day day : Day.values()) {
    System.out.println(day + ": " + day.getDescription());
}

```


</details>

## What are annotations in Java, and how are they used?
<details>
<summary>Answer</summary>

- Annotations in Java are a form of metadata that provide information about the code but are not directly part of the program logic. 
- They are used for various purposes, such as configuration, code generation, or runtime processing.

Common uses include:
- Providing hints to the compiler (@Override, @Deprecated)
- Defining runtime behavior (@Entity, @Transaction)
- Framework configurations (@Autowired in Spring)

```java
public class MyClass {
    @Override
    public String toString() {
        return "MyClass Object";
    }
}

```
</details>

## `What is the difference between @Retention(RetentionPolicy.RUNTIME) and @Retention(RetentionPolicy.CLASS)?`
<details>
<summary>Answer</summary>

- The @Retention annotation specifies how long the annotation information should be retained.
  - RetentionPolicy.RUNTIME: The annotation is available at runtime and can be accessed through reflection.
  - RetentionPolicy.CLASS: The annotation is available at compile-time and in the class file but not at runtime.

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface MyAnnotation { }

```

</details>

## Can you explain the difference between @Target and @Retention annotations?
<details>
<summary>Answer</summary>
 
- @Target specifies where the annotation can be applied (e.g., methods, fields, classes).
- @Retention specifies at what point in the Java lifecycle the annotation information is available (e.g., compile-time, runtime).

Example : 

```java
@Target(ElementType.METHOD)  // This annotation can only be applied to methods
@Retention(RetentionPolicy.RUNTIME)  // The annotation is available at runtime
public @interface MyCustomAnnotation {}

```
</details>


## What is a strong reference in Java?
<details>
<summary>Answer</summary>

- A strong reference is the default type of reference in Java. 
- When an object is referenced by a strong reference, it is considered "alive" and will not be garbage collected. 
- As long as there is a strong reference to an object, the object will not be reclaimed by the garbage collector, regardless of how much memory is available. 
- Strong references are the most common and default type of reference used in Java.

```java
Object obj = new Object(); // strong reference

```

- In the example above, obj is a strong reference to the Object instance. As long as obj points to the object, it cannot be garbage collected.

</details>


## What is a weak reference in Java?
<details>
<summary>Answer</summary>

- A weak reference is a type of reference in Java that allows an object to be collected by the garbage collector if no strong references to it exist. 
- When the garbage collector runs, objects with only weak references are eligible for garbage collection, even if they are still referenced weakly.
- Weak references are typically used for memory-sensitive caches or similar scenarios where you don't want an object to remain in memory if no strong references exist.
 
```java
WeakReference<Object> weakRef = new WeakReference<>(new Object());

```
- In this example, weakRef holds a weak reference to the object. If the object is no longer strongly reachable, it becomes eligible for garbage collection.

</details>


## What is a soft reference in Java?
<details>
<summary>Answer</summary>

- A soft reference is similar to a weak reference, but it has a slightly different behavior in terms of garbage collection. 
- Objects referenced by soft references are collected only when the JVM is low on memory. 
- This makes soft references suitable for implementing memory-sensitive caches, where objects should remain in memory as long as the system has available resources.

- The garbage collector will only reclaim an object with a soft reference if the JVM needs memory, but until that time, the object will not be garbage collected.

```java
SoftReference<Object> softRef = new SoftReference<>(new Object());

```

- In the above code, the object referenced by softRef will stay in memory until the JVM decides to free up memory.

</details>


## What is a phantom reference in Java?
<details>
<summary>Answer</summary>

- A phantom reference is the weakest type of reference in Java. 
- An object referenced by a phantom reference will be garbage collected when it is no longer reachable by any strong or weak references, but unlike weak and soft references, the object is not available directly through the phantom reference. 
- Instead, phantom references are used to track when an object is about to be collected by the garbage collector, typically for cleanup tasks like deallocating native memory.

- To use phantom references, you need to associate the reference with a ReferenceQueue. Once the object is about to be collected, the phantom reference will be added to the queue.

```java
PhantomReference<Object> phantomRef = new PhantomReference<>(new Object(), new ReferenceQueue<>());

```

- In this example, the object referenced by phantomRef will be garbage collected as soon as there are no more strong or weak references, and it will be added to the ReferenceQueue after the object is finalized.

</details>

##  What is the difference between weak references and soft references?
<details>
<summary>Answer</summary>

Both weak references and soft references allow objects to be garbage collected under specific circumstances, but the difference lies in when the garbage collector reclaims the object:

- Weak References: The object is eligible for garbage collection as soon as it is no longer strongly reachable. The garbage collector can collect weakly referenced objects even when memory is not constrained.
- Soft References: The object is eligible for garbage collection only when the JVM runs low on memory. The garbage collector will keep soft-referenced objects in memory longer than weakly-referenced ones, only collecting them when necessary.

**Use Case Difference:**
- Weak references are often used for caches or mappings where the object can be discarded as soon as it is no longer needed.
- Soft references are commonly used for memory-sensitive caches where you want the object to be kept as long as possible until memory is needed.

</details>


## Can you explain the impact of weak, soft, and phantom references on garbage collection?
<details>
<summary>Answer</summary>

The impact of weak, soft, and phantom references on garbage collection varies based on their characteristics:

-  Weak References: Objects with weak references are eligible for garbage collection immediately once there are no strong references to them. This means the garbage collector does not wait for low memory conditions and will collect them as soon as possible.
- Soft References: Objects with soft references are collected only when the JVM is low on memory. Until memory pressure arises, the garbage collector will leave them in memory, which can be useful for caching scenarios where you want to retain objects as long as there is enough heap space.
- Phantom References: Phantom references are the most specialized type and are used for performing cleanup tasks after an object has been finalized and is about to be collected. Phantom references do not provide direct access to the object, but instead, they are placed in a ReferenceQueue when the object is about to be reclaimed.

- Each reference type allows for different levels of control over when and how objects are garbage collected, and the choice of reference depends on the application’s memory management needs.

</details>





