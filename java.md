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
