# Java Lambda Questions & Answer

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

## What is a Lambda Expression in Java?
<details>
<summary>Answer</summary>

- A lambda expression in Java is a short block of code that takes in parameters and returns a value. 
- It can be used primarily to define the behavior of a method in functional programming style. 
- Lambda expressions were introduced in Java 8 to provide a clear and concise way to represent an instance of a functional interface.

- syntax:

```java
(parameters) -> expression

//Example 
(a, b) -> a + b

```

</details>

## Why were Lambda Expressions introduced in Java? Can you explain some of the benefits of using Lambdas?
<details>
<summary>Answer</summary>

- Lambda expressions were introduced in Java 8 primarily to bring functional programming capabilities to Java and to address certain limitations with the traditional approach of using anonymous inner classes. Here are some key reasons why lambda expressions were introduced:
  - Concise Code:
    - Before Java 8, many simple operations (like passing behavior to methods) required verbose anonymous class declarations. Lambda expressions allow us to express these operations in a much shorter and more readable form.
    - Example : Before Lambda (Anonymous Class):
```java
List<String> names = Arrays.asList("John", "Jane", "Doe");
Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String s1, String s2) {
        return s1.compareTo(s2);
    }
});

```
After lambda Expression: 
```java
List<String> names = Arrays.asList("John", "Jane", "Doe");
names.sort((s1, s2) -> s1.compareTo(s2));

```

- Readability and Maintainability:
  - Lambda expressions help reduce boilerplate code and make the code more readable, especially in places where short pieces of code are being passed around (like callbacks or event handlers).
- Functional Programming Support:
  - Java was traditionally an imperative programming language, but with the introduction of lambdas, Java can now adopt a more functional programming style. Lambdas make it easier to write higher-order functions and leverage operations like filtering, mapping, and reducing directly on collections, especially through the Stream API.
- Parallelization
  - Lambdas play a crucial role in parallel processing. Java 8 introduced the Stream API, which works seamlessly with lambdas to allow developers to process collections in parallel without the need to explicitly handle threads.
  - Example

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .map(n -> n * n)     // square the numbers
       .filter(n -> n > 10) // filter squares greater than 10
       .forEach(System.out::println);

```


</details>

## What is a Functional Interface in Java?
<details> 
<summary>Answer</summary>

- A Functional Interface is an interface that has exactly one abstract method. It may have multiple default or static methods, but only one abstract method. Lambda expressions can be used to provide the implementation of this single abstract method.

- Example
```java
@FunctionalInterface
public interface MyFunction {
    int add(int a, int b);  // single abstract method
}

```
</details>

## What is the use of @FunctionalInterface annotation?
<details>
<summary>Answer</summary>

- The @FunctionalInterface annotation is used to indicate that an interface is intended to be a functional interface.
- This annotation is not required, but it provides compile-time checking to ensure the interface has exactly one abstract method. 
- If the interface has more than one abstract method, a compilation error will occur.

- Example
```java
@FunctionalInterface
public interface MyFunction {
    void run();  // single abstract method
}

```
</details>

## What are the advantages of using Lambda Expressions?
<details>
<summary>Answer</summary>

- **Conciseness:** Lambda expressions allow for more compact and readable code.
- **Less Boilerplate Code:** They remove the need for anonymous class implementations.
- **Enhanced Readability:** With the functional programming style, it becomes easier to understand and maintain code.
- **Encourages Functional Programming:** It promotes the use of higher-order functions and makes the code more declarative.

</details>

## What is the difference between an Anonymous Inner Class and a Lambda Expression?
<details>
<summary>Answer</summary>

- Both anonymous inner classes and lambda expressions allow you to define a class on the fly, but they differ in syntax, readability, and usage:
  - **Anonymous Inner Class:** More verbose and requires the declaration of a class with the method implementation.
  - **Lambda Expression:** Shorter and more readable as it allows you to pass behavior as arguments without needing to define a full class.

- Anonymous Inner Class:

```java
MyFunction myFunc = new MyFunction() {
    public int add(int a, int b) {
        return a + b;
    }
};

```
- Lambda Expression:

```java
MyFunction myFunc = (a, b) -> a + b;

```
</details>

## Explain the syntax of a Lambda Expression.
<details>
<summary>Answer</summary>

- A Lambda Expression has the following general syntax:

```java
(parameters) -> expression

```
- Where
  - Parameters: Represents the parameters passed to the method (can be empty).
  - Arrow (->): Separates the parameters from the body of the lambda expression.
  - Expression or Block: Represents the actual implementation of the method, which can be a single expression or a block of code.

Example 
```java
(int a, int b) -> a + b

```
</details>


## What is the difference between Function<T, R> and Consumer<T>?
<details>
<summary>Answer</summary>

- Function<T, R>: Takes an argument of type T and returns a result of type R. It is used when you want to apply a function to an input and get an output.
```java
Function<Integer, Integer> square = x -> x * x;

