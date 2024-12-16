# Java Thread Questions & Answer

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


## What is a thread in Java?
<details>
<summary>Answer</summary>

- A thread in Java is a lightweight process that allows the program to perform multiple tasks concurrently. 
- Java provides built-in support for multithreading, which enables developers to write programs that can execute multiple threads simultaneously.

- Threads in Java are implemented using the Thread class or implementing the Runnable interface. 
- Each thread has its own stack, program counter, and local variables, but they share the heap space.

</details>

## What is the difference between Thread and Runnable in Java?
<details>
<summary>Answer</summary>

- **Thread:** A Thread class represents a thread of execution in a program. You can either create a new Thread object and override its run() method, or pass a Runnable object to the Thread constructor.
- **Runnable:** A Runnable is a functional interface with a single method run(), representing a task that can be executed by a thread. Implementing Runnable allows for more flexibility because you can pass the same Runnable task to multiple threads.

**Key Differences:**
- Thread is a class, whereas Runnable is an interface.
- Runnable allows for better code separation and reusability since it doesn't require extending the Thread class.

</details>

## How can you create a thread in Java?
<details>
<summary>Answer</summary>

**There are two ways to create a thread in Java:**

- By extending the Thread class:

```java
class MyThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t = new MyThread();
        t.start(); // Start the thread
    }
}

```

- By implementing the Runnable interface:

```java
class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) {
        Runnable r = new MyRunnable();
        Thread t = new Thread(r);
        t.start(); // Start the thread
    }
}

```
</details>


## What is the start() method in Java threads?
<details>
<summary>Answer</summary>

- The start() method in Java is used to initiate the execution of a thread. 
- When you invoke start(), a new thread is created, and the run() method is executed in that thread. 
- It is important to note that start() should only be called once on a thread object. 
- Calling run() directly would just execute it in the current thread, not a new thread.

```java
Thread thread = new Thread();
thread.start(); // This calls the run() method in a new thread

```

</details>

## What is the difference between sleep() and wait() in Java?
<details>
<summary>Answer</summary>
 
- sleep(long millis): This method is a static method of the Thread class, and it pauses the current thread for a specified number of milliseconds. 
- The thread is paused and doesn't hold any locks.

```java
Thread.sleep(1000); // Sleeps for 1 second

```
- **wait():**
  - This method is defined in the Object class and must be called from within a synchronized block. 
  - It makes the current thread release the lock and enter the waiting state until another thread notifies it using notify() or notifyAll().

```java
synchronized(obj) {
    obj.wait(); // Causes the current thread to wait
}

```
</details>

## What is thread synchronization in Java?
<details>
<summary>Answer</summary>

- Thread synchronization in Java is the mechanism that ensures that only one thread can access a critical section (a block of code) at a time. 
- This is important to avoid data inconsistency when multiple threads modify shared data simultaneously.

**You can achieve synchronization by using:**
- Synchronized methods:

```java
public synchronized void method() {
    // synchronized code block
}

```

- Using Synchronized blocks:

```java
public void method() {
    synchronized(this) {
        // critical section
    }
}

```
- By synchronizing methods or blocks, we ensure that only one thread can execute them at a time, preventing race conditions.
</details>

## What is a race condition in Java?
<details>
<summary>Answer</summary>

- A race condition occurs when two or more threads try to access and modify shared resources concurrently, leading to inconsistent or unexpected results. 
- This happens when thread synchronization is not properly managed.

```java
class Counter {
    private int count = 0;

    public void increment() {
        count++; // Non-synchronized method may cause race condition
    }
}

```

- In this case, multiple threads calling the increment() method simultaneously may cause the value of count to be incorrect.
- To avoid race conditions, we use synchronization to ensure that only one thread can access the critical section at a time.

</details>

## What is a deadlock in Java?
<details>
<summary>Answer</summary>

- Deadlock is a situation in multithreading where two or more threads are blocked forever because they are waiting for each other to release resources that they need.

**Deadlock occurs when:**

    - Thread 1 holds lock A and waits for lock B.
    - Thread 2 holds lock B and waits for lock A.

**To prevent deadlocks, we can:**
- Use a timeout for acquiring locks (e.g., ReentrantLock with tryLock()).
- Always acquire locks in the same order.

</details>

## What are notify() and notifyAll() methods in Java?
<details>
<summary>Answer</summary>

- Both notify() and notifyAll() are used to wake up threads that are waiting on an object’s monitor.

**notify():**
- Wakes up a single thread that is waiting on the object's monitor (if any threads are waiting). If multiple threads are waiting, it is not guaranteed which thread will be awakened.

