# Java String Q & A

# Java String Interview Questions

## 1. What is the difference between String, StringBuilder, and StringBuffer in Java?
<details>
<summary>Answer</summary>

- **String**: Immutable, meaning its value cannot be changed once created. It is stored in the string pool.
- **StringBuilder**: Mutable and not synchronized, designed for single-threaded scenarios where you need to perform frequent string modifications.
- **StringBuffer**: Mutable and synchronized, designed for multi-threaded scenarios where string modifications occur.

</details>

## 2. How does the `intern()` method work in Java?
<details>
<summary>Answer</summary>

The `intern()` method ensures that all equal string literals refer to the same object in memory. If a string is already in the string pool, the method returns the reference to that string, otherwise, it adds the string to the pool.

</details>

## 3. Can you explain the immutability of the String class in Java?
<details>
<summary>Answer</summary>

The String class in Java is immutable, meaning once a String object is created, its value cannot be changed. Any modification to a string creates a new string object. This is achieved by making the fields `final` and `private`, and not providing methods that modify the string value.

</details>

## 4. What is the significance of the `String` pool in Java?
<details>
<summary>Answer</summary>

The string pool (also known as the string literal pool) is a special memory region where Java stores unique string literals. When you create a string using a literal (e.g., `"Hello"`), it is checked in the pool. If it already exists, the existing reference is returned; otherwise, a new string object is created and added to the pool.

</details>

## 5. How do you compare two strings in Java?
<details>
<summary>Answer</summary>

- Use `equals()` method for content comparison.
- Use `==` for reference comparison (checks if two references point to the same object).

</details>

## 6. What will be the output of the following code?

```java
String str1 = "Java";
String str2 = "Java";
System.out.println(str1 == str2);
