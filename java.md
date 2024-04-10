## JVM vs JRE vs JDK 

JVM, JRE, and JDK are all related to Java programming, but they serve different purposes:

1. **JVM (Java Virtual Machine):**
   - JVM is an abstract computing machine that enables a computer to run Java programs.
   - It provides a runtime environment in which Java bytecode can be executed.
   - JVM interprets the bytecode into machine code or uses Just-In-Time (JIT) compilation to translate it into native machine code for the host platform.
   - JVM provides features like automatic memory management (garbage collection), exception handling, and security.

2. **JRE (Java Runtime Environment):**
   - JRE is a package of software that includes JVM, libraries, and other components necessary for running Java applications.
   - It provides the runtime environment for Java programs without development tools, such as compilers and debuggers.
   - JRE allows end-users to run Java applications on their machines without needing to install the full JDK.

3. **JDK (Java Development Kit):**
   - JDK is a full-featured software development kit that includes everything needed to develop, debug, and deploy Java applications.
   - It contains JRE, development tools (such as javac compiler, debugger, and other utilities), and libraries.
   - JDK is used by developers to write and compile Java code, as well as to create Java applications, applets, and servlets.

In summary, JDK is used by developers for Java development, including writing and compiling code, while JRE is used by end-users to run Java applications, and JVM is the runtime environment that executes Java bytecode.

## Thread life cycle in Java

In Java, threads have a well-defined life cycle, which consists of several distinct states. The thread life cycle in Java includes the following states:

1. New: The thread is in the "new" state when it is created but has not yet started executing. In this state, the thread has been instantiated but has not yet been started by invoking the `start()` method.

2. Runnable: Once the `start()` method is called on a thread object, it moves to the "runnable" state. In this state, the thread is eligible to be scheduled for execution by the thread scheduler. However, it doesn't guarantee immediate execution, as it depends on the availability of system resources and the scheduling algorithm.

3. Running: When a thread is executing its code, it is in the "running" state. In this state, the thread's instructions are being executed by the CPU. It continues to run until it either completes its task, gets blocked, or voluntarily gives up the CPU by invoking `yield()` or `sleep()` methods.

4. Blocked/Waiting: A thread enters the "blocked" or "waiting" state when it is temporarily unable to proceed with its execution. This can happen for various reasons, such as waiting for I/O operations to complete or waiting for a lock to be released. When the blocking condition is resolved, the thread moves back to the "runnable" state.

5. Timed Waiting: Similar to the "blocked/waiting" state, a thread can enter the "timed waiting" state when it needs to wait for a specific period. This can occur when the thread calls methods like `Thread.sleep()`, `Object.wait()`, or `Thread.join()` with a specified timeout. After the time elapses or the condition is satisfied, the thread re-enters the "runnable" state.

6. Terminated: A thread reaches the "terminated" state when it completes its execution or explicitly terminates by calling the `Thread.interrupt()` or `Thread.stop()` method. Once a thread is terminated, it cannot be restarted or moved to any other state.

It's important to note that the transition between thread states is managed by the Java runtime and the underlying operating system, based on various factors such as system resources, thread priorities, synchronization, and blocking operations.

Understanding the thread life cycle in Java helps in proper thread management, coordination, and synchronization in multi-threaded applications.

## Which package use for handle thread pool in java ?
In Java, the `java.util.concurrent` package provides classes and interfaces to handle thread pools. Thread pools are a common mechanism for managing and reusing threads in concurrent programming. The primary classes and interfaces for thread pool management in the `java.util.concurrent` package are:

1. `Executor`: This is an interface that represents an object capable of executing tasks. It provides a single method `execute(Runnable command)` to submit a task for execution.

2. `ExecutorService`: This is a subinterface of `Executor` that extends its functionality by providing additional methods to manage the lifecycle of threads and handle the execution of tasks. It defines methods to submit tasks, control task completion, and obtain `Future` objects representing the results of asynchronous computations.

3. `ThreadPoolExecutor`: This is a class that provides an implementation of the `ExecutorService` interface. It manages a pool of worker threads and allows you to control various parameters related to thread pool size, task scheduling, and thread eviction policies.

4. `Executors`: This class provides utility methods for creating different types of thread pools. It offers static factory methods to create thread pools of fixed size, cached thread pools with automatic thread reclamation, single-threaded executor services, and more.

Here's an example of creating a thread pool using the `Executors` class:

