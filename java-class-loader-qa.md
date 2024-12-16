# Java Class loader Questions & Answer

## Disclaimer
- [Disclaimer](disclaimer-qa.md)

## What is a ClassLoader in Java?
<details>
<summary>Answer</summary>

- A ClassLoader in Java is responsible for dynamically loading classes into the JVM during runtime. 
- The JVM uses a hierarchical class loading model, which includes the Bootstrap ClassLoader, Extension ClassLoader, and System ClassLoader. 
- ClassLoaders allow the JVM to load classes from locations like the classpath, JAR files, or even custom sources.

</details>

## What are the different types of ClassLoaders in Java?
<details>
<summary>Answer</summary>

- There are three main types of ClassLoaders in Java:
  - **Bootstrap ClassLoader:** Loads core Java classes (from rt.jar).
  - **Extension ClassLoader:** Loads classes from the JDK's ext directory or directories specified by the java.ext.dirs system property.
  - **System ClassLoader (Application ClassLoader):** Loads classes from the classpath defined by the user.


- These class loaders form a hierarchy, with each class loader delegating to its parent loader.

</details>

## What is the purpose of the findClass() method in ClassLoader?
<details>
<summary>Answer</summary>

- The findClass() method is used by the ClassLoader to locate a class file and return a Class object representing that class. 
- It's a method that must be overridden in custom ClassLoaders to load a class from a custom source (e.g., a database or network). 
- It is called internally by loadClass().


```java
import java.io.*;
import java.net.URL;
import java.net.URLClassLoader;

public class MyClassLoader extends ClassLoader {
    
    private String classPath;

    // Constructor accepting classpath location
    public MyClassLoader(String classPath) {
        this.classPath = classPath;
    }

    // Override the findClass method to load a class from a specified directory
    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        try {
            // Convert class name to file path by replacing '.' with '/'
            String classFileName = classPath + File.separator + name.replace('.', File.separatorChar) + ".class";
            File classFile = new File(classFileName);
            
            // If the class file doesn't exist, throw ClassNotFoundException
            if (!classFile.exists()) {
                throw new ClassNotFoundException("Class not found: " + name);
            }

            // Read the class file into a byte array
            byte[] classData = new byte[(int) classFile.length()];
            try (FileInputStream fis = new FileInputStream(classFile)) {
                fis.read(classData);
            }

            // Define the class from the byte array
            return defineClass(name, classData, 0, classData.length);
        } catch (IOException e) {
            throw new ClassNotFoundException("Failed to load class: " + name, e);
        }
    }
    
    // Test the custom class loader
    public static void main(String[] args) {
        try {
            // Specify the directory containing the class files
            String classPath = "/path/to/classes";
            
            // Create an instance of MyClassLoader
            MyClassLoader myClassLoader = new MyClassLoader(classPath);
            
            // Load the class using the custom class loader
            Class<?> loadedClass = myClassLoader.loadClass("com.example.MyClass");

            // Use reflection to instantiate the class and call a method
            Object instance = loadedClass.getDeclaredConstructor().newInstance();
            System.out.println("Class " + loadedClass.getName() + " loaded successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```
</details>

## What is the difference between loadClass() and findClass()?

<details>
<summary>Answer</summary>

- loadClass(): Responsible for loading the class and checking whether it's already loaded. It delegates the actual class loading to the findClass() method, if not already loaded.
- findClass(): A method to be implemented in custom ClassLoaders to load the class from a specific location. It is called internally by loadClass() when the class is not found.

</details>

## What is the difference between Class.forName() and ClassLoader.loadClass()?
<details>
<summary>Answer</summary>

- Class.forName(): Loads the class and initializes it (executes static blocks and static variable initializations).
- ClassLoader.loadClass(): Loads the class but does not initialize it, meaning static blocks are not executed until the class is explicitly used.

</details>

## What is the ClassLoader hierarchy in Java?
<details>
<summary>Answer</summary>

- The ClassLoader hierarchy in Java follows a parent-child relationship:
  - Bootstrap ClassLoader (loads core Java libraries).
  - Extension ClassLoader (loads classes from ext directories).
  - System (Application) ClassLoader (loads classes from the user-defined classpath).
</details>


## What is the role of the Bootstrap ClassLoader?
<details>
<summary>Answer</summary>

- The Bootstrap ClassLoader is responsible for loading the core Java libraries (e.g., java.lang.*, java.util.*) from the rt.jar or equivalent location. 
- It is the parent of all other class loaders and is implemented in native code, making it the first class loader in the class loading hierarchy.

</details>

## Can you explain the Class Loading process in Java?
<details>
<summary>Answer</summary>

- The class loading process occurs in three steps:
  - Loading: The class loader loads the class from a specified source (e.g., classpath or JAR).
  - Linking: Includes Verification, Preparation (default values for static variables), and Resolution (symbolic references are resolved).
  - Initialization: Static blocks and static variables are initialized.

</details>

## How can you create a custom ClassLoader?
<details>
<summary>Answer</summary>

- You can create a custom ClassLoader by extending the ClassLoader class and overriding the findClass() method to define how the class data is located and loaded.

Example:
```java
public class MyClassLoader extends ClassLoader {
    @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
        // Load class data from a custom source
        byte[] data = loadClassData(name);
        return defineClass(name, data, 0, data.length);
    }
}

```
</details>

## What is the purpose of defineClass() in ClassLoader?
<details>
<summary>Answer</summary>

- The defineClass() method is used to define a class from a byte array. After reading class data (e.g., from a file or network), you pass it to defineClass() to create a Class object. 
- This method is typically used in custom ClassLoaders to convert raw byte data into a class.

</details>

## What happens when a class is loaded multiple times in Java?
<details>
<summary>Answer</summary>

- A class is loaded only once per ClassLoader. If a class is requested again by the same ClassLoader, it is not reloaded. 
- However, if the class is requested by different ClassLoaders (e.g., in different web applications), the class is treated as different classes by the JVM.

</details>

##  What is the getParent() method in a ClassLoader and why is it important?
<details>
<summary>Answer</summary>

- The getParent() method returns the parent ClassLoader of the current ClassLoader. 
- It's important because Java ClassLoaders follow a delegation model. 
- When a ClassLoader is asked to load a class, it first delegates the request to its parent before attempting to load the class itself. 
- This ensures that the system classes are always loaded by the Bootstrap ClassLoader.

```java
 @Override
    protected Class<?> findClass(String name) throws ClassNotFoundException {
  System.out.println("Trying to load class: " + name);

  // First, try to load the class using the parent class loader
  try {
    // Attempt to load the class from the parent class loader
    Class<?> loadedClass = getParent().loadClass(name);  // Call to parent's loadClass
    System.out.println("Class loaded by parent class loader: " + loadedClass.getName());
    return loadedClass;
  } catch (ClassNotFoundException e) {
    System.out.println("Class not found by parent, attempting to load manually.");
  }
  // Here you can load the class ..

}
```
</details>

## What is the significance of the getResource() and getResourceAsStream() methods?
<details>
<summary>Answer</summary>

- getResource(String name): Returns the URL of a resource (e.g., configuration files, images) that can be loaded from the classpath.
- getResourceAsStream(String name): Returns an InputStream for reading the resource as a stream of bytes.

</details>