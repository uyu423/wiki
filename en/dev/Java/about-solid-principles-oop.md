---
title: SOLID Principles for Object-Oriented Programming
description: 
published: true
date: 2023-02-17T18:00:28.506Z
tags: java, oop
editor: markdown
dateCreated: 2022-12-24T21:41:54.164Z
---

- [객체지향 프로그래밍의 SOLID 원칙***Korean** version of this document is available*](/ko/dev/Java/about-solid-principles-oop)
{.links-list}

![solid-logo.png](/solid-logo.png =700x){.align-center}

## What is SOLID principles?

- SOLID is a set of five principles for object-oriented programming and design that was introduced by **Robert C. Martin.**

> **About Robert C. Martin.**
> 
> a.k.a "Uncle Bob," is a software engineer, author, and speaker who is well known for his work on software design and development. He is the author of numerous books and articles on software development, including the popular book "Clean Code: A Handbook of Agile Software Craftsmanship," which is a guide to writing clean and maintainable code. **He is also the creator of the SOLID principles**, which are a set of principles for designing maintainable and scalable software systems.
> 
> Martin is a strong advocate for agile software development practices, and he is a co-author of the Agile Manifesto. He has spoken at numerous conferences and workshops around the world, and he has also served as a mentor and coach to many software developers. Martin is highly respected in the software development community, and his work has had a significant impact on the way that software is developed and maintained.
> 

- The acronym **SOLID** stands for the following five principles:
  1. **Single Responsibility Principle (SRP)**: A class should have only one reason to change.
  1. **Open-Closed Principle (OCP)**: Software entities (classes, modules, functions, etc.) should be open for extension but closed for modification.
  1. **Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types.
  1. **Interface Segregation Principle (ISP)**: Clients should not be forced to depend on interfaces they do not use.
  1. **Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

- Let's take a closer look at each principle.

### Single Responsibility Principle (SRP)
- The Single Responsibility Principle states that a class should have only one reason to change. This means that a class should have a single, well-defined responsibility and should not be responsible for multiple things.

- Adhering to the Single Responsibility Principle can help you write code that is easier to maintain and test, because changes to the class are isolated to a single responsibility. It can also help you avoid code duplication and improve the modularity of your software.

- here is a simple Java code example that violates the SRP:

```java
public class Employee {
  private String name;
  private int age;
  private double salary;
  private String address;

  public Employee(String name, int age, double salary, String address) {
    this.name = name;
    this.age = age;
    this.salary = salary;
    this.address = address;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    this.age = age;
  }

  public double getSalary() {
    return salary;
  }

  public void setSalary(double salary) {
    this.salary = salary;
  }

  public String getAddress() {
    return address;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public void calculateTax() {
    // calculate tax based on salary and age
  }

  public void sendEmail() {
    // send email to employee's address
  }
}
```

- In this example, the `Employee` class violates the SRP because it has multiple responsibilities: it holds employee information (`name`, `age`, `salary`, and `address`) and it also calculates taxes and sends emails. A class should have only one responsibility, so this class should be split into two separate classes: one for holding employee information and another for calculating taxes and sending emails.

- Here is a simple Java code example that adheres to the SRP:

```java
public class Employee {
  private String name;
  private int age;
  private double salary;
  private String address;

  public Employee(String name, int age, double salary, String address) {
    this.name = name;
    this.age = age;
    this.salary = salary;
    this.address = address;
  }

  public String getName() {
    return name;
  }

  public void setName(String name) {
    this.name = name;
  }

  public int getAge() {
    return age;
  }

  public void setAge(int age) {
    this.age = age;
  }

  public double getSalary() {
    return salary;
  }

  public void setSalary(double salary) {
    this.salary = salary;
  }

  public String getAddress() {
    return address;
  }

  public void setAddress(String address) {
    this.address = address;
  }
}

public class TaxCalculator {
  public double calculateTax(Employee e) {
    // calculate tax based on salary and age
  }
}

public class EmailSender {
  public void sendEmail(Employee e) {
    // send email to employee's address
  }
}
```

- In this example, each class has a single responsibility. The `Employee` class is responsible for holding employee information, the `TaxCalculator` class is responsible for calculating taxes, and the `EmailSender` class is responsible for sending emails. This adheres to the SRP because each class has only one responsibility, and therefore only one reason to change. If we need to make a change to the way taxes are calculated, we can do so in the `TaxCalculator` class without affecting the other classes. Similarly, if we need to change the way emails are sent, we can do so in the `EmailSender` class without affecting the other classes.