```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Create a fixed-size thread pool with 5 threads
        ExecutorService executor = Executors.newFixedThreadPool(5);

        // Submit tasks for execution
        for (int i = 0; i < 10; i++) {
            Runnable task = new MyTask(i);
            executor.execute(task);
        }

        // Shutdown the executor when no more tasks need to be submitted
        executor.shutdown();
    }

    static class MyTask implements Runnable {
        private int taskId;

        public MyTask(int taskId) {
            this.taskId = taskId;
        }

        @Override
        public void run() {
            System.out.println("Task " + taskId + " executed by thread: " + Thread.currentThread().getName());
        }
    }
}
```

## Java synchronized keyword

In Java, the `synchronized` keyword is used to provide mutual exclusion and thread-safety in concurrent programming. It ensures that only one thread can access a synchronized block or method at a time, preventing multiple threads from interfering with shared resources simultaneously. The `synchronized` keyword can be applied to methods or blocks of code.

1. Synchronized Methods:
When a method is declared as `synchronized`, it becomes a synchronized method. Only one thread can execute a synchronized method on a particular instance of the class at a time. Other threads attempting to invoke the synchronized method will be blocked until the executing thread completes the method or releases the lock.

Example:
```java
public synchronized void synchronizedMethod() {
    // Synchronized method code
}
```

2. Synchronized Blocks:
Synchronized blocks allow finer-grained control over the section of code that needs to be synchronized. A synchronized block is enclosed within braces and requires a lock object as a parameter. The lock object can be any Java object, and it serves as the mutual exclusion mechanism.

Example:
```java
public void someMethod() {
    // Non-synchronized code

    synchronized(lockObject) {
        // Synchronized block code
    }

    // Non-synchronized code
}
```

In the above example, only one thread can enter the synchronized block at a time if they share the same `lockObject`. Other threads that encounter the synchronized block will wait until the lock is released.

Key points to note about the `synchronized` keyword:

- Synchronization ensures that changes made by one thread are visible to other threads. It provides memory visibility and prevents race conditions.
- Synchronized blocks or methods introduce some performance overhead due to acquiring and releasing locks, so they should be used judiciously.
- It's important to ensure that all threads accessing shared resources use synchronization to avoid inconsistencies or data corruption.
- Synchronization can be applied to both instance methods and static methods, allowing for synchronization at the object level or class level, respectively.

While the `synchronized` keyword is a powerful tool for managing concurrent access to shared resources, Java also provides other synchronization mechanisms such as locks, semaphores, and condition variables, which may offer more flexibility in certain scenarios.

In the above example, a fixed-size thread pool with 5 threads is created using `Executors.newFixedThreadPool(5)`. Tasks are submitted for execution using the `execute()` method of `ExecutorService`. Each task is represented by a `Runnable` object. Finally, the `shutdown()` method is called on the executor to gracefully shut it down after executing all submitted tasks.

Using the thread pool classes and interfaces from the `java.util.concurrent` package simplifies the management of threads and improves the efficiency of concurrent programming in Java.

## What is string constant pool in java

In Java, the "String constant pool" is a special area of memory where Java keeps unique string literals. When you create a string using double quotes (`" "`), Java first checks if that string already exists in the string constant pool. If it does, Java returns a reference to the existing string; otherwise, it creates a new string object in the pool and returns a reference to it.

Here's an example:

```java
String s1 = "hello";
String s2 = "hello";
String s3 = new String("hello");

System.out.println(s1 == s2);  // true, because both s1 and s2 refer to the same string in the constant pool
System.out.println(s1 == s3);  // false, because s3 is a new string object created with the `new` keyword
```

In this example, `s1` and `s2` both refer to the same string object `"hello"` in the string constant pool because Java detects that `"hello"` is already present in the pool and reuses it. However, `s3` is created with the `new` keyword, so it's a separate object, even though its content is the same as `"hello"`. Therefore, `s1 == s3` returns `false`.

The use of the string constant pool helps conserve memory and improves performance by avoiding unnecessary duplication of string objects.

## Where string constant pool store ?

The string constant pool is part of the Java Runtime Environment's (JRE) method area, which is a part of the Java heap memory. 

In the Java memory model, the method area is a shared, read-only memory space that stores class structures, method and field information, static variables, constant pool, and other metadata required by the JVM. The string constant pool is one of the components within the method area.

When a Java program is executed, the JVM loads classes into the method area and initializes their metadata, including the constant pool for each class. The string constant pool is where unique string literals are stored, and it is shared across all instances of a class.

