## What is data racing ?

Data racing, also known as a race condition, is a phenomenon that occurs in concurrent programming when multiple threads or processes access shared data concurrently and modify it in an uncontrolled manner. It arises when the final outcome of the program depends on the relative timing or interleaving of the operations performed by different threads.

In a race condition, the behavior of the program becomes unpredictable and incorrect due to the following reasons:

1. Non-Atomic Operations: Operations that are intended to be executed as a single, indivisible unit are not atomic. They can be divided into multiple smaller steps, and if multiple threads are executing these steps concurrently, the interleaving of these steps can lead to unexpected results.

2. Shared Mutable State: Race conditions occur when multiple threads access and modify shared mutable state, such as variables or data structures, without proper synchronization. If one thread modifies the shared data while another thread is reading or modifying it, the outcome can be inconsistent or corrupted.

3. Lack of Synchronization: In concurrent programming, synchronization mechanisms like locks, mutexes, or semaphores are used to coordinate and control access to shared resources. If synchronization is not properly employed, threads can access and modify the shared data simultaneously, leading to race conditions.

4. Timing Dependencies: Race conditions can be influenced by timing dependencies, where the relative order or timing of events affects the outcome. Even small variations in thread scheduling or execution speed can lead to different results.

Race conditions can manifest in various ways, such as incorrect calculations, unexpected program crashes, data corruption, or inconsistent program states. They are often difficult to reproduce and debug since their occurrence depends on the specific timing and interleaving of threads, making them intermittent and non-deterministic.

To mitigate race conditions, proper synchronization techniques, such as locks, atomic operations, or thread-safe data structures, should be employed to ensure mutually exclusive access to shared data. By properly synchronizing access to shared resources, developers can prevent data races and ensure the correctness and reliability of concurrent programs.