### Open-Closed Principle (OCP)

- The Open-Closed Principle states that a class should be open for extension but closed for modification. This means that you should be able to add new functionality to a class without changing its existing code.

- Adhering to the Open-Closed Principle can help you write code that is more flexible and easier to maintain, because you can add new features without breaking existing functionality. It can also help you reduce the risk of introducing bugs when modifying existing code.

- here is a simple Java code example that violates the OCP:

```java
public class Rectangle {
  private int width;
  private int height;

  public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
  }

  public int getArea() {
    return width * height;
  }
}

public class Square extends Rectangle {
  public Square(int side) {
    super(side, side);
  }
}

public class AreaCalculator {
  public int calculateArea(Rectangle r) {
    if (r instanceof Square) {
      Square s = (Square) r;
      return s.getSideLength() * s.getSideLength();
    } else {
      return r.getWidth() * r.getHeight();
    }
  }
}
```

- In this example, the `AreaCalculator` class violates the OCP because it has been modified to handle a new type of shape (squares). If we want to add a new type of shape, we would need to modify the `AreaCalculator` class again, which goes against the OCP.

- Here is a simple Java code example that adheres to the OCP:

```java
public interface Shape {
  int getArea();
}

public class Rectangle implements Shape {
  private int width;
  private int height;

  public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
  }

  @Override
  public int getArea() {
    return width * height;
  }
}

public class Square implements Shape {
  private int sideLength;

  public Square(int sideLength) {
    this.sideLength = sideLength;
  }

  @Override
  public int getArea() {
    return sideLength * sideLength;
  }
}

public class AreaCalculator {
  public int calculateArea(Shape s) {
    return s.getArea();
  }
}
```

- In this example, the `AreaCalculator` class adheres to the OCP because it does not need to be modified to handle new types of shapes. We can simply create a new class that implements the `Shape` interface and pass it to the `calculateArea` method. The `calculateArea` method will work for any shape that implements the `Shape` interface, without the need to modify the method itself.


### Liskov Substitution Principle (LSP)

- The Liskov Substitution Principle states that subtypes should be substitutable for their base types. This means that if a class is a subtype of another class, it should be able to be used in the same way as the base class without affecting the correctness of the program.

- Adhering to the Liskov Substitution Principle can help you write code that is more flexible and easier to maintain, because you can use subtypes in the same way as the base type without worrying about unintended side effects. It can also help you write code that is easier to understand, because you know that subtypes can be used in the same way as the base type.

- here is a simple Java code example that violates the LSP:

```java
public class Rectangle {
  protected int width;
  protected int height;

  public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
  }

  public int getWidth() {
    return width;
  }

  public void setWidth(int width) {
    this.width = width;
  }

  public int getHeight() {
    return height;
  }

  public void setHeight(int height) {
    this.height = height;
  }

  public int getArea() {
    return width * height;
  }
}

public class Square extends Rectangle {
  public Square(int sideLength) {
    super(sideLength, sideLength);
  }

  @Override
  public void setWidth(int width) {
    super.setWidth(width);
    super.setHeight(width);
  }

  @Override
  public void setHeight(int height) {
    super.setHeight(height);
    super.setWidth(height);
  }
}

public class AreaCalculator {
  public int calculateArea(Rectangle r) {
    return r.getWidth() * r.getHeight();
  }
}
```

- In this example, the `Square` class violates the LSP because it does not behave in the same way as a `Rectangle`. The `AreaCalculator` class expects a `Rectangle` object to have a `setWidth` and `setHeight` method that allows the width and height to be set independently, but the `Square` class does not allow this. Instead, setting the width or height of a `Square` object also sets the other dimension, which goes against the behavior of a `Rectangle`. This means that a `Square` object is not a valid substitute for a `Rectangle` object, which violates the LSP.

- Here is a simple Java code example that adheres to the LSP:

```java
public interface Shape {
  int getArea();
  int getWidth();
  void setWidth(int width);
  int getHeight();
  void setHeight(int height);
}

public class Rectangle implements Shape {
  private int width;
  private int height;

  public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
  }

  @Override
  public int getWidth() {
    return width;
  }

  @Override
  public void setWidth(int width) {
    this.width = width;
  }

  @Override
  public int getHeight() {
    return height;
  }

  @Override
  public void setHeight(int height) {
    this.height = height;
  }

  @Override
  public int getArea() {
    return width * height;
  }
}

public class Square implements Shape {
  private int sideLength;

  public Square(int sideLength) {
    this.sideLength = sideLength;
  }

  @Override
  public int getWidth() {
    return sideLength;
  }

  @Override
  public void setWidth(int width) {
    this.sideLength = width;
  }

  @Override
  public int getHeight() {
    return sideLength;
  }

  @Override
  public void setHeight(int height) {
    this.sideLength = height;
  }

  @Override
  public int getArea() {
    return sideLength * sideLength;
  }
}

public class AreaCalculator {
  public int calculateArea(Shape s) {
    return s.getWidth() * s.getHeight();
  }
}
```

