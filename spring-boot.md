### In spring boot how many ways we can use IOC ?

In Spring Boot, there are mainly three ways to utilize Inversion of Control (IOC) and dependency injection:

1. Constructor Injection: This is the most preferred and recommended way of dependency injection in Spring Boot. You can annotate the constructor of a class with `@Autowired`, and Spring will automatically resolve and inject the required dependencies when creating an instance of that class. For example:

```java
@Service
public class MyService {
    private final MyRepository myRepository;

    @Autowired
    public MyService(MyRepository myRepository) {
        this.myRepository = myRepository;
    }
}
```

2. Setter Injection: In this approach, you annotate a setter method with `@Autowired`, and Spring will inject the dependency by invoking the setter method. Setter injection is considered less preferable than constructor injection because it allows optional dependencies and can lead to objects in an inconsistent state. However, it can still be useful in certain scenarios. For example:

```java
@Service
public class MyService {
    private MyRepository myRepository;

    @Autowired
    public void setMyRepository(MyRepository myRepository) {
        this.myRepository = myRepository;
    }
}
```

3. Field Injection: This approach involves directly injecting dependencies into the fields of a class using the `@Autowired` annotation. Field injection is generally discouraged because it violates encapsulation and makes it harder to write unit tests. However, it can be used for quick prototyping or in certain framework-related scenarios. For example:

```java
@Service
public class MyService {
    @Autowired
    private MyRepository myRepository;
}
```

It's worth mentioning that starting from Spring Framework 4.3, constructor injection is recommended as the default choice for dependency injection. It promotes immutability and helps ensure that the required dependencies are always provided. Therefore, it's generally recommended to use constructor injection whenever possible in Spring Boot applications.

## Why should we not field injection ?

Field injection is generally discouraged for several reasons:

1. Encapsulation and Readability: Field injection violates the principle of encapsulation, as it directly exposes dependencies as public fields. This can make it harder to reason about the class's behavior and can lead to unwanted direct access to dependencies from other classes. Using encapsulation through constructor or setter injection provides better encapsulation and promotes better code readability.

2. Testability: Field injection makes it difficult to write unit tests for the class because the dependencies are directly injected into the fields. In order to mock or substitute dependencies during testing, you would need to use reflection or other techniques to modify the private fields. With constructor or setter injection, you can easily provide mock dependencies for testing purposes.

3. Dependency Hiding: With field injection, the dependencies are hidden within the class, and it's not immediately clear what dependencies are required by the class. This can make it harder for developers to understand the class's dependencies and can lead to confusion or errors when working with the codebase. Constructor or setter injection makes the dependencies explicit and easier to understand.

4. Circular Dependencies: Field injection can lead to circular dependencies, where two or more classes depend on each other directly or indirectly through their fields. Circular dependencies can create runtime errors and make it harder to reason about the flow of your application. Constructor injection helps to avoid circular dependencies by forcing you to explicitly define the dependencies and their order of instantiation.

5. Immutability: Field injection does not support immutability, as the dependencies are directly assigned to the fields. Immutability is a desirable characteristic in software design as it promotes thread safety and helps prevent unintended side effects. Constructor injection, on the other hand, allows you to create immutable objects by initializing the dependencies in the constructor and making them final.

Overall, constructor or setter injection is considered a better practice in Spring Boot applications as it promotes encapsulation, testability, and explicit dependency management, while also helping to prevent circular dependencies and supporting immutability.

## What is @Lazy in spring boot constructor injection ?

In Spring Boot, the `@Lazy` annotation is used in conjunction with constructor injection to indicate that a dependency should be lazily initialized. Lazy initialization means that the dependency will be created only when it is first requested, rather than being eagerly created at the time the containing bean is instantiated.

By default, Spring performs eager initialization, where all dependencies of a bean are created when the containing bean is created. However, in some cases, you may have dependencies that are not always needed or have a significant initialization cost. In such scenarios, you can use `@Lazy` to defer the creation of those dependencies until they are actually required.

Here's an example of using `@Lazy` in constructor injection:

```java
@Service
public class MyService {
    private final MyRepository myRepository;

    @Autowired
    public MyService(@Lazy MyRepository myRepository) {
        this.myRepository = myRepository;
    }
}
```

In the above example, the `MyRepository` dependency is marked with `@Lazy`. This means that the `MyRepository` bean will not be created when the `MyService` bean is instantiated. Instead, it will be created only when it is first accessed or requested by the `MyService` bean.

Using `@Lazy` can help improve the performance of your application by avoiding the unnecessary creation of dependencies that may not be used during the entire lifecycle of the bean. It can be particularly useful when dealing with dependencies that have resource-intensive initialization processes or when you have circular dependencies that would otherwise cause issues with eager initialization.

It's important to note that `@Lazy` is not limited to constructor injection and can also be used with other types of injection, such as setter injection or field injection.

## Which factor impact to how many request spring booot can handle at once time ?
Several factors can impact how many requests a Spring Boot application can handle simultaneously. Here are some key factors to consider:

1. Thread pool configuration: The thread pool configuration of the underlying servlet container, such as Tomcat, Jetty, or Undertow, plays a significant role. The thread pool determines the number of threads available to handle incoming requests. By adjusting the thread pool size, you can control the concurrency level of your application. Configuring an appropriate thread pool size based on your application's workload and available system resources is crucial.

2. Hardware resources: The available hardware resources, including CPU, memory, and network bandwidth, influence the application's capacity to handle concurrent requests. A server with a higher number of CPU cores and sufficient memory can handle more concurrent requests efficiently. It's important to monitor resource utilization during load testing to ensure that the application is not overwhelmed by resource constraints.

3. Application design and architecture: The design and architecture of your Spring Boot application can impact its concurrency capabilities. An application that is well-optimized, follows best practices, and utilizes asynchronous and non-blocking programming models can handle more concurrent requests with fewer threads. Leveraging reactive programming with libraries like Spring WebFlux or implementing asynchronous processing can improve the scalability and responsiveness of your application.

4. Blocking operations: The presence of blocking operations within your application can limit its concurrency capabilities. If your application performs blocking operations such as synchronous I/O or long-running computations, it can tie up threads and reduce the number of requests that can be processed concurrently. It's important to identify blocking operations and consider alternatives like asynchronous I/O or offloading blocking tasks to separate threads or thread pools.

5. Network latency and external dependencies: The response time of external services or dependencies that your application interacts with can impact its concurrency. If your application heavily relies on external services with high latency, it may increase the time spent waiting for responses, which can affect the number of concurrent requests that can be handled.

6. Workload characteristics: The nature of the workload your application experiences, including the rate of incoming requests and their processing time, affects its concurrency. A high rate of incoming requests or requests with long processing times can put more strain on the application, potentially reducing the number of concurrent requests it can handle effectively.

It's important to consider these factors and perform load testing under realistic conditions to determine the optimal configuration and capacity of your Spring Boot application. Monitoring the application's performance and resource utilization during load testing can help identify bottlenecks and optimize the application's concurrency capabilities.

