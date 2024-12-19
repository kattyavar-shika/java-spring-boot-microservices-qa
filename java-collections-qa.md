# Java Collections Questions & Answer

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

# Overview 

## Java Collections Overview: Implementation Comparison

Note: Under review. 

| **Aspect**                | **ArrayList**  | **LinkedList**  | **Vector**  | **Stack**  | **CopyOnWriteArrayList**  | **HashSet**  | **LinkedHashSet**  | **TreeSet**  | **CopyOnWriteArraySet**  | **EnumSet**  | **HashMap**  | **LinkedHashMap**  | **TreeMap**  | **EnumMap**  | **ConcurrentHashMap**  | **IdentityHashMap**  | **ConcurrentLinkedQueue**  | **ArrayDeque**  | **PriorityQueue**  | **ConcurrentLinkedDeque**  |
|---------------------------|----------------|-----------------|-------------|------------|--------------------------|--------------|---------------------|--------------|--------------------------|--------------|--------------|---------------------|--------------|-------------|-------------------------|-----------------------|----------------------------|-----------------|--------------------|---------------------------|
| **Collection Type**        | List           | List            | List        | List       | List                     | Set          | Set                 | Set          | Set                      | Set          | Map          | Map                 | Map          | Map         | Map                     | Map                   | Queue                      | Deque            | Queue              | Deque                      |
| **Allows Duplicates**      | Yes            | Yes             | Yes         | Yes        | Yes                      | No           | No                  | No           | No                       | No           | No           | No                  | No           | No          | No                      | No                    | Yes                        | Yes              | Yes                | Yes                       |
| **Order**                  | Insertion order | Insertion order | Insertion order | Insertion order | Insertion order         | No order     | Insertion order      | Sorted order | Insertion order         | No order     | Insertion order | Insertion order     | Sorted order | Insertion order | No order                | No order              | FIFO (First-In-First-Out)  | Insertion order  | Priority order      | Insertion order            |
| **Null Elements**          | Yes            | Yes             | Yes         | Yes        | Yes                      | Yes          | Yes                 | No           | Yes                      | No           | Yes          | Yes                 | No           | Yes         | Yes                     | Yes                   | Yes                        | Yes              | Yes                | Yes                       |
| **Thread-Safety**          | No             | No              | Yes         | Yes        | Yes                      | No           | No                  | No           | Yes                      | No           | No           | No                  | No           | No          | Yes                     | No                    | Yes                        | No               | No                 | Yes                       |
| **Performance**            | `O(1)` access (for get/set), `O(n)` for insertions/removals in middle | `O(1)` for add/remove at ends, `O(n)` for access by index | `O(1)` for access, `O(n)` for insertions/removals in middle | `O(1)` for access, `O(n)` for insertions/removals in middle | `O(1)` for access, slower for writes (due to copying) | `O(1)` average for add/remove/contains | `O(1)` average for add/remove/contains | `O(log n)` for add/remove/contains | `O(1)` for add/remove/contains | `O(1)` average for add/remove/contains | `O(1)` average for add/remove/contains | `O(log n)` for add/remove/contains | `O(1)` for add/remove/contains | `O(1)` average for put/get/remove | `O(1)` for add/remove | `O(log n)` for add/remove | `O(1)` for add/remove | `O(1)` average for add/remove/contains | `O(1)` for add/remove | `O(log n)` for add/remove | `O(1)` for add/remove |
| **Best For**               | Random access, dynamic arrays | Insertions/deletions at ends, deque operations | Synchronized collections | LIFO operations, stack functionality | Concurrent access, read-heavy lists | Ensuring uniqueness, fast lookups | Ensuring uniqueness with order | Sorted elements, range queries | Concurrent access, read-heavy sets | Efficient key-value mapping, fast lookups | Key-value mappings with order | Sorted key-value mappings | High-concurrency maps | Identity-based key-value mapping | Concurrent access, task queue | Deque operations, fast access from both ends | Task scheduling, priority-based processing | Concurrent deque operations |


##  What are the main interfaces in Java Collections Framework?
<details>
<summary>Answer</summary>