- In this example, the `Square` class adheres to the LSP because it behaves in the same way as a `Rectangle`. Both classes implement the `Shape` interface, which defines the behavior that is expected of a shape. The `Square` class correctly implements all of the methods defined in the `Shape` interface, so it can be used as a substitute for a `Rectangle` object. The `AreaCalculator` class can use either a `Rectangle` or a `Square` object without knowing the specific type, because both types adhere to the behavior defined in the `Shape` interface. This adheres to the LSP because a subclass should be able to be used in the same way as its superclass, without the need to modify the code that uses the superclass.

### Interface Segregation Principle (ISP)

- The Interface Segregation Principle states that clients should not be forced to depend on interfaces they do not use. This means that you should create small, specific interfaces rather than large, general ones.

- Adhering to the Interface Segregation Principle can help you write code that is more flexible and easier to understand, because you can create specialized interfaces that are easier to implement and use. It can also help you avoid unnecessary dependencies and improve the modularity of your software.

- Here is a simple Java code example that violates the ISP:

```java
public interface Shape {
  int getArea();
  int getWidth();
  void setWidth(int width);
  int getHeight();
  void setHeight(int height);
  String getColor();
  void setColor(String color);
}

public class Rectangle implements Shape {
  private int width;
  private int height;
  private String color;

  public Rectangle(int width, int height, String color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }

  @Override
  public int getWidth() {
    return width;
  }

  @Override
  public void setWidth(int width) {
    this.width = width;
  }

  @Override
  public int getHeight() {
    return height;
  }

  @Override
  public void setHeight(int height) {
    this.height = height;
  }

  @Override
  public String getColor() {
    return color;
  }

  @Override
  public void setColor(String color) {
    this.color = color;
  }

  @Override
  public int getArea() {
    return width * height;
  }
}
```

- In this example, the `Rectangle` class implements the `Shape` interface, which defines the behavior that is expected of a shape. However, the `Shape` interface violates the ISP because it has methods that are not applicable to all types of shapes. The `getColor` and `setColor` methods, for example, do not make sense for a rectangle because it does not have a color in the same way that a circle does. This means that the `Rectangle` class is forced to implement methods that it does not need, which violates the ISP.

- Here is a simple Java code example that adheres to the ISP:

```java
public interface Shape {
  int getArea();
  int getWidth();
  void setWidth(int width);
  int getHeight();
  void setHeight(int height);
}

public interface ColoredShape extends Shape {
  String getColor();
  void setColor(String color);
}

public class Rectangle implements Shape {
  private int width;
  private int height;

  public Rectangle(int width, int height) {
    this.width = width;
    this.height = height;
  }

  @Override
  public int getWidth() {
    return width;
  }

  @Override
  public void setWidth(int width) {
    this.width = width;
  }

  @Override
  public int getHeight() {
    return height;
  }

  @Override
  public void setHeight(int height) {
    this.height = height;
  }

  @Override
  public int getArea() {
    return width * height;
  }
}

public class ColoredRectangle implements ColoredShape {
  private int width;
  private int height;
  private String color;

  public ColoredRectangle(int width, int height, String color) {
    this.width = width;
    this.height = height;
    this.color = color;
  }

  @Override
  public int getWidth() {
    return width;
  }

  @Override
  public void setWidth(int width) {
    this.width = width;
  }

  @Override
  public int getHeight() {
    return height;
  }

  @Override
  public void setHeight(int height) {
    this.height = height;
  }

  @Override
  public String getColor() {
    return color;
  }

  @Override
  public void setColor(String color) {
    this.color = color;
  }

  @Override
  public int getArea() {
    return width * height;
  }
}
```

- In this example, the `Rectangle` class implements the `Shape` interface, which defines the behavior that is expected of a shape. The `ColoredRectangle` class extends the `Rectangle` class and also implements the `ColoredShape` interface, which adds the ability to set and get a color. This adheres to the ISP because each interface defines a specific set of behaviors, and a class only needs to implement the interfaces that are relevant to its specific needs. This allows us to create classes that have only the behaviors that they need, without being forced to implement unnecessary methods.