**notifyAll():**
- Wakes up all the threads that are waiting on the object's monitor.


```java
synchronized (obj) {
    obj.notify(); // or obj.notifyAll();
}

```

</details>


## What is the difference between ExecutorService and ThreadPoolExecutor?
<details>
<summary>Answer</summary>

**ExecutorService:**
- An interface that provides a higher-level replacement for the Thread class. 
- It provides methods for managing and controlling thread execution, such as submit(), shutdown(), and invokeAll().

**ThreadPoolExecutor:**
- A concrete implementation of the ExecutorService interface. 
- It provides a pool of threads to execute tasks concurrently. 
- The ThreadPoolExecutor can be configured with various parameters like core pool size, maximum pool size, and the queue used for holding tasks.

```java
ExecutorService executor = Executors.newFixedThreadPool(10);
executor.submit(() -> {
    // task code
});
executor.shutdown();

```
</details>


## What is the ForkJoinPool in Java?
<details>
<summary>Answer</summary>

- The ForkJoinPool is a specialized implementation of ExecutorService designed to work efficiently with tasks that can be divided into smaller subtasks recursively. 
- It is useful for parallelizing divide-and-conquer algorithms.
- ForkJoinPool uses a work-stealing algorithm, where idle threads can "steal" tasks from other threads, improving resource utilization.

Example of using ForkJoinPool:

```java
ForkJoinPool forkJoinPool = new ForkJoinPool();
forkJoinPool.submit(() -> {
    // divide-and-conquer task
});

```

</details>


## What is the difference between synchronized block and ReentrantLock in Java?
<details>
<summary>Answer</summary>

Both synchronized block and ReentrantLock are used to achieve thread synchronization, but they differ in terms of flexibility and features.

- **synchronized block:**
  - Simpler and easier to use.
  - Implicitly locks the object, and the lock is automatically released when the block is exited (either normally or via an exception).
  - Cannot try to acquire a lock with a timeout.
  - Works only with intrinsic locks (objects).

```java
synchronized (lockObject) {
    // synchronized code
}

```

- **ReentrantLock**:
  - A more advanced and flexible alternative to synchronized.
  - Provides additional functionality like tryLock(), lockInterruptibly(), and newCondition().
  - You must manually release the lock using unlock().
  - Allows for fair locking (threads can acquire the lock in the order they request it) via the ReentrantLock(true) constructor.

```java
ReentrantLock lock = new ReentrantLock();
try {
    lock.lock();
    // critical section
} finally {
    lock.unlock();
}

```

</details>


## What is a thread pool, and why is it used?

<details>
<summary>Answer</summary>

- A thread pool is a collection of pre-instantiated worker threads that are ready to execute tasks. 
- Instead of creating a new thread every time a task is executed (which can be inefficient), tasks are submitted to the thread pool, where they are assigned to available threads.

**Advantages of using a thread pool:**
- Improved performance: Avoids the overhead of repeatedly creating and destroying threads.
- Resource management: Limits the number of threads, preventing resource exhaustion.
- Better resource utilization: Threads in a pool can be reused, making it more efficient in managing threads.


Java provides the ExecutorService interface, which is implemented by classes such as ThreadPoolExecutor and factory methods like Executors.newFixedThreadPool().

```java
ExecutorService executor = Executors.newFixedThreadPool(10);
executor.submit(() -> {
    // task code
});

```

</details>

## What is the significance of the volatile keyword in Java?
<details>
<summary>Answer</summary>

- The volatile keyword in Java is used to indicate that a variable’s value can be changed by different threads concurrently. When a field is declared volatile, it ensures that:
  - **Visibility**
    - The value of the variable is always visible to all threads. This means when one thread modifies the value of a volatile variable, the new value is immediately visible to other threads.
  - **Atomicity**
    -  For simple types like boolean, int, etc., access to volatile variables is atomic (for example, reading and writing a volatile int is atomic). However, compound actions like i++ are not atomic and still require synchronization.

```java
private volatile boolean flag = false;

public void updateFlag() {
    flag = true; // This change will be visible to all threads immediately
}

```

- The volatile keyword should not be used as a replacement for proper synchronization, but it can be helpful for flags or state variables that are frequently checked but not modified in complex ways.


</details>


## What is the ThreadLocal class in Java, and when would you use it?
<details>
<summary>Answer</summary>

- The ThreadLocal class provides thread-local variables, which means each thread accessing a ThreadLocal variable gets its own copy of the variable. 
- This ensures that one thread cannot see or modify the value of a variable that is used by another thread.
- Each thread can have its own independent copy of a variable, which eliminates the need for synchronization.
- **Usage**
  -  It's useful when you need to store data that is thread-specific (e.g., database connections or user session data). 
  - This way, no synchronization is needed since each thread accesses its own isolated copy.