By storing string literals in the string constant pool, Java optimizes memory usage by avoiding unnecessary duplication of identical string objects. This approach also improves performance by facilitating faster string comparison and reducing the overhead of string creation.

## Why need separate the string constant pool from the general heap memory ?

Separating the string constant pool from the general heap memory serves several purposes, primarily related to optimization and efficiency:

1. **Constant Strings**: Strings declared as constants or literals in the code are immutable. They don't change throughout the program's execution. Placing them in a separate pool allows for optimization because the compiler can recognize duplicate string literals and store them only once. This saves memory space and enhances performance by reducing the need for duplicate string allocations.

2. **Quick Lookup**: Placing strings in a separate pool allows for quick lookup and comparison. Since strings in the constant pool are immutable, they can be cached and reused throughout the program. This speeds up operations like string comparisons, as they can often be reduced to simple reference checks rather than comparing each character.

3. **Garbage Collection Optimization**: String constant pool management can be optimized separately from general heap memory management. Garbage collection strategies can be tailored specifically for immutable strings, which may differ from those used for mutable objects in the heap. For example, since strings in the pool are immutable, they don't need to be checked for changes during garbage collection cycles, which can improve garbage collection performance.

4. **Security**: Since string literals are often used in critical parts of code, separating them into a distinct memory area can provide additional security benefits. For instance, if a program has a vulnerability that allows unauthorized memory access, keeping sensitive string literals separate can make it harder for attackers to manipulate or exploit them.

5. **Predictable Behavior**: By isolating string literals in a separate pool, developers can rely on consistent behavior regarding string manipulation and comparison. This separation helps in maintaining predictable program behavior, which is crucial for debugging and ensuring the correctness of the software.

Overall, separating the string constant pool from the general heap memory helps in optimizing memory usage, improving performance, enhancing security, and ensuring predictable behavior in programs that heavily utilize string literals.

## Questions about exception

1. What is the difference between checked and unchecked exceptions?

2. What happens behind the code int data=50/0;?

3. Why use multiple catch block?

4. Is there any possibility when the finally block is not executed?

5. What is exception propagation?

6. What is the difference between the throw and throws keyword?

7. What are the 4 rules for using exception handling with method overriding?

Let's break down your questions one by one:

1. **Difference between checked and unchecked exceptions:**
   - Checked exceptions are the exceptions that are checked at compile-time. These are exceptions that the compiler forces you to handle or declare using a `throws` clause. Examples include `IOException`, `SQLException`, etc.
   - Unchecked exceptions, on the other hand, are not checked at compile-time. These usually occur at runtime and are subclasses of `RuntimeException`. Examples include `NullPointerException`, `ArrayIndexOutOfBoundsException`, etc.

2. **What happens behind the code `int data = 50/0;`?**
   - This line of code will throw an `ArithmeticException` at runtime because dividing by zero is not allowed in Java. When the code is executed, the JVM will encounter this division by zero operation and throw the exception.

3. **Why use multiple catch blocks?**
   - Multiple catch blocks are used to handle different types of exceptions separately. This allows you to provide specific error handling logic for each type of exception that might occur in your code.

4. **Is there any possibility when the finally block is not executed?**
   - Yes, there are a few scenarios where the finally block may not be executed:
     - If the JVM exits while executing the try or catch block due to a call to `System.exit()`.
     - If the thread executing the try or catch block is interrupted or killed.
     - If there's an infinite loop or deadlock within the try or catch block that prevents the program from proceeding.

5. **What is exception propagation?**
   - Exception propagation is the mechanism by which an exception is passed from one method to another method in the call stack until it's caught or until the program terminates.

6. **Difference between the throw and throws keyword:**
   - `throw` keyword is used to explicitly throw an exception within a method or block of code.
   - `throws` keyword is used in the method signature to declare that the method might throw certain types of exceptions. It doesn't actually throw the exception but specifies that the method may throw it, and the responsibility to handle it lies with the caller.

7. **Four rules for using exception handling with method overriding:**
   - The overridden method cannot throw checked exceptions that are new or broader than the ones declared by the overridden method.
   - The overriding method can throw narrower or fewer exceptions than the overridden method.
   - The overriding method can throw any unchecked exception, regardless of whether the overridden method declares the same exception or not.
   - The overriding method must not throw any new or broader checked exceptions that are not subclasses of the exceptions thrown by the overridden method.
