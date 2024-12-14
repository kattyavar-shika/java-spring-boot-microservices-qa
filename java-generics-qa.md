# Java Generics Questions & Answer

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

## What are Generics in Java?
<details>
<summary>Answer</summary>

- Generics in Java allow you to write classes, interfaces, and methods that can operate on objects of various types while providing compile-time type safety. 
- Using Generics, you can write code that works with any data type but ensures that type-related errors are caught at compile time, rather than at runtime.

- Generics are introduced in Java 5 and allow you to define classes, interfaces, and methods with type parameters.

- Example 

```java
class Box<T> {
    private T value;
    public T getValue() {
        return value;
    }
    public void setValue(T value) {
        this.value = value;
    }
}

```

- Here, T is a placeholder for any type, and when creating a Box object, you specify the type.

</details>

## What are the advantages of using Generics?
<details>
<summary>Answer</summary>

-  Generics offer several advantages:
  -  **Type Safety:** With generics, you can enforce type checks at compile time, reducing the risk of ClassCastException at runtime.
  - **Code Reusability:** Generics allow you to write more generic, reusable code without worrying about specific data types.
  - **Elimination of Type Casting:** Since the type is known at compile time, explicit casting is not required when working with collections or other generic classes.
  - **Cleaner Code:** Generics provide a cleaner, more readable way to handle types in your code without repetitive or verbose type declarations.

</details>

## What is the difference between a raw type and a generic type?
<details>
<summary>Answer</summary>

- A raw type refers to a generic type that is used without specifying a type parameter. 
- It is backward-compatible with older versions of Java, where generics were not used. A generic type is one where you specify the type parameter.

- For example 
  - **Raw Type:** List list = new ArrayList();
  - **Generic Type:** `List<String> list = new ArrayList<>();`

- Using raw types results in loss of type safety, as the compiler does not check the types for you. Generics enforce compile-time checking to ensure correct types.

</details>

## What is the syntax to define a generic method in Java?
<details>
<summary>Answer</summary>

- The syntax for defining a generic method in Java involves specifying the type parameter before the return type of the method.

- Example

```java
public <T> void printArray(T[] array) {
    for (T element : array) {
        System.out.println(element);
    }
}

```

- Here, `<T> is the type parameter that allows the method to work with arrays of any type, whether it’s String[], Integer[], or any other object type.`

</details>

## What are bounded type parameters in Generics?
<details>
<summary>Answer</summary>

- Bounded type parameters allow you to restrict the types that can be used as arguments for a generic type. 
- You can specify an upper bound using the extends keyword to restrict the types to subclasses of a particular class or interface.

- For example, to restrict the generic type to only Number and its subclasses:

```java
public <T extends Number> void printNumber(T number) {
    System.out.println(number);
}

```

- In this case, the method accepts any type that is a subclass of Number, like Integer, Double, etc.

</details>

 
## What is the difference between `List<?> and List<Object>` in Generics? 
<details>
<summary>Answer</summary>

- `List<?> is an unbounded wildcard. It can represent a list of any type, but you cannot add any elements to it (except null). `
- It’s used when you need to work with any kind of list but don’t need to modify the list.

- Example 
```java
List<?> list = new ArrayList<String>();
// list.add("Hello"); // Compilation error, cannot add elements
// Required type:capture of ? Provided: String

```

- `List<Object>` is a list of Object type, meaning you can add any type of object to it.   
 However, it’s still specifically a `List<Object>` and doesn't provide the flexibility of being able to hold different types of objects.

- Example 

```java
List<Object> list = new ArrayList<>();
list.add("Hello");  // Works fine
list.add(100);      // Also works fine

```
</details>


## What are wildcards in Java Generics?
<details>
<summary>Answer</summary>

- Wildcards in Java Generics are used to represent an unknown type. There are three types of wildcards:
  - `Unbounded Wildcard (?)`: Represents an unknown type. Example:

    ```java
    public void printList(List<?> list) { ... }
    
    ```
    
  - This can accept a list of any type (like List<Integer>, List<String>, etc.), but you can't add elements (except null).
- `Upper Bounded Wildcard (? extends T):` Represents a type that is a subclass of a given class or implements an interface. Example:

    ```java
    public void printNumbers(List<? extends Number> list) { ... }
    
    ```
  - This accepts a list of any subclass of Number, such as `List<Integer> or List<Double>`.

- Lower Bounded Wildcard (? super T): Represents a type that is a superclass of a given class.

    ```java
    public void addNumbers(List<? super Integer> list) { ... }
    
    ```
  - This accepts a list of Integer or any of its superclasses, such as `List<Number> or List<Object>`.

</details>

## What is the use of generics in the Collections framework?
<details>
<summary>Answer</summary>

- Generics are extensively used in the Java Collections framework to provide type safety and eliminate the need for casting. 
- By using generics in collections like List, Set, and Map, the compiler can enforce that only the specified type of elements are added to the collection.

```java
List<String> list = new ArrayList<>();
list.add("Hello");
list.add("World");
// list.add(100); // Compilation error, because only String is allowed

```
- In contrast, without generics:

```java
List list = new ArrayList();
list.add("Hello");
list.add(100);  // Allowed, but you would need casting when retrieving items
String str = (String) list.get(0); // Type casting is required

```

</details>

##  Can you create a generic class that accepts both objects and primitive types?
<details>
<summary>Answer</summary>

- No, Java Generics cannot directly handle primitive types (like int, char, double, etc.) because generics work only with objects.
- However, Java automatically converts primitive types to their corresponding wrapper classes (autoboxing).

```java
class Box<T> {
    private T value;
    public T getValue() {
        return value;
    }
    public void setValue(T value) {
        this.value = value;
    }
}

Box<Integer> box = new Box<>(); // Using Integer for int
box.setValue(10); // Autoboxing happens

```
- Primitive types must be wrapped in their respective classes like Integer, Character, Double, etc., when used with generics.

</details>

## What is the Type Erasure in Java Generics?
<details>
<summary>Answer</summary>

- **Type erasure** is the process by which Java removes generic type information during compilation.  
   This means that the generic type is replaced with its raw type (like Object for non-bounded types) when the code is compiled into bytecode.

Example 
```java
public class Box<T> {
    private T value;
    public void setValue(T value) {
        this.value = value;
    }
    public T getValue() {
        return value;
    }
}

```
- At runtime, the Box class will be represented as Box<Object> or a similar raw type, depending on whether the type is bounded.
- Type erasure allows for backward compatibility with older versions of Java that didn’t support generics, but it also means that the type information is not available at runtime.

</details>












