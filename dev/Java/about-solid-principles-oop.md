---
title: 객체지향 프로그래밍의 SOLID 원칙에 대해
description: 
published: true
date: 2022-12-24T22:52:16.086Z
tags: java, oop
editor: markdown
dateCreated: 2022-12-24T22:39:17.183Z
---

- [About the SOLID Principles for Object-Oriented Programming***English** version of this document is available*](/en/dev/Java/about-solid-principles-oop)
{.links-list}

# TBU (To Be Updated)

## SOLID 원칙?

- SOLID는 **Robert C. Martin**이 소개한 객체 지향 프로그래밍 및 설계를 위한 5가지 원칙입니다.

> **Robert C. Martin ?**
>
> a.k.a "Uncle Bob" 소프트웨어 설계 및 개발로 잘 알려진 소프트웨어 엔지니어, 저자 및 연사입니다. 그는 깨끗하고 유지 보수 가능한 코드를 작성하는 방법을 안내하는 "Clean Code: A Handbook of Agile Software Craftsmanship"을 포함하여 소프트웨어 개발에 관한 수많은 책과 아티클의 저자입니다. 그는 **유지 관리 및 확장 가능한 소프트웨어 시스템을 설계하기 위한 일련의 원칙인 SOLID 원칙의 창시자**이기도 합니다.
>
> Martin은 애자일 소프트웨어 개발 방법론을 강력하게 옹호하며 Agile Manifesto의 공동 저자입니다. 그는 전 세계의 수많은 컨퍼런스와 워크숍에서 연설했으며 많은 소프트웨어 개발자의 멘토이자 코치로도 활동했습니다. Martin은 소프트웨어 개발 커뮤니티에서 높은 평가를 받고 있으며 그의 작업은 소프트웨어 개발 및 유지 관리 방법에 상당한 영향을 미쳤습니다.
>

- **SOLID**라는 약어는 다음 다섯 가지 원칙을 나타냅니다.
   1. **단일 책임 원칙(SRP)**: 하나의 클래스는 하나의 책임만을 가져야 한다.
   1. **개방-폐쇄 원칙(OCP)**: 소프트웨어 요소는 확장에는 열려 있지만 수정에는 닫혀 있어야한 다.
   1. **리스코프 치환 원칙(LSP)**: 상위 타입의 인스턴스는 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야한다.
   1. **인터페이스 분리 원칙(ISP)**: 클라이언트가 사용하지 않는 인터페이스에 의존하도록 강요해서는 안된다. 특정 클라이언트를 위한 여러 개의 인터페이스가 한 개의 범용 인터페이스 보다 낫다.
   1. **의존관계 역전 원칙(DIP)**: 고수준 모듈은 저수준 모듈에 의존해서는 안된다.구체화에 의존하지 않고, 추상화에 의존해야 한다.

- 각 원칙에 대해 자세히 살펴보겠습니다.

### 단일 책임 원칙 (SRP)

- 단일 책임 원칙(Single Responsibility Principle)에 따르면 하나의 클래스는 변경해야 할 이유가 하나만 있어야 합니다. 이것은 클래스가 하나의 잘 정의된 책임만을 가져야 하며 여러 가지를 책임지지 않아야 함을 의미합니다.

- 단일 책임 원칙을 준수하면 클래스에 대한 변경 사항이 단일 책임으로 격리되기 때문에 유지 관리 및 테스트가 더 쉬운 코드를 작성하는 데 도움이 될 수 있습니다. 또한 코드 중복을 방지하고 소프트웨어의 모듈성을 개선하는 데 도움이 될 수 있습니다.

- 다음은 SRP를 위반하는 간단한 Java 코드 예제입니다.

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

- 이 예에서 `Employee` 클래스는 직원 정보(`name`, `age`, `salary` 및 `address`)를 보유하고 세금을 계산하거나 이메일을 보내는 등 여러 가지 책임이 있기 때문에 SRP를 위반합니다. 클래스는 하나의 책임만 가져야 하므로 이 클래스는 두 개의 별도 클래스로 분리되어야 합니다. 하나는 직원 정보를 보관하고 다른 하나는 세금을 계산하고 이메일을 보내는 것입니다.

- 다음은 SRP를 준수하는 간단한 Java 코드 예제입니다.

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

- 이 예에서 각 클래스는 단일 책임만을 가집니다. `Employee` 클래스는 직원 정보를 가지고 있고 `TaxCalculator` 클래스는 세금 계산을 담당하며 `EmailSender` 클래스는 이메일 전송을 담당합니다. 이것은 각 클래스가 하나의 책임만 가지고 있으므로 변경해야 할 이유가 하나이기 때문에 SRP를 준수합니다. 세금 계산 방식을 변경해야 하는 경우 다른 클래스에 영향을 주지 않고 `TaxCalculator` 클래스를 변경하면 됩니다. 마찬가지로 이메일 전송 방식을 변경해야 하는 경우 다른 클래스에 영향을 주지 않고 `EmailSender` 클래스를 변경하면 됩니다.


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