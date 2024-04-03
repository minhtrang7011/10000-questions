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

