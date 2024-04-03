## What is SOLID principle

The SOLID principles are a set of five design principles that help in creating software that is easy to understand, maintain, and extend. These principles were introduced by Robert C. Martin (also known as Uncle Bob) and are widely regarded as best practices in software development. Each principle focuses on a specific aspect of software design and promotes loose coupling, high cohesion, and flexibility. The SOLID principles are as follows:

1. Single Responsibility Principle (SRP): A class should have only one reason to change. It states that a class should have a single responsibility or job. By keeping classes focused on a specific task, you can minimize the impact of changes and make the code easier to understand and maintain.

2. Open-Closed Principle (OCP): Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. This principle encourages designing modules that are easily extendable without modifying the existing code. Instead of changing the existing code, you should be able to add new functionality through inheritance, composition, or interfaces.

3. Liskov Substitution Principle (LSP): Subtypes must be substitutable for their base types. This principle emphasizes the importance of maintaining the behavior and contracts of the base class when creating derived classes. Subclasses should be able to be used in place of their base class without affecting the correctness of the program.

4. Interface Segregation Principle (ISP): Clients should not be forced to depend on interfaces they do not use. ISP encourages the creation of specific and focused interfaces rather than having large, monolithic interfaces. Clients should only depend on the interfaces that are relevant to them, reducing the impact of changes and promoting flexibility.

5. Dependency Inversion Principle (DIP): High-level modules should not depend on low-level modules. Both should depend on abstractions. DIP promotes loose coupling by advocating the use of abstractions (interfaces or abstract classes) to define dependencies. This allows for flexibility and easier testing, as dependencies can be easily substituted with different implementations.

By adhering to the SOLID principles, you can create software that is modular, extensible, and easier to maintain and evolve over time. These principles help in reducing code smells, improving code quality, and promoting good software design practices.

Examples illustrating each of the SOLID principles:

1. Single Responsibility Principle (SRP):
```java
public class Customer {
    private String name;
    private String email;

    public void setName(String name) {
        // Setter logic
    }

    public void setEmail(String email) {
        // Setter logic
    }

    public void save() {
        // Logic to save customer to the database
    }

    public void sendEmail() {
        // Logic to send an email to the customer
    }
}
```
In this example, the `Customer` class violates the SRP because it has multiple responsibilities: storing customer data and sending emails. It would be better to separate these responsibilities into different classes, such as `CustomerRepository` for database operations and `EmailService` for sending emails.

2. Open-Closed Principle (OCP):
```java
public abstract class Shape {
    public abstract double calculateArea();
}

public class Rectangle extends Shape {
    private double width;
    private double height;

    public double calculateArea() {
        return width * height;
    }
}

public class Circle extends Shape {
    private double radius;

    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}
```
In this example, the `Shape` class and its subclasses demonstrate adherence to the OCP. The `Shape` class defines an abstract method `calculateArea()`, which is implemented by its subclasses. New shapes can be added by creating new subclasses without modifying the existing code.

3. Liskov Substitution Principle (LSP):
```java
public class Rectangle {
    protected double width;
    protected double height;

    public void setWidth(double width) {
        this.width = width;
    }

    public void setHeight(double height) {
        this.height = height;
    }

    public double calculateArea() {
        return width * height;
    }
}

public class Square extends Rectangle {
    @Override
    public void setWidth(double width) {
        this.width = width;
        this.height = width;
    }

    @Override
    public void setHeight(double height) {
        this.height = height;
        this.width = height;
    }
}
```
This example violates the LSP. Although a `Square` is a specific type of `Rectangle`, the behavior of the `Square` class does not conform to the behavior expected from the `Rectangle` class. Changing the width of a `Square` should not automatically change its height, as it does in the `Square` class. This violates the substitutability principle, as substituting a `Square` for a `Rectangle` would lead to unexpected behavior.

4. Interface Segregation Principle (ISP):
```java
public interface Printer {
    void print();
    void scan();
    void fax();
}

public class SimplePrinter implements Printer {
    public void print() {
        // Print logic
    }

    public void scan() {
        // Scan logic
    }

    public void fax() {
        // Fax logic
    }
}

public class AdvancedPrinter implements Printer {
    public void print() {
        // Print logic
    }

    public void scan() {
        // Scan logic
    }

    public void fax() {
        // Fax logic
    }

    public void photocopy() {
        // Photocopy logic
    }
}
```
In this example, the `Printer` interface violates the ISP because it includes methods like `fax()` and `scan()` that might not be relevant for all implementations. Instead, the interface could be split into smaller, more focused interfaces, such as `Printable`, `Scannable`, and `Faxable`, allowing clients to depend only on the interfaces they need.

5. Dependency Inversion Principle (DIP):
```java
public interface MessageSender {
    void sendMessage(String message);
}

public class EmailSender implements MessageSender {
    public void sendMessage(String message) {
        // Logic to send an email
    }
}

public class SMSsender implements MessageSender {
    public void sendMessage(String message) {
        // Logic to send an SMS
    }
}

public class NotificationService {
    private MessageSender messageSender;

    public NotificationService(MessageSender messageSender) {
        this.messageSender = messageSender;
    }

    public void sendNotification(String message) {
        messageSender.sendMessage(message);
    }
}
```
In this example, the `NotificationService` depends on the `MessageSender` interface instead of concrete implementations like `EmailSender` or `SMSsender`. This promotes loose coupling, and the actual implementation can be easily changed by providing a different implementation of `MessageSender` without modifying the `NotificationService` class.

These examples showcase how the SOLID principles can guide the design and structure of your code to achieve maintainable, flexible, and modular software.
