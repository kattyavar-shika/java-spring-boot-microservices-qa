# Java String Questions & Answer

### Disclaimer

This content is created for educational purposes and aims to assist learners in preparing for Java, Spring Boot, and Microservices-related interviews.

- The questions and answers are intended to provide insight into common interview topics and are based on publicly available knowledge, research, and common practices within the industry.
- This content is not directly copied from any specific sources and is the result of personal understanding, research, and synthesis.
- If any external content, text, or ideas have been used, they have been cited and attributed appropriately (where applicable).

If you are the owner of any content referenced or used in this document and believe that proper attribution has not been provided, please contact the author so that the necessary changes can be made.

---

**Note**: By using this repository or document, you acknowledge that the information provided is for educational purposes only, and you are responsible for verifying the accuracy of the content before relying on it for professional purposes.


## What is the difference between String, StringBuilder, and StringBuffer in Java?
<details>
<summary>Answer</summary>

- **String**: Immutable, meaning its value cannot be changed once created. It is stored in the string pool.
- **StringBuilder**: Mutable and not synchronized, designed for single-threaded scenarios where you need to perform frequent string modifications.
- **StringBuffer**: Mutable and synchronized, designed for multi-threaded scenarios where string modifications occur.

</details>

## How does the `intern()` method work in Java?
<details>
<summary>Answer</summary>

The `intern()` method ensures that all equal string literals refer to the same object in memory. If a string is already in the string pool, the method returns the reference to that string, otherwise, it adds the string to the pool.

</details>

## Can you explain the immutability of the String class in Java?
<details>
<summary>Answer</summary>

The String class in Java is immutable, meaning once a String object is created, its value cannot be changed. Any modification to a string creates a new string object. This is achieved by making the fields `final` and `private`, and not providing methods that modify the string value.

</details>

## What is the significance of the `String` pool in Java?
<details>
<summary>Answer</summary>

The string pool (also known as the string literal pool) is a special memory region where Java stores unique string literals. When you create a string using a literal (e.g., `"Hello"`), it is checked in the pool. If it already exists, the existing reference is returned; otherwise, a new string object is created and added to the pool.

</details>

## How do you compare two strings in Java?
<details>
<summary>Answer</summary>

- Use `equals()` method for content comparison.
- Use `==` for reference comparison (checks if two references point to the same object).

</details>

## What will be the output of the following code?

```java
String str1 = "Java";
String str2 = "Java";
System.out.println(str1 == str2);
```

<details>
<summary>Answer</summary>
- true
Since both str1 and str2 point to the same string in the string pool.


</details>

## What is the purpose of String.format() method in Java?
<details>
<summary> Answer</summary>

- String.format() is used to create formatted strings, similar to the printf function. 
- It allows you to insert values into a string with placeholders, making the string creation more flexible and readable.

</details>

## What is the result of calling the toUpperCase() method on a String?
<details>
<summary> Answer</summary>

- toUpperCase() returns a new string where all the characters are converted to uppercase. The original string remains unchanged because Strings are immutable.

</details>

## What is the time complexity of String concatenation using + operator and StringBuilder?
<details>
<summary> Answer</summary>

- Using + for string concatenation: O(n^2) because a new String object is created every time you concatenate.
- Using StringBuilder: O(n) because StringBuilder appends to the existing buffer without creating new objects for each operation.

</details>

## How can you reverse a string in Java?

<details>
<summary> Answer</summary>

```java 
String str = "Hello";
String reversed = new StringBuilder(str).reverse().toString();
System.out.println(reversed);  // Output: "olleH"
```
</details>

## What happens when you compare a string with null using the equals() method?
<details>
<summary> Answer</summary>

- Calling equals() on a null value will throw a NullPointerException. Always ensure that the string you are calling equals() on is not null or use Objects.equals() which safely handles null.

</details>

## What is the use of the matches() method in Java String?
<details>
<summary> Answer</summary>

- The matches() method checks if the string matches the given regular expression. It returns true if the string matches the pattern and false otherwise.

```java 
String str = "hello123";
System.out.println(str.matches("\\w+"));  // Output: true

```
</details>

## How do you convert a String to an integer in Java?
<details>
<summary> Answer</summary>

```java 
String str = "123";
int num = Integer.parseInt(str);
```

- Alternatively, Integer.valueOf(str) can be used if you need the result as an Integer object.
</details>

## What is the difference between substring(int start) and substring(int start, int end)?
<details>
<summary> Answer</summary>

- substring(int start): Returns a new string starting from the start index to the end of the string.
- substring(int start, int end): Returns a new string from start index to end - 1 index (exclusive of the end index).

</details>

## How do you check if a string is empty or null in Java?
<details>
<summary> Answer</summary>

```java 
String str = "";
if (str == null || str.isEmpty()) {
    System.out.println("String is null or empty");
}
```
</details>

## What is the use of String.join() method in Java? 
<details>
<summary> Answer</summary>

- String.join() is used to join elements of a collection (like a list or array) into a single string with a specified delimiter.

```java 
String result = String.join(",", "apple", "banana", "cherry");
System.out.println(result);  // Output: "apple,banana,cherry"
```
</details>

## Can you explain the concept of "String immutability" with an example?
<details>
<summary> Answer</summary>

- Strings in Java are immutable. Once a String object is created, its value cannot be changed.
-  Example
```java 
String s1 = "Java";
s1 = s1.concat(" Programming");
System.out.println(s1);  // Output: "Java Programming"
// The original string "Java" is not changed, a new String object is created.

```

</details>

## What is the difference between StringBuilder and StringBuffer in Java?
<details>
<summary> Answer</summary>

- **StringBuilder:** Faster as it is not synchronized, used in single-threaded environments.
- **StringBuffer:** Slower due to synchronization, used in multi-threaded environments.

</details>




## ref

## 
<details>
<summary> Answer</summary>

- 

</details>