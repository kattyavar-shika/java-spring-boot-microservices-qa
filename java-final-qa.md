# Java final Questions & Answer

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

## What is the final keyword in Java?
<details>
<summary>Answer</summary>

- The final keyword in Java is used to define constants, prevent method overriding, and prevent inheritance. 
- It can be applied to variables, methods, and classes.
  - **Final Variable:** Once a variable is declared as final, its value cannot be changed after initialization.
  - **Final Method:** A final method cannot be overridden by subclasses.
  - **Final Class:** A final class cannot be subclassed or extended.

</details>

## What happens if we declare a method as final in Java?
<details>
<summary>Answer</summary>

- If a method is declared as final, it cannot be overridden by any subclass. This is useful when we want to ensure that a specific method's behavior is not modified by subclassing.

- Example

```java
class Parent {
    final void show() {
        System.out.println("This is a final method");
    }
}

class Child extends Parent {
    // This will cause a compile-time error
    // void show() {
    //     System.out.println("Trying to override final method");
    // }
}

```

</details>

## What happens if we declare a class as final in Java?
<details>
<summary>Answer</summary>

- A final class cannot be subclassed or extended. This means you cannot create any subclasses from a final class. It is useful when we want to prevent inheritance for security or design reasons.

- Example 

```java
final class MyClass {
    void display() {
        System.out.println("This is a final class.");
    }
}

// This will cause a compile-time error
// class Child extends MyClass {
// }

```
</details>

## Can a final variable be modified in Java?
<details>
<summary>Answer</summary>

- No, once a variable is declared as final, its value cannot be changed after initialization. 
- However, if the final variable is a reference type (e.g., an object), the reference itself cannot be changed, but the object it points to can still be modified.

- Example 

```java
final int x = 10;
// x = 20; // This will cause a compile-time error

final List<String> list = new ArrayList<>();
list.add("Hello"); // This is allowed as the object can still be modified.

```

</details>

##  What is the difference between final, finally, and finalize in Java?
<details>
<summary>Answer</summary>

- final: Used to declare constants, prevent method overriding, and prevent inheritance.
- finally: Used in exception handling. The finally block is always executed after the try block, regardless of whether an exception is thrown or not.
- finalize: A method in the Object class that is called by the garbage collector before an object is destroyed. It is used to perform cleanup tasks.

</details>

## Can a constructor be declared as final in Java?
<details>
<summary>Answer</summary>

- No, constructors cannot be declared as final in Java. 
- The purpose of a constructor is to initialize objects, and it is not subject to inheritance or overriding, so declaring it as final does not serve any purpose.

- Example
```java
// This will cause a compile-time error
// final MyClass() {
//     System.out.println("This is a final constructor");
// }

```

</details>

## What is the use of final with local variables?
<details>
<summary>Answer</summary>

- When a local variable is declared as final, its value cannot be changed once it has been assigned. 
- This is typically used to create constants within methods or to ensure that a variable is not modified after its initial assignment.

- Example 

```java
void method() {
    final int x = 5;
    // x = 10; // This will cause a compile-time error
}

```
</details>

## Can final be used with lambda expressions in Java?
<details>
<summary>Answer</summary>

-  Yes, in Java, local variables used inside a lambda expression must be effectively final, meaning their values cannot change after they are initialized. 
- The variable doesn’t need to be explicitly declared as final, but it must be treated as though it were.

- Example
```java

void method() {
    int x = 10; // Effectively final
    Runnable r = () -> {
        System.out.println(x);  // This is allowed
    };
    x = 20; // Error: variable x might be modified, so it's not effectively final
}


```

</details>

## What is the benefit of using the final keyword for method parameters?
<details>
<summary>Answer</summary>

- Declaring method parameters as final ensures that the parameter value cannot be modified inside the method body. 
- This improves readability and makes it clear that the method will not alter the parameter values.

- Example 

```java
void method(final int x) {
    // x = 10; // This will cause a compile-time error
    System.out.println(x);
}

```

</details>

## Is it possible to use final with abstract methods in Java?
<details>
<summary>Answer</summary>

- No, it is not possible to use the final keyword with abstract methods. 
- Abstract methods are meant to be overridden in subclasses, while final methods cannot be overridden. 
- Therefore, the two concepts are mutually exclusive.

- Example 

```java
// This will cause a compile-time error
// abstract final void display();

```

</details>

## You have the following base and derived classes in Java. The method in the base class takes a final parameter. In the derived class, if the final keyword is removed from the parameter in the overridden method, what will happen?

```java
class Base {
    public void greet(final String name) {
        System.out.println("Hello, " + name);
        // name = "New Value"; // This would cause a compile-time error
    }
}

class Derived extends Base {
    @Override
    public void greet(String name) {  // No 'final' keyword here
        name = "New Value";  // This is now allowed
        System.out.println("Hello, " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        Base base = new Base();
        base.greet("John");

        Derived derived = new Derived();
        derived.greet("Jane");
    }
}

```
<details>
<summary>Answer</summary>

- What happens when final is removed:
  - If the final keyword is removed from the method parameter in the derived class, the code will still compile and run, but now the method in the derived class can modify the value of the parameter. This is because final only prevents reassignment of the parameter in the method body within the class where it is declared.
- final keyword in base class:
  - The final keyword in the base class means that the parameter value cannot be modified inside the method body of that method. However, this is a constraint only within the body of the method.
- Good Practice:
  - While it's technically allowed to remove final in the derived class, it may not be considered good practice to do so. This is because the use of final in the base class likely indicates an intention to ensure that the parameter remains immutable. Removing final could potentially violate that intention.



</details>