The main interfaces in Java Collections Framework are:

- Collection: The root interface in the collection hierarchy, extended by all other collection interfaces.
- List: Represents an ordered collection (sequence) of elements that can contain duplicate elements. Example: ArrayList, LinkedList.
- Set: A collection that does not allow duplicate elements. Example: HashSet, LinkedHashSet, TreeSet.
- Queue: A collection designed for holding elements prior to processing. Example: LinkedList, PriorityQueue.
- Deque: A double-ended queue that allows elements to be added or removed from both ends. Example: ArrayDeque.
- Map: A collection of key-value pairs, where each key is unique. Example: HashMap, TreeMap, LinkedHashMap.

</details>

## What is the difference between ArrayList and LinkedList?

<details>
<summary>Answer</summary>

- **ArrayList**
  - Internally uses a dynamic array to store elements.
  - Provides faster random access (get()), but slower insertion and deletion, especially in the middle of the list.
  - Memory consumption is more efficient for smaller data sets.

- **LinkedList**
  - Internally uses a doubly linked list.
  - Provides faster insertion and deletion of elements, especially at the beginning or middle.
  - Slower random access (get()), as it needs to traverse the list from the beginning or end to the desired position.
    
</details>

## What is the difference between HashMap and TreeMap?
<details>
<summary>Answer</summary>

- **HashMap**
  - It is based on hashing and does not maintain any order of the elements.
  - Allows one null key and multiple null values.
  - Offers constant-time complexity for basic operations like put() and get(), assuming a good hash function.

- **TreeMap**
  - It is based on a Red-Black tree, and it maintains the keys in a sorted order (natural order or according to a custom comparator).
  - Does not allow null keys (but allows null values).
  - Operations like put(), get(), and remove() are slower than HashMap because of the need to maintain order, but they offer log-time complexity.

</details>

## Explain the differences between HashSet and TreeSet.
<details>
<summary>Answer</summary>

- **HashSet**
  - Does not guarantee any order of the elements.
  - It uses a hash table for storage and offers constant-time complexity for add, remove, and contains operations.
  - Does not maintain elements in any sorted order.
- **TreeSet**
  - Maintains elements in a sorted order (either natural or according to a custom comparator).
  - It is slower than HashSet for basic operations (O(log n) time complexity) because it uses a Red-Black tree for storage.
  - Does not allow null elements.

</details>

## What is the difference between Iterator and ListIterator?
<details>
<summary>Answer</summary>

- **Iterator**
  - Can be used with any collection type (e.g., List, Set).
  - Provides methods like hasNext(), next(), and remove().
  - Can only traverse in the forward direction.

- **ListIterator**
  - A more advanced iterator that is available only for List collections (e.g., ArrayList, LinkedList).
  - Provides methods like hasNext(), next(), previous(), hasPrevious(), add(), set(), and remove().
  - Can traverse both forward and backward in the list.

</details>

## What are the differences between ArrayList and Vector?
<details>
<summary>Answer</summary>

- **ArrayList**
  - Not synchronized (not thread-safe).
  - Grows dynamically as elements are added.
  - Offers better performance in most situations compared to Vector due to its lack of synchronization overhead.

- **Vector**
  - Synchronized, making it thread-safe but at the cost of performance.
  - It doubles the size of the array when it runs out of space (growth rate).
  - Considered outdated, as ArrayList is preferred unless thread safety is specifically needed.

</details>

## What is a ConcurrentHashMap?
<details>
<summary>Answer</summary>

- ConcurrentHashMap is a thread-safe variant of HashMap introduced in Java 5, designed for concurrent access.
- It allows multiple threads to read and write to the map simultaneously without locking the entire map, improving performance in multi-threaded environments.
- It is segmented into different parts (buckets), and each part can be locked independently, allowing for greater concurrency.

</details>

## What is the difference between synchronizedList and CopyOnWriteArrayList?
<details>
<summary>Answer</summary>

- **synchronizedList**
  - A wrapper for any list that synchronizes access to the list.
  - Each method call on the list is synchronized, making it thread-safe, but at the cost of performance.

