---
title: 객체 지향 프로그래밍: 개념 및 모범 사례
description: 
published: true
date: 2023-02-17T18:01:08.574Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:10:47.976Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Object-Oriented Programming: Concepts and Best Practices***English** version of this document is available*](/en/Knowledge-base/Common/object-oriented-programming-concepts-and-best-practices)
{.links-list}


객체 지향 프로그래밍(Object-Oriented Programming, OOP)은 필드 형태의 데이터와 메서드 형태의 코드를 포함하는 데이터 구조인 객체 개념을 기반으로 하는 프로그래밍 패러다임입니다.

OOP는 소프트웨어가 기능이 아닌 개체를 중심으로 구성되는 소프트웨어 개발 접근 방식입니다. OOP의 기본 아이디어는 실세계의 엔터티를 나타내는 개체를 만들고 이러한 개체에서 작동하는 코드를 작성하는 것입니다.

OOP에는 네 가지 주요 원칙이 있습니다.

### 1. 캡슐화

캡슐화는 외부 세계에서 개체의 세부 정보를 숨기는 프로세스입니다. 아이디어는 개체가 자체 데이터 및 동작에 대한 책임이 있어야 하며 내부를 시스템의 나머지 부분에 노출해서는 안 된다는 것입니다.

캡슐화를 달성하는 한 가지 방법은 개체의 필드를 비공개로 만들고 시스템의 다른 부분이 제어된 방식으로 개체와 상호 작용할 수 있도록 하는 공용 메서드를 제공하는 것입니다.

예를 들어 은행 계좌를 나타내는 클래스를 생각해 보십시오. 계정 잔액 및 계정 소유자의 이름과 같은 계정 세부 정보를 캡슐화할 수 있습니다. 클래스의 필드를 비공개로 만들고 데이터 액세스 및 수정을 위한 공개 메서드를 제공하여 이를 수행할 수 있습니다.

```java
public class Account {
    private double balance;
    private String name;
    
    public Account(double balance, String name) {
        this.balance = balance;
        this.name = name;
    }
    
    public double getBalance() {
        return balance;
    }
    
    public void setBalance(double balance) {
        this.balance = balance;
    }
    
    public String getName() {
        return name;
    }
    
    public void setName(String name) {
        this.name = name;
    }
}
```

보시다시피 'Account' 클래스는 은행 계좌의 데이터와 동작을 캡슐화합니다. 필드를 '비공개'로 만들어 시스템의 다른 부분에서 데이터에 직접 액세스하거나 수정하는 것을 방지합니다. '공용' 방법은 시스템의 다른 부분이 계정과 상호 작용할 수 있는 제어된 방법을 제공합니다.

 캡슐화는 두 가지 이유로 중요합니다. 첫째, 객체의 내부를 외부 세계로부터 숨긴 상태로 유지하는 데 도움이 됩니다. 이렇게 하면 시스템의 다른 부분이 실수로 개체의 내부를 손상시키는 것에 대해 걱정할 필요가 없기 때문에 코드를 더 쉽게 이해하고 유지 관리할 수 있습니다.

둘째, 캡슐화를 통해 시스템의 나머지 부분에 영향을 주지 않고 개체의 내부를 변경할 수 있습니다. 예를 들어 `getBalance` 메서드가 작동하는 방식을 변경하기로 결정한 경우 해당 메서드를 호출하는 코드에 영향을 주지 않고 변경할 수 있습니다. `Account` 클래스의 공용 인터페이스가 동일하게 유지되는 한 `Account` 클래스를 사용하는 코드를 변경할 필요가 없습니다.

### 2. 상속

상속은 기존 클래스에서 상속하는 새 클래스를 만들어 클래스의 코드를 재사용하는 메커니즘입니다. 새 클래스는 기존 클래스의 모든 필드와 메서드를 상속하며 자체 필드와 메서드를 추가할 수 있습니다.

예를 들어 2D 포인트를 나타내는 클래스를 생각해 보십시오.

```java
public class Point2D {
    private double x;
    private double y;
    
    public Point2D(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    public double getX() {
        return x;
    }
    
    public void setX(double x) {
        this.x = x;
    }
    
    public double getY() {
        return y;
    }
    
    public void setY(double y) {
        this.y = y;
    }
}
```

이제 3D 포인트를 나타내는 새 클래스를 만들고 싶다고 가정해 보겠습니다. 이 클래스를 처음부터 만들 수도 있지만 단순히 `Point2D` 클래스에서 상속하고 z 좌표에 대한 새 필드를 추가하는 것이 훨씬 더 쉬울 것입니다.

```java
public class Point3D extends Point2D {
    private double z;
    
    public Point3D(double x, double y, double z) {
        super(x, y);
        this.z = z;
    }
    
    public double getZ() {
        return z;
    }
    
    public void setZ(double z) {
        this.z = z;
    }
}
```

보시다시피 `Point3D` 클래스는 `Point2D` 클래스에서 상속됩니다. 즉, `Point2D` 클래스와 동일한 필드와 메서드가 모두 있고 자체 `z` 필드가 있습니다.