```

-  Consumer<T>: Takes an argument of type T and returns no result (void). It is typically used when you want to perform an operation that consumes the input but doesn't produce a result.

```java
Consumer<String> print = str -> System.out.println(str);

```
</details>

## What are Predicate<T> and its typical use cases?

<details>
<summary>Answer</summary>

- A Predicate<T> is a functional interface that represents a condition or boolean function. It accepts one argument of type T and returns a boolean value (true or false). 
- It is commonly used in filtering operations, such as in stream filtering.

```java

Predicate<Integer> isEven = num -> num % 2 == 0;

//Usage 
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream().filter(isEven).collect(Collectors.toList());

```
</details>

## What is a method reference in Java and how is it different from a Lambda expression?
<details>
<summary>Answer</summary>

- A method reference is a shorthand syntax in Java for calling a method directly. 
- It is a more concise and readable alternative to lambda expressions when you just want to call an existing method.

```java
//Syntax 
ClassName::methodName

//Usage 
// Lambda expression
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.forEach(name -> System.out.println(name));

// Method reference
  names.forEach(System.out::println);

```

</details>

## Can you use Lambda expressions with Collections in Java?
<details>
<summary>Answer</summary>

- Yes, lambda expressions can be used with Java Collections, particularly with the Stream API introduced in Java 8. They provide a functional way to process collections.

```java
List<String> names = Arrays.asList("John", "Jane", "Joe");
names.stream()
     .filter(name -> name.startsWith("J"))
     .forEach(System.out::println);

```
</details>

## What is the Stream API and how does it relate to Lambda Expressions?
<details>
<summary>Answer</summary>

- The Stream API is a new abstraction in Java 8 that allows for functional-style operations on sequences of elements (such as collections). Lambda expressions are heavily used in the Stream API to define operations like filtering, mapping, and reducing.
- Example of using Stream and lambda:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
numbers.stream()
       .map(x -> x * x)    // square each number
       .forEach(System.out::println);

```

</details>


## What is the significance of the default and static methods in functional interfaces?
<details>
<summary>Answer</summary>

- default methods: These are methods with an implementation inside a functional interface. They provide a default behavior that can be overridden by implementing classes or lambdas if needed.
- static methods: These are methods that belong to the interface itself and are not associated with any instance.

```java
@FunctionalInterface
public interface MyInterface {
    void abstractMethod();  // abstract method

    default void defaultMethod() {
        System.out.println("This is a default method.");
    }

    static void staticMethod() {
        System.out.println("This is a static method.");
    }
}

```

</details>

## Can Lambda Expressions access local variables?
<details>
<summary>Answer</summary>

- Yes, lambda expressions can access local variables, but only if they are **final or effectively final**. 
- This ensures that the local variables are not modified after being captured by the lambda expression.

```java
public void testLambda() {
    int temp = 5; // effectively final
    final int num = 10;
    MyFunction func = (a, b) -> a + b + num + temp;  // num must be final or effectively final
}

```
</details>

## How does the this keyword work inside a Lambda Expression in Java?
<details>
<summary>Answer</summary>

- In Java, the behavior of the this keyword inside a lambda expression is different from its behavior inside regular methods or constructors.
- In Lambda Expressions:
  - The this keyword in a lambda expression refers to the instance of the enclosing class, not the lambda expression itself.
  - This is because a lambda expression does not create its own instance. Instead, it is treated as an implementation of a functional interface, and thus, it uses the enclosing class’s instance for context.
- In Regular Methods/Constructors
  - The this keyword refers to the current instance of the class in which the method or constructor is defined.


```java
class Outer {
    private String name = "Outer class";

    public void testLambda() {
        // Lambda Expression
        MyFunction myFunc = () -> {
            System.out.println("Inside lambda, this refers to: " + this.name); // 'this' refers to Outer instance
        };
        myFunc.execute();
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        outer.testLambda();
    }
}

@FunctionalInterface
interface MyFunction {
    void execute();
}

```

- Explanation: 
  -  In the above example, the this inside the lambda expression refers to the instance of the Outer class, because the lambda is defined within the method of the Outer class.

- **Key Points to Remember:**
  - Lambda Expressions do not have their own this reference. The this keyword inside a lambda refers to the instance of the enclosing class where the lambda expression is defined.
  - In an inner class (anonymous class), this refers to the instance of the inner class. However, in a lambda expression, this still refers to the instance of the enclosing class.
  - this in static methods: If you define a lambda inside a static method, this is not available because static methods do not belong to an instance, and thus, there is no instance to refer to with this.

```java
class Outer {
    public static void testStaticLambda() {
        MyFunction lambda = () -> {
            // System.out.println(this); // Error: 'this' cannot be referenced from a static context
        };
        lambda.execute();
    }

    public static void main(String[] args) {
        Outer.testStaticLambda();
    }
}

@FunctionalInterface
interface MyFunction {
    void execute();
}

```

In this case, trying to use this inside a static context will lead to a compilation error, as this cannot be referenced from a static method, where no instance exists.

</details>