- **CopyOnWriteArrayList**
  - A thread-safe list where any modification (e.g., add, remove, set) creates a new copy of the underlying array.
  - Ideal for cases where there are more reads than writes.
  - It has better performance for read-heavy operations but incurs a performance penalty on write-heavy operations.

</details>

## What are the benefits of using LinkedHashMap over HashMap?
<details>
<summary>Answer</summary>

- LinkedHashMap maintains the insertion order (or access order if configured) of elements.
- It is useful when you need to maintain the order of elements, while still having constant-time complexity for get() and put().
- It uses a doubly-linked list in addition to a hash table, so it adds some overhead compared to HashMap but provides more control over the order of elements.

</details>

## What is the difference between fail-fast and fail-safe iterators?
<details>
<summary>Answer</summary>

- **Fail-fast iterators:**
  - These iterators throw a ConcurrentModificationException if the collection is modified while being iterated (except through the iterator itself).
  - Example: ArrayList, HashMap.

- **Fail-safe iterators:**
  - These iterators do not throw ConcurrentModificationException. They work with a copy of the collection, so modifications to the collection while iterating do not affect the iterator.
  - Example: CopyOnWriteArrayList, ConcurrentHashMap.

</details>

## What is Collections.unmodifiableList()
<details>
<summary>Answer</summary>

- Collections.unmodifiableList() returns an unmodifiable view of a list. 
- The list itself cannot be modified, and any attempt to modify it (e.g., add(), remove(), etc.) will throw an UnsupportedOperationException. 
- It is useful when you need to expose a read-only version of a collection to prevent accidental modification.

</details>

## What are the differences between PriorityQueue and Queue?
<details>
<summary>Answer</summary>

- **Queue**
  - A general interface for holding elements prior to processing.
  - Implementations include LinkedList, ArrayDeque, etc.
  - Elements are typically processed in FIFO (First-In-First-Out) order.

- **PriorityQueue**
  - A specific implementation of Queue that orders elements based on their priority (using natural ordering or a custom comparator).
  - It does not guarantee FIFO ordering but instead processes elements based on their priority.
  - It is useful in situations like scheduling tasks where some tasks have higher priority than others.

</details>

## What is the purpose of the Comparator interface?
<details>
<summary>Answer</summary>

- Comparator is used to define a custom order for objects in a collection (such as a TreeSet or TreeMap). 
- It allows you to specify how two objects should be compared to determine their relative ordering. 
- This is useful when the natural ordering (via Comparable) is not sufficient, or when you need multiple sorting strategies.

</details>

## What is the difference between Iterator.remove() and Collection.remove()?
<details>
<summary>Answer</summary>

- **iterator.remove():**
  - Removes the last element returned by the iterator. This method can only be called after calling next(), and it removes the element from the collection while iterating.
  - It's the only safe way to remove elements from a collection during iteration without causing ConcurrentModificationException.
- **Collection.remove()**
  - Removes a specific element from the collection (if present). You provide the element, and it removes it from the collection.
  - It is not tied to an iteration process.

</details>

## What is the hashCode() method and how does it work in collections?
<details>
<summary>Answer</summary>

- The hashCode() method is used by hash-based collections like HashMap, HashSet, Hashtable, etc., to determine the bucket where the object should be stored.
- When two objects are equal (i.e., a.equals(b) returns true), they must have the same hash code. However, objects with the same hash code are not necessarily equal (this is known as a hash collision).
- The hashCode() method must be consistent and should be implemented in a way that allows for quick lookups, avoiding excessive collisions in hash-based collections.

</details>

## What is the significance of the Comparable interface in Java collections?
<details>
<summary>Answer</summary>

- The Comparable interface is used to define the natural ordering of objects in a collection (such as TreeSet, TreeMap, or PriorityQueue).
- t provides the compareTo() method, which compares the current object with another object of the same type. 
- The compareTo() method must return:
  - A negative integer if the current object is less than the other object.
  - Zero if the current object is equal to the other object.
  - A positive integer if the current object is greater than the other object.

