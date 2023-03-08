---
title: 객체지향 프로그래밍의 SOLID 원칙
description: 
published: true
date: 2023-02-17T18:00:29.955Z
tags: java, oop
editor: markdown
dateCreated: 2022-12-24T22:39:17.183Z
---

- [SOLID Principles for Object-Oriented Programming***English** version of this document is available*](/en/dev/Java/about-solid-principles-oop)
{.links-list}

![solid-logo.png](/solid-logo.png =700x){.align-center}

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

  // getters and setters

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

  // getters and setters
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


### 개방-폐쇄 원칙 (OCP)

- 개방-폐쇄 원칙(Open-Closed Principle)이란 클래스는 확장에는 열려 있어야 하지만 수정에는 닫혀 있어야 한다는 것입니다. 즉, 기존 코드를 변경하지 않고도 클래스에 새 기능을 추가할 수 있어야 합니다.

- 개방-폐쇄 원칙을 준수하면 기존 기능을 중단하지 않고 새로운 기능을 추가할 수 있기 때문에 더 유연하고 유지 관리하기 쉬운 코드를 작성할 수 있습니다. 또한 기존 코드를 수정할 때 버그가 발생할 위험을 줄이는 데 도움이 될 수 있습니다.

- 다음은 OCP를 위반하는 간단한 Java 코드 예제입니다.

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
- 이 예에서 `AreaCalculator` 클래스는 새로운 유형의 모양(사각형)을 처리하도록 수정되었기 때문에 OCP를 위반합니다. 새로운 유형의 도형을 추가하려면 `AreaCalculator` 클래스를 다시 수정해야하고, 또 다시 OCP를 위반합니다.

- 다음은 OCP를 준수하는 간단한 Java 코드 예제입니다.

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

- 새로운 유형의 도형을 처리하기 위해 `AreaCalculator` 클래스를 수정할 필요가 없기 때문에 OCP를 준수합니다. `Shape` 인터페이스를 구현하는 새 클래스를 만들고 `calculateArea` 메서드에 전달합니다. `calculateArea` 메서드는 메서드 자체를 수정할 필요 없이 `Shape` 인터페이스를 구현하는 모든 도형에 대해 작동합니다.

### 리스코프 치환 원칙 (LSP)

- 리스코프 치환 원칙(Liskov Substitution Principle)에 따르면 하위 타입은 상위 타입을 대체할 수 있어야 합니다. 즉, 클래스가 다른 클래스의 하위 타입인 경우 프로그램의 정확성에 영향을 주지 않고 상위 클래스와 동일한 방식으로 사용할 수 있어야 합니다.

- 리스코프 치환 원칙을 준수하면 의도하지 않은 사이드 이펙트에 대한 걱정 없이 상위 타입과 동일한 방식으로 하위 타입을 사용할 수 있으므로 더 유연하고 유지 관리하기 쉬운 코드를 작성할 수 있습니다. 또한 상위 타입과 동일한 방식으로 하위 타입을 사용할 수 있다는 것을 알고 있기 때문에 이해하기 쉬운 코드를 작성하는 데 도움이 될 수 있습니다.

- 다음은 LSP를 위반하는 간단한 Java 코드 예제입니다.

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

- 이 예에서 `Square` 클래스는 `Rectangle`과 동일한 방식으로 동작하지 않기 때문에 LSP를 위반합니다. `AreaCalculator` 클래스는 `Rectangle` 객체가 너비와 높이를 독립적으로 설정할 수 있는 `setWidth` 및 `setHeight` 메서드를 가질 것으로 예상하지만 `Square` 클래스는 이를 허용하지 않습니다. 대신 `Square` 객체의 너비 또는 높이를 설정하면 `Rectangle`의 다른 값도 변경됩니다. 이것은 `Square` 객체가 `Rectangle` 객체의 유효한 대체 타입이 아님을 의미합니다.

- 다음은 LSP를 준수하는 간단한 Java 코드 예제입니다.

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

- 이 예에서 `Square` 클래스는 `Rectangle`과 동일한 방식으로 동작하기 때문에 LSP를 준수합니다. 두 클래스 모두 모양에 대해 예상되는 동작을 정의하는 `Shape` 인터페이스를 구현합니다. `Square` 클래스는 `Shape` 인터페이스에 정의된 모든 메서드를 올바르게 구현하므로 `Rectangle` 객체의 대체 타입으로 사용할 수 있습니다. `AreaCalculator` 클래스는 특정 타입을 몰라도 `Rectangle` 또는 `Square` 개체를 사용할 수 있습니다. 두 타입 모두 `Shape` 인터페이스에 정의된 동작을 준수하기 때문입니다. 하위 클래스는 상위 클래스를 사용하는 코드를 수정할 필요 없이 상위 클래스와 동일한 방식으로 사용할 수 있어야 하므로 LSP를 준수합니다.

### 인터페이스 분리 원칙 (ISP)

- 인터페이스 분리 원칙(Interface Segregation Principle)에 따르면 클라이언트는 사용하지 않는 인터페이스에 강제로 의존해서는 안 됩니다. 즉, 크고 범용적인 인터페이스를 만드는 것이 아닌 작고 구체적인 인터페이스를 만들어야 함을 의미합니다.

- 인터페이스 분리 원칙을 준수하면 더 쉽게 구현하고 사용할 수 있는 특수 인터페이스를 만들 수 있으므로 더 유연하고 이해하기 쉬운 코드를 작성할 수 있습니다. 또한 불필요한 종속성을 피하고 소프트웨어의 모듈성을 개선하는 데 도움이 될 수 있습니다.