상속은 기존 클래스를 기반으로 새 클래스를 만들 수 있기 때문에 코드 재사용을 위한 강력한 도구입니다. 이렇게 하면 기존 클래스에 이미 있는 코드를 다시 구현할 필요가 없기 때문에 많은 시간과 노력을 절약할 수 있습니다.

### 3. 다형성

다형성은 객체가 다른 형태를 취하는 능력입니다. OOP의 맥락에서 이것은 클래스가 여러 구현을 가질 수 있거나 개체가 다른 상황에서 다르게 동작할 수 있음을 의미합니다.

다형성의 일반적인 용도 중 하나는 관련 클래스 그룹에 대한 공통 인터페이스를 정의하는 것입니다. 예를 들어 모양을 나타내는 일련의 클래스를 고려하십시오.

```java
public interface Shape {
    public double getArea();
}

public class Rectangle implements Shape {
    private double width;
    private double height;
    
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }
    
    public double getWidth() {
        return width;
    }
    
    public void setWidth(double width) {
        this.width = width;
    }
    
    public double getHeight() {
        return height;
    }
    
    public void setHeight(double height) {
        this.height = height;
    }
    
    public double getArea() {
        return width * height;
    }
}

public class Circle implements Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    public double getRadius() {
        return radius;
    }
    
    public void setRadius(double radius) {
        this.radius = radius;
    }
    
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

public class Triangle implements Shape {
    private double base;
    private double height;
    
    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }
    
    public double getBase() {
        return base;
    }
    
    public void setBase(double base) {
        this.base = base;
    }
    
    public double getHeight() {
        return height;
    }
    
    public void setHeight(double height) {
        this.height = height;
    }
    
    public double getArea() {
        return 0.5 * base * height;
    }
}
```

보시다시피 `Shape` 인터페이스는 `getArea`라는 단일 메서드를 정의합니다. 이 메서드는 `Rectangle`, `Circle` 및 `Triangle` 클래스에 의해 구현됩니다.

다형성을 사용하여 특정 모양에 대한 세부 정보를 몰라도 모든 모양에서 작동할 수 있는 코드를 작성할 수 있습니다.

```java
public void printArea(Shape shape) {
    System.out.println("The area of the shape is: " + shape.getArea());
}
```

`printArea` 메소드는 `Shape` 객체를 매개변수로 받아 도형의 면적을 출력합니다. `printArea` 메서드는 특정 도형의 세부 사항을 모르기 때문에 `Shape` 인터페이스를 구현하는 모든 객체와 함께 작동할 수 있습니다.

다형성은 특정 유형에 얽매이지 않는 코드를 작성할 수 있게 해주기 때문에 강력한 개념입니다. 필요한 인터페이스를 구현하는 모든 객체와 함께 코드를 사용할 수 있기 때문에 코드가 더 유연하고 재사용 가능합니다.

### 4. 추상화

추상화는 외부 세계에서 개체의 세부 정보를 숨기는 프로세스입니다. 아이디어는 개체가 구현의 세부 사항을 알 필요 없이 시스템의 다른 부분이 개체와 상호 작용할 수 있도록 하는 간단한 인터페이스를 노출해야 한다는 것입니다.

추상화를 달성하는 한 가지 방법은 추상 클래스를 정의하는 것입니다. 추상 클래스는 인스턴스화할 수 없지만 하위 클래스로 만들 수 있는 클래스입니다. 추상 클래스는 모든 하위 클래스에서 구현해야 하는 인터페이스를 정의합니다.

예를 들어 모양을 나타내는 클래스를 생각해 보십시오.

```java
public abstract class Shape {
    public abstract double getArea();
}
```

보시다시피 `Shape` 클래스는 추상 클래스입니다. 이는 인스턴스화할 수 없지만 서브클래싱할 수 있음을 의미합니다. `Shape` 클래스는 모든 하위 클래스가 구현해야 하는 인터페이스를 정의합니다. 이 경우 인터페이스는 `getArea` 메서드로 정의됩니다.

추상화를 사용하여 특정 셰이프의 세부 정보를 몰라도 모든 셰이프에서 작동할 수 있는 코드를 작성할 수 있습니다.

```java
public void printArea(Shape shape) {
    System.out.println("The area of the shape is: " + shape.getArea());
}
```

`printArea` 메소드는 `Shape` 객체를 매개변수로 받아 도형의 면적을 출력합니다. `printArea` 메서드는 특정 도형의 세부 사항을 모르기 때문에 `Shape` 클래스에서 상속되는 모든 객체와 함께 작동할 수 있습니다.

추상화는 특정 유형에 얽매이지 않는 코드를 작성할 수 있게 해주기 때문에 강력한 개념입니다. 이렇게 하면 `Shape` 클래스에서 상속되는 모든 객체와 함께 코드를 사용할 수 있기 때문에 코드가 더 유연하고 재사용 가능합니다.

## 자원

- [객체지향 프로그래밍](https://en.wikipedia.org/wiki/Object-oriented_programming)
- [캡슐화](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming))
- [상속](https://en.wikipedia.org/wiki/Inheritance_(객체 지향_프로그래밍))
- [다형성](https://en.wikipedia.org/wiki/Polymorphism_(computer_science))
- [추상화](https://en.wikipedia.org/wiki/Abstraction_(computer_science))