- Collections like TreeSet and TreeMap use this interface to order elements.
Example

```java
import java.util.*;

class Student implements Comparable<Student> {
    private String name;
    private int age;

    // Constructor
    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    // Implement the compareTo() method to compare by age
    @Override
    public int compareTo(Student other) {
        // Compare by age
        return Integer.compare(this.age, other.age);
    }

    // toString() method for better display
    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class TreeSetExample {
    public static void main(String[] args) {
        // Create a TreeSet to store Students
        Set<Student> students = new TreeSet<>();

        // Add students to the TreeSet
        students.add(new Student("Student1", 22));
        students.add(new Student("Student2", 20));
        students.add(new Student("Student3", 23));
        students.add(new Student("Student4", 21));

        // Print the sorted TreeSet
        System.out.println("Sorted TreeSet of students by age:");
        for (Student student : students) {
            System.out.println(student);
        }
    }
}

```

</details>

## What is the difference between poll() and remove() in a Queue?
<details>
<summary>Answer</summary>

- **poll():**
  - Retrieves and removes the head of the queue. If the queue is empty, it returns null.
  - It's a safer option if you’re unsure whether the queue is empty.
- **remove()**
  - Retrieves and removes the head of the queue. If the queue is empty, it throws a NoSuchElementException.
  - It's generally used when you're sure the queue will not be empty.

</details>


## What is the LinkedHashSet and when would you use it?
<details>
<summary>Answer</summary>

- LinkedHashSet is a collection that implements the Set interface and maintains the insertion order of elements. It uses a hash table (like HashSet) for fast access, but also maintains a linked list of the elements to preserve the order in which they were inserted.
- When to use:
  - When you need the uniqueness guarantee of a Set, but also want to maintain the order of insertion (the order in which elements are added).
  - It is slower than HashSet because of the extra overhead of maintaining the order.

</details>

## Explain the Collections.synchronizedList() method.
<details>
<summary>Answer</summary>

- Collections.synchronizedList() returns a thread-safe version of the specified list. The list returned is backed by the original list but with all methods synchronized.
- This ensures that all operations on the list are thread-safe and can be used in a concurrent environment.
- However, synchronization can introduce performance overhead, and you must manually synchronize blocks of code when iterating over the list to prevent ConcurrentModificationException.

</details>

## How does the CopyOnWriteArrayList work, and when should you use it?
<details>
<summary>Answer</summary>

- CopyOnWriteArrayList is a thread-safe variant of ArrayList where modifications (like add(), remove(), set()) result in a copy of the underlying array being made.
- This ensures that any modifications don’t affect iterators, so iterating over a CopyOnWriteArrayList can occur concurrently with modifications without throwing ConcurrentModificationException.
- When to use: It's ideal for scenarios with frequent reads and rare writes, as it offers excellent performance for read-heavy use cases but incurs a performance penalty for write-heavy operations due to copying the entire array during modifications.

</details>

## What are HashMap's internal working and how does it handle collisions?
<details>
<summary>Answer</summary>

- A HashMap stores key-value pairs in an array of buckets, where the key is hashed to determine the appropriate bucket.
- Collisions occur when multiple keys have the same hash code and thus map to the same bucket. HashMap handles collisions using a technique called bucket chaining, where each bucket contains a linked list (or a tree if the bucket size exceeds a threshold, i.e., 8).
- When two or more keys map to the same bucket, the HashMap will store them in the list or tree, and lookups involve traversing the list or tree to find the correct key.

</details>

## What is the purpose of the Collections.sort() method?
<details>
<summary>Answer</summary>

- Collections.sort() is a utility method in the Collections class used to sort a list of objects.
- By default, it sorts the list in natural order, i.e., according to the Comparable interface of the objects. You can also pass a custom comparator to sort the list according to specific criteria.

</details>

## How does a TreeMap maintain order internally?
<details>
<summary>Answer</summary>

- TreeMap maintains the keys in a sorted order using a Red-Black tree, a self-balancing binary search tree.
- It uses either the natural ordering of the keys (via the Comparable interface) or a custom Comparator provided at the time of instantiation to sort the keys.
- Operations like put(), get(), remove(), etc., have a time complexity of O(log n) because the tree is balanced.