### Dependency Inversion Principle (DIP)

- Dependency Inversion Principle (DIP) states that high-level modules should not depend on low-level modules, but rather both should depend on abstractions. This means that you should depend on abstractions (such as interfaces or abstract classes) rather than on concrete implementations when writing code.

- Adhering to the Dependency Inversion Principle can help you write code that is more flexible and easier to maintain, because you can change the concrete implementation of a dependency without affecting the code that depends on it. It can also help you improve the modularity of your software, because high-level modules are not tightly coupled to low-level ones.

- here is a simple Java code example that violates the DIP:

```java
public class User {
  private String username;
  private String password;

  public User(String username, String password) {
    this.username = username;
    this.password = password;
  }

  public String getUsername() {
    return username;
  }

  public void setUsername(String username) {
    this.username = username;
  }

  public String getPassword() {
    return password;
  }

  public void setPassword(String password) {
    this.password = password;
  }
}

public class UserService {
  public void authenticateUser(User user) {
    // authenticate the user
  }
}

public class Application {
  public static void main(String[] args) {
    UserService userService = new UserService();
    User user = new User("john.doe", "password123");
    userService.authenticateUser(user);
  }
}
```

- In this example, the `Application` class violates the DIP because it depends on the `UserService` class and the `User` class. This means that if either of these classes needs to be changed or replaced, the `Application` class will also need to be changed. This makes the `Application` class more difficult to maintain and test, because it is dependent on other classes.

- Here is a simple Java code example that adheres to the DIP:

```java
public interface UserRepository {
  User findByUsername(String username);
  void saveUser(User user);
}

public class InMemoryUserRepository implements UserRepository {
  private Map<String, User> users;

  public InMemoryUserRepository() {
    this.users = new HashMap<>();
  }

  @Override
  public User findByUsername(String username) {
    return users.get(username);
  }

  @Override
  public void saveUser(User user) {
    users.put(user.getUsername(), user);
  }
}

public interface UserAuthenticationService {
  boolean authenticate(String username, String password);
}

public class UserAuthenticationServiceImpl implements UserAuthenticationService {
  private UserRepository userRepository;

  public UserAuthenticationServiceImpl(UserRepository userRepository) {
    this.userRepository = userRepository;
  }

  @Override
  public boolean authenticate(String username, String password) {
    User user = userRepository.findByUsername(username);
    if (user == null) {
      return false;
    }
    return user.getPassword().equals(password);
  }
}

public class Application {
  public static void main(String[] args) {
    UserRepository userRepository = new InMemoryUserRepository();
    UserAuthenticationService authenticationService = 
        new UserAuthenticationServiceImpl(userRepository);
    User user = new User("john.doe", "password123");
    userRepository.saveUser(user);
    boolean authenticated = authenticationService.authenticate("john.doe", "password123");
    System.out.println(authenticated);
  }
}
```

- In this example, the `Application` class adheres to the DIP because it depends on abstractions (interfaces) rather than concrete implementations. The `Application` class depends on the `UserAuthenticationService` interface, which is implemented by the `UserAuthenticationServiceImpl` class. The `UserAuthenticationServiceImpl` class depends on the `UserRepository` interface, which is implemented by the `InMemoryUserRepository` class. This means that if the implementation of any of these classes needs to be changed, the `Application` class will not be affected, as long as the interface is maintained. This makes the `Application` class more flexible and easier to maintain because it is not tightly coupled to specific implementations.

## Advantages to following the SOLID principles

There are several advantages to following the SOLID principles when programming:

### Improved flexibility

- Adhering to the SOLID principles can help you write code that is more flexible and easier to change, because you can add new features without breaking existing functionality, and you can use abstractions rather than concrete implementations to reduce the coupling between different parts of your code.

### Increased reusability

- Adhering to the SOLID principles can help you write code that is more reusable, because you can design classes and interfaces that are focused on a single responsibility and can be easily used in different contexts.

### Better code organization

- Adhering to the SOLID principles can help you write code that is easier to understand and maintain, because you can organize your code into small, modular components that are easy to understand and test.

### Reduced risk of introducing bugs

- Adhering to the SOLID principles can help you reduce the risk of introducing bugs when modifying your code, because you can add new features without modifying existing code and you can use abstractions rather than concrete implementations to reduce the coupling between different parts of your code.

Overall, following the SOLID principles can help you write code that is more flexible, reusable, and easy to understand, which can make it easier to maintain and extend over time.