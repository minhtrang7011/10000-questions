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