```java
ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 1);

public void someMethod() {
    Integer value = threadLocal.get();
    System.out.println(value);
    threadLocal.set(value + 1);
}

```
- Each thread will have its own value that is stored in ThreadLocal.

</details>


## What is the difference between Callable and Runnable in Java?
<details>
<summary>Answer</summary>

**Runnable**:
- Represents a task that can be executed by a thread.
- The run() method does not return a result and cannot throw a checked exception.
- It is mainly used for tasks that do not need to return a value or throw exceptions.

```java
Runnable task = () -> {
    System.out.println("Task is running");
};

```

**Callable**:
- Similar to Runnable, but it can return a result and throw a checked exception.
- The call() method returns a result (wrapped in a Future), which can be accessed later using Future.get().

```java
Callable<Integer> task = () -> {
    return 123;
};
ExecutorService executor = Executors.newFixedThreadPool(1);
Future<Integer> result = executor.submit(task);
Integer value = result.get();  // This will return 123

```

- Callable is useful when you need to get a result from the task or handle exceptions during execution.

</details>


##  What is the join() method in Java threads, and how is it used?
<details>
<summary>Answer</summary>

- The join() method allows one thread to wait for the completion of another thread. 
- When join() is called on a thread, the calling thread (usually the main thread) pauses until the thread on which join() was called finishes executing.
- Usage: It's useful when you need to ensure that one thread has completed its execution before another thread continues.

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running");
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        MyThread t1 = new MyThread();
        t1.start();
        t1.join();  // Main thread waits for t1 to finish
        System.out.println("Main thread continues");
    }
}

```

- In the above example, the main thread will wait until t1 completes before it proceeds with the next statement.

</details>

##  What is the difference between notify() and notifyAll() in a synchronized context?
<details>
<summary>Answer</summary>

- notify(): Wakes up one thread that is waiting on the current object's monitor. If there are multiple threads waiting, one of them is chosen at random, but there is no guarantee as to which one.
- notifyAll(): Wakes up all the threads that are waiting on the current object's monitor. This is useful when you want all threads to check a certain condition after being notified.


**When to use notify() vs notifyAll():**
- Use notify() when you know only one thread should proceed (for example, when a condition is met, and only one thread should proceed).
- Use notifyAll() when multiple threads may need to be notified to re-check conditions or perform actions based on updated data.

</details>

## What is the significance of the ExecutorService interface in Java?
<details>
<summary>Answer</summary>

- ExecutorService is a high-level interface in Java that provides a framework for managing and controlling thread execution. It decouples the task submission from the mechanics of how each task will be executed (e.g., using a thread pool). It is part of the java.util.concurrent package.
- Provides methods like submit(), invokeAll(), and shutdown().
- The ExecutorService manages the lifecycle of threads, making it easier to implement parallel tasks without directly managing individual threads.
- It simplifies the process of task scheduling, handling timeouts, and managing thread pools.

```java
ExecutorService executorService = Executors.newFixedThreadPool(4);
Future<Integer> future = executorService.submit(() -> {
    // Perform some task
    return 123;
});
Integer result = future.get();  // Get the result of the task
executorService.shutdown();

```

</details>


## What is Starvation or Thread Starvation?
<details>
<summary>Answer</summary>

- Starvation refers to a situation in multithreading where a thread is perpetually denied access to resources it needs to proceed (like CPU time), usually because other threads are continually getting the resources instead. 
- As a result, the starved thread may never get a chance to execute, or it executes very infrequently.

- Example Scenario of Starvation: If you have a situation where threads with high priority are always executing and consuming resources, the lower-priority threads might never get a chance to run, leading to starvation.

```java
class StarvationExample {
    public static void main(String[] args) {
        Thread lowPriorityThread = new Thread(() -> {
            while (true) {
                System.out.println("Low priority thread is running");
            }
        });

        Thread highPriorityThread = new Thread(() -> {
            while (true) {
                System.out.println("High priority thread is running");
            }
        });

        // Set priority of high-priority thread to maximum
        highPriorityThread.setPriority(Thread.MAX_PRIORITY);
        lowPriorityThread.setPriority(Thread.MIN_PRIORITY);

        lowPriorityThread.start();
        highPriorityThread.start();
    }
}

