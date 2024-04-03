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

In the above example, a fixed-size thread pool with 5 threads is created using `Executors.newFixedThreadPool(5)`. Tasks are submitted for execution using the `execute()` method of `ExecutorService`. Each task is represented by a `Runnable` object. Finally, the `shutdown()` method is called on the executor to gracefully shut it down after executing all submitted tasks.

Using the thread pool classes and interfaces from the `java.util.concurrent` package simplifies the management of threads and improves the efficiency of concurrent programming in Java.