- 다음은 ISP를 위반하는 간단한 Java 코드 예제입니다.


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

- 이 예에서 `Rectangle` 클래스는 모양에 대해 예상되는 동작을 정의하는 `Shape` 인터페이스를 구현합니다. 그러나 `Shape` 인터페이스는 모든 유형의 도형에 적용할 수 없는 메소드를 가지고 있기 때문에 ISP를 위반합니다. 예를 들어 `getColor` 및 `setColor` 메서드는 색상이 없는 사각형에 적합하지 않습니다. 이는 `Rectangle` 클래스가 필요하지 않은 메서드를 강제로 구현하도록 하여 ISP를 위반하는 것을 의미합니다.

- 다음은 ISP를 준수하는 간단한 Java 코드 예제입니다.


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

- 이 예에서 `Rectangle` 클래스는 모양에 대해 예상되는 동작을 정의하는 `Shape` 인터페이스를 구현합니다. `ColoredRectangle` 클래스는 `Rectangle` 클래스를 확장하고 색상을 설정하고 가져오는 기능을 추가하는 `ColoredShape` 인터페이스도 구현합니다. 이는 각 인터페이스가 특정 동작 집합을 정의하고 클래스는 특정 요구 사항과 관련된 인터페이스만 구현하면 되므로 ISP를 준수합니다. 이를 통해 불필요한 메서드를 강제로 구현하지 않고 필요한 동작만 있는 클래스를 만들 수 있습니다.


### 의존관계 역전 원칙 (DIP)

- 의존관계 역전 원칙(Dependency Inversion Principle)는 상위 수준 모듈이 하위 수준 모듈에 의존해서는 안 되며 둘 다 추상화에 의존해야 한다고 명시합니다. 즉, 코드를 작성할 때 구체적인 구현보다는 추상화(예: 인터페이스 또는 추상 클래스)에 의존해야 합니다.

- 의존관계 역전 원칙 원칙을 준수하면 의존되는 코드에 영향을 주지 않고 의존성의 구체적인 구현을 변경할 수 있기 때문에 더 유연하고 유지 관리하기 쉬운 코드를 작성하는 데 도움이 될 수 있습니다. 또한 상위 수준 모듈이 하위 수준 모듈과 밀접하게 결합되지 않기 때문에 소프트웨어의 모듈성을 개선하는 데 도움이 될 수 있습니다.

- 다음은 DIP를 위반하는 간단한 Java 코드 예제입니다.

```java
public class User {
  private String username;
  private String password;

  public User(String username, String password) {
    this.username = username;
    this.password = password;
  }

  // getters and setters
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

- 이 예제에서 `Application` 클래스는 `UserService` 클래스와 `User` 클래스에 의존하므로 DIP를 위반합니다. 즉, 이러한 클래스 중 하나를 변경하거나 대체해야 하는 경우 `Application` 클래스도 변경해야 합니다. 이는 다른 클래스에 종속되기 때문에 `Application` 클래스를 유지 관리하고 테스트하기 더 어렵게 만듭니다.

- 다음은 DIP를 준수하는 간단한 Java 코드 예제입니다.

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

- 이 예에서 'Application' 클래스는 구체적인 구현이 아닌 추상화(인터페이스)에 의존하기 때문에 DIP를 준수합니다. `Application` 클래스는 `UserAuthenticationServiceImpl` 클래스에 의해 구현되는 `UserAuthenticationService` 인터페이스에 의존합니다. `UserAuthenticationServiceImpl` 클래스는 `InMemoryUserRepository` 클래스에 의해 구현되는 `UserRepository` 인터페이스에 의존합니다. 즉, 이러한 클래스의 구현을 변경해야 하는 경우 인터페이스가 유지되는 한 `Application` 클래스는 영향을 받지 않습니다. 이는 특정 구현에 밀접하게 결합되지 않기 때문에 `Application` 클래스를 보다 유연하고 유지 관리하기 쉽게 만듭니다.

## SOLID 원칙을 준수할 때의 장점

프로그래밍할 때 SOLID 원칙을 준수하면 몇 가지 장점이 있습니다.

### 유연성 향상

- SOLID 원칙을 준수하면 기존 기능을 손상시키지 않고 새로운 기능을 추가할 수 있고 구체적인 구현 대신 추상화를 사용하여 코드의 다른 부분 간의 결합을 줄일 수 있으므로 더 유연하고 변경하기 쉬운 코드를 작성할 수 있습니다.

### 재사용성 증가

- SOLID 원칙을 준수하면 단일 책임에 초점을 맞추고 다양한 컨텍스트에서 쉽게 사용할 수 있는 클래스와 인터페이스를 설계할 수 있으므로 재사용 가능한 코드를 작성하는 데 도움이 될 수 있습니다.

### 더 나은 코드 구성

- SOLID 원칙을 준수하면 이해하고 테스트하기 쉬운 작은 모듈식 구성 요소로 코드를 구성할 수 있으므로 이해하고 유지 관리하기 쉬운 코드를 작성하는 데 도움이 될 수 있습니다.

### 버그 발생 위험 감소

- SOLID 원칙을 준수하면 기존 코드를 수정하지 않고 새 기능을 추가할 수 있고 구체적인 구현 대신 추상화를 사용하여 코드의 다른 부분 간의 결합을 줄일 수 있기 때문에 코드를 수정할 때 버그가 발생할 위험을 줄이는 데 도움이 될 수 있습니다.

전반적으로 SOLID 원칙을 따르면 더 유연하고 재사용 가능하며 이해하기 쉬운 코드를 작성하여 시간이 지남에 따라 더 쉽게 유지 관리하고 확장할 수 있습니다.