```
</details>


## Can you explain the key differences between instance-level locking (synchronized(this)) and class-level locking (synchronized(SomeClass.class)) in Java? When would you use one over the other?
<details>
<summary>Answer</summary>

- In Java, both instance-level locking and class-level locking are used for synchronizing code blocks to ensure that only one thread can execute a specific section of code at a time. However, the key differences between them lie in what they lock on and how they affect thread synchronization.
- Let's break down the differences and when to use each:

**Scope of Synchronization:**
- **Instance-Level Locking (synchronized(this)):**
  - Applies to instance methods and instance variables.
  - When a method or block is synchronized on this, it ensures that only one thread can execute a synchronized method/block on the same instance at a time.
  - This means synchronization is applied on a per-instance basis, meaning different instances of the class can be accessed concurrently if they are synchronized on this.
```java
class Counter {
    private int count = 0;

    public void increment() {
        synchronized(this) {  // Synchronize on the instance level (this)
            count++;
        }
    }

    public void decrement() {
        synchronized(this) {  // Synchronize on the instance level (this)
            count--;
        }
    }
}

```
- Here, two different threads accessing increment() or decrement() on different instances of Counter can run concurrently, as they synchronize on separate instances.


**Class-Level Locking (synchronized(SomeClass.class)):**
- Applies to static methods and static variables.
- When synchronized on the class object (SomeClass.class), the lock applies to all threads accessing static methods or variables for the entire class, not just individual instances.
- This means only one thread can execute any synchronized block or static method on the class at a time, regardless of how many instances exist.

```java
class Counter {
    private static int count = 0;

    public static void increment() {
        synchronized(Counter.class) {  // Synchronize on the class object (Counter.class)
            count++;
        }
    }

    public static void decrement() {
        synchronized(Counter.class) {  // Synchronize on the class object (Counter.class)
            count--;
        }
    }
}

```
- Here, all threads accessing the static methods increment() or decrement() will be synchronized on the class object, meaning only one thread can execute these methods at a time, even if different threads are working with different instances of Counter.


</details>


## What happens to the main thread when it creates other threads but does not wait for them to finish (i.e., does not use join())? Will the main thread terminate immediately, or will it wait for the other threads to complete? How does the behavior differ for daemon and non-daemon threads?
<details>
<summary>Answer</summary>

In Java, the behavior of the main thread when it creates other threads and doesn't wait for them depends on whether the created threads are daemon or non-daemon threads.


- Main Thread with Non-Daemon Threads:
  - Main thread execution: When the main thread creates other non-daemon threads (i.e., threads that are not marked as daemon), it will not wait for those threads to finish, unless explicitly instructed to do so using the join() method.
  - Main thread behavior: As soon as the main thread finishes executing its tasks, it will terminate, but the JVM will not exit until all non-daemon threads have completed their execution. This is because the JVM keeps running as long as any non-daemon threads are alive.
  - JVM behavior: The JVM will continue running until all non-daemon threads (including those created by the main thread) have finished executing, even if the main thread has already finished.


```java
class MyThread extends Thread {
    @Override
    public void run() {
        try {
            Thread.sleep(2000);  // Simulating work
            System.out.println("Thread finished work.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class MainThreadExample {
    public static void main(String[] args) {
        Thread t1 = new MyThread();
        Thread t2 = new MyThread();

        t1.start();
        t2.start();

        System.out.println("Main thread finishing.");
        // Main thread does NOT wait for t1 and t2 to finish
    }
}

```

- The main thread prints "Main thread finishing." and exits, but the JVM will not terminate immediately. It waits until both t1 and t2 (non-daemon threads) finish their work.



- Main Thread with Daemon Threads:
  - Main thread execution: When the main thread creates daemon threads (i.e., threads that are marked as daemon using thread.setDaemon(true)), the behavior is different:
  - Main thread behavior: The main thread will finish its execution as soon as it completes its tasks, without waiting for the daemon threads to finish.
  - JVM behavior: The JVM will exit immediately when the main thread finishes, even if daemon threads are still running. This happens because daemon threads are background threads that do not prevent the JVM from exiting.

```java
class DaemonThread extends Thread {
    @Override
    public void run() {
        try {
            Thread.sleep(2000);  // Simulating work
            System.out.println("Daemon thread finished work.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

public class MainThreadExample {
    public static void main(String[] args) {
        Thread t1 = new DaemonThread();
        Thread t2 = new DaemonThread();

        t1.setDaemon(true);  // Marking as daemon thread
        t2.setDaemon(true);  // Marking as daemon thread

        t1.start();
        t2.start();

        System.out.println("Main thread finishing.");
        // Main thread does NOT wait for t1 and t2 to finish
    }
}

```

- The main thread finishes and prints "Main thread finishing." immediately. 
- The JVM will exit, even though the daemon threads (t1 and t2) may still be running or not finished with their tasks.

</details>

