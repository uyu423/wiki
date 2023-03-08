---
title: Object-Oriented Programming: Concepts and Best Practices
description: 
published: true
date: 2023-02-17T18:01:09.992Z
tags: 
editor: markdown
dateCreated: 2023-01-30T00:10:47.977Z
---

- [객체 지향 프로그래밍: 개념 및 모범 사례***Korean** version of this document is available*](/ko/Knowledge-base/Common/object-oriented-programming-concepts-and-best-practices)
{.links-list}


Object-Oriented Programming (OOP) is a programming paradigm based on the concept of objects, which are data structures that contain data, in the form of fields, and code, in the form of methods. 

OOP is a approach to software development in which software is organized around objects, rather than around functionality. The main idea behind OOP is to create objects that represent entities in the real world, and to write code that operates on these objects. 

There are four main principles of OOP:

### 1. Encapsulation

Encapsulation is the process of hiding the details of an object from the outside world. The idea is that an object should be responsible for its own data and behavior, and should not exposing its internals to the rest of the system. 

One way to achieve encapsulation is to make the fields of an object private, and to provide public methods that allow other parts of the system to interact with the object in a controlled way. 

For example, consider a class that represents a bank account. We might want to encapsulate the details of the account, such as the account balance and the account holder's name. We can do this by making the fields of the class private, and providing public methods for accessing and modifying the data:

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

As you can see, the `Account` class encapsulates the data and behavior of a bank account. By making the fields `private`, we prevent other parts of the system from directly accessing or modifying the data. The `public` methods provide a controlled way for other parts of the system to interact with the account. 

 Encapsulation is important for two reasons. First, it helps to keep the internals of an object hidden from the outside world. This makes the code easier to understand and maintain, because we don't need to worry about other parts of the system accidentally breaking the internals of our objects. 

Second, encapsulation allows us to change the internals of an object without affecting the rest of the system. For example, if we decided to change the way that the `getBalance` method worked, we could do so without affecting any code that calls that method. As long as the public interface of the `Account` class remains the same, code that uses the `Account` class will not need to be changed. 

### 2. Inheritance

Inheritance is a mechanism for reusing the code in a class by creating a new class that inherits from an existing class. The new class inherits all of the fields and methods of the existing class, and can add its own fields and methods. 

For example, consider a class that represents a 2D point:

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

Now, let's say we want to create a new class that represents a 3D point. We could create this class from scratch, but it would be much easier to simply inherit from the `Point2D` class and add a new field for the z coordinate:

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

As you can see, the `Point3D` class inherits from the `Point2D` class. This means that it has all of the same fields and methods as the `Point2D` class, plus its own `z` field. 

Inheritance is a powerful tool for code reuse, because it allows us to create new classes that are based on existing classes. This can save a lot of time and effort, because we don't have to reimplement the code that is already present in the existing class. 

### 3. Polymorphism

Polymorphism is the ability of an object to take on different forms. In the context of OOP, this means that a class can have multiple implementations, or that an object can behave differently in different situations. 

One common use of polymorphism is to define a common interface for a group of related classes. For example, consider a set of classes that represent shapes:

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

As you can see, the `Shape` interface defines a single method, `getArea`. This method is implemented by the `Rectangle`, `Circle`, and `Triangle` classes. 

We can use polymorphism to write code that can work with any shape, without knowing the details of the specific shape:

```java
public void printArea(Shape shape) {
    System.out.println("The area of the shape is: " + shape.getArea());
}
```

The `printArea` method takes a `Shape` object as a parameter, and prints out the area of the shape. Since the `printArea` method doesn't know the details of the specific shape, it can work with any object that implements the `Shape` interface. 

Polymorphism is a powerful concept because it allows us to write code that is not tied to any specific type. This makes our code more flexible and reusable, because we can use it with any object that implements the required interface. 

### 4. Abstraction

Abstraction is the process of hiding the details of an object from the outside world. The idea is that an object should expose a simple interface that allows other parts of the system to interact with it, without needing to know the details of its implementation. 

One way to achieve abstraction is to define an abstract class. An abstract class is a class that cannot be instantiated, but can be subclassed. An abstract class defines an interface that must be implemented by all subclasses. 

For example, consider a class that represents a shape:

```java
public abstract class Shape {
    public abstract double getArea();
}
```

As you can see, the `Shape` class is an abstract class. This means that it cannot be instantiated, but can be subclassed. The `Shape` class defines an interface that all subclasses must implement. In this case, the interface is defined by the `getArea` method. 

We can use abstraction to write code that can work with any shape, without knowing the details of the specific shape:

```java
public void printArea(Shape shape) {
    System.out.println("The area of the shape is: " + shape.getArea());
}
```

The `printArea` method takes a `Shape` object as a parameter, and prints out the area of the shape. Since the `printArea` method doesn't know the details of the specific shape, it can work with any object that inherits from the `Shape` class. 

Abstraction is a powerful concept because it allows us to write code that is not tied to any specific type. This makes our code more flexible and reusable, because we can use it with any object that inherits from the `Shape` class. 

## Resources

- [Object-Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming)
- [Encapsulation](https://en.wikipedia.org/wiki/Encapsulation_(computer_programming))
- [Inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming))
- [Polymorphism](https://en.wikipedia.org/wiki/Polymorphism_(computer_science))
- [Abstraction](https://en.wikipedia.org/wiki/Abstraction_(computer_science))