</details>

## What is the difference between TreeSet and HashSet?
<details>
<summary>Answer</summary>

- **TreeSet**
  - Maintains elements in sorted order (either natural order or according to a custom comparator).
  - Slower operations than HashSet (O(log n)) because it uses a Red-Black tree for storage.

- **HashSet**
  - Does not maintain any specific order.
  - Offers constant-time complexity (O(1)) for basic operations like add(), remove(), and contains(), assuming a good hash function.

</details>


## What is the Map.Entry interface?
<details>
<summary>Answer</summary>

- The Map.Entry interface represents a key-value pair in a Map. It allows you to access both the key and the value in an entry of the map.
- It's used in situations where you want to iterate over the map's entries, e.g., using the entrySet() method of a Map:

```java
for (Map.Entry<K, V> entry : map.entrySet()) {
    K key = entry.getKey();
    V value = entry.getValue();
}

```
</details>

##  What is the difference between remove() and clear() in Java Collections?
<details>
<summary>Answer</summary>

- remove(): Removes a single element from the collection, based on either the element itself (for List, Set) or its index (for List). The method returns true if the element was removed, otherwise false.
  - Example: list.remove(Integer.valueOf(3));
- clear(): Removes all elements from the collection. After calling clear(), the collection will be empty.
  - Example: list.clear();

</details>

## What is a WeakHashMap in Java?
<details>
<summary>Answer</summary>

- A WeakHashMap is a map implementation that uses weak references for its keys. If a key is no longer in use (i.e., it is garbage collected), the entry is automatically removed from the map.
- Use case: It's useful for caching or memory-sensitive applications where you don't want to prevent garbage collection of the keys.

```java
Map<KeyType, ValueType> map = new WeakHashMap<>();

```
</details>

## Explain the EnumSet in Java Collections.
<details>
<summary>Answer</summary>

- EnumSet is a specialized Set implementation specifically for use with enum types. It is highly optimized and uses bitwise operations to store the enum constants efficiently.
- EnumSet allows you to create sets that contain only enum values, providing performance improvements over other Set implementations like HashSet when working with enums.

Example 
```java
EnumSet<Day> weekend = EnumSet.of(Day.SATURDAY, Day.SUNDAY);

```

- Advantages
  - It is faster and more space-efficient than HashSet for enums.
  - Provides methods like range(), complementOf(), and allOf() to perform set operations on enum values.

</details>

## Explain the use of Comparator vs Comparable in Java Collections.
<details>
<summary>Answer</summary>

- **Comparable**
  -  The Comparable interface is used to define the natural ordering of objects. It has a single method compareTo(T o) that compares the current object with another object of the same type.
  - Used for: Sorting objects in a collection (e.g., TreeSet, TreeMap) when the class of the objects implements Comparable.

Example 
```java
class Employee implements Comparable<Employee> {
    public int compareTo(Employee other) {
        return this.id - other.id;
    }
}

```

- **Comparator**
  - The Comparator interface is used to define a custom ordering for objects. It has the compare(T o1, T o2) method to compare two objects of the same type.
  - Used for: Sorting objects in cases where the natural ordering (Comparable) is not enough, or when you need multiple sorting strategies.

```java
class EmployeeComparator implements Comparator<Employee> {
    public int compare(Employee e1, Employee e2) {
        return e1.name.compareTo(e2.name);
    }
}

```

</details>

## How do you iterate over a Map in Java?
<details>
<summary>Answer</summary>

You can iterate over a Map using different methods:

- Using entrySet() (most common method for iterating over both keys and values):
```java
for (Map.Entry<K, V> entry : map.entrySet()) {
    K key = entry.getKey();
    V value = entry.getValue();
}

```

- Using keySet() (if you only need the keys):
```java
for (K key : map.keySet()) {
    V value = map.get(key);
}

```

- Using values() (if you only need the values):

```java
for (V value : map.values()) {
    // process value
}

```

</details>



















