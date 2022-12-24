---
title: About the SOLID Principles for Object-Oriented Programming
description: 
published: true
date: 2022-12-24T21:41:54.164Z
tags: java, oop
editor: markdown
dateCreated: 2022-12-24T21:41:54.164Z
---

## What is SOLID principles?

SOLID is a set of five principles for object-oriented programming and design that was introduced by Robert C. Martin. The acronym SOLID stands for the following five principles:

### Single Responsibility Principle (SRP)
- The Single Responsibility Principle states that a class should have only one reason to change. This means that a class should have a single, well-defined responsibility and should not be responsible for multiple things.

- Adhering to the Single Responsibility Principle can help you write code that is easier to maintain and test, because changes to the class are isolated to a single responsibility. It can also help you avoid code duplication and improve the modularity of your software.

- Here is an example of a class that violates the Single Responsibility Principle, because it has multiple responsibilities:

```java
public class Employee {
  private String name;
  private String address;
  private String phone;
  private double salary;

  public Employee(String name, String address, String phone, double salary) {
    this.name = name;
    this.address = address;
    this.phone = phone;
    this.salary = salary;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public String getAddress() {
    return address;
  }

  public void setPhone(String phone) {
    this.phone = phone;
  }

  public String getPhone() {
    return phone;
  }

  public void setSalary(double salary) {
    this.salary = salary;
  }

  public double getSalary() {
    return salary;
  }

  public void saveEmployee() {
    // code to save employee to database
  }

  public void sendEmail() {
    // code to send email to employee
  }
}
```

- This class has responsibilities related to managing employee information (e.g., setting and getting name, address, phone, and salary) as well as saving employee information to a database and sending email to employees.

- Here is an example of how we could refactor this class to adhere to the Single Responsibility Principle:

```java
public class Employee {
  private String name;
  private String address;
  private String phone;
  private double salary;

  public Employee(String name, String address, String phone, double salary) {
    this.name = name;
    this.address = address;
    this.phone = phone;
    this.salary = salary;
  }

  public void setName(String name) {
    this.name = name;
  }

  public String getName() {
    return name;
  }

  public void setAddress(String address) {
    this.address = address;
  }

  public String getAddress() {
    return address;
  }

  public void setPhone(String phone) {
    this.phone = phone;
  }

  public String getPhone() {
    return phone;
  }

  public void setSalary(double salary) {
    this.salary = salary;
  }

  public double getSalary() {
    return salary;
  }
}

public class EmployeeRepository {
  public void saveEmployee(Employee employee) {
    // code to save employee to database
  }
}

public class EmailService {
  public void sendEmail(Employee employee) {
    // code to send email to employee
  }
}

```

### Open-Closed Principle (OCP)

- The Open-Closed Principle states that a class should be open for extension but closed for modification. This means that you should be able to add new functionality to a class without changing its existing code.

- Adhering to the Open-Closed Principle can help you write code that is more flexible and easier to maintain, because you can add new features without breaking existing functionality. It can also help you reduce the risk of introducing bugs when modifying existing code.

- here is a simple Java code example illustrating the Open-Closed Principle (OCP):

```java
public abstract class Animal {
  public abstract void makeSound();
}

public class Cat extends Animal {
  @Override
  public void makeSound() {
    System.out.println("Meow");
  }
}

public class Dog extends Animal {
  @Override
  public void makeSound() {
    System.out.println("Woof");
  }
}

public class AnimalSoundPrinter {
  public void printSounds(List<Animal> animals) {
    for (Animal animal : animals) {
      animal.makeSound();
    }
  }
}
```

- In this example, the AnimalSoundPrinter class is able to print the sounds made by different types of animals without having to know the specific implementation details of each animal. This is an example of how the AnimalSoundPrinter class is open for extension (we can add new types of animals without modifying the AnimalSoundPrinter class) but closed for modification (we don't need to change the AnimalSoundPrinter class to add new types of animals).

### Liskov Substitution Principle (LSP)

- The Liskov Substitution Principle states that subtypes should be substitutable for their base types. This means that if a class is a subtype of another class, it should be able to be used in the same way as the base class without affecting the correctness of the program.

- Adhering to the Liskov Substitution Principle can help you write code that is more flexible and easier to maintain, because you can use subtypes in the same way as the base type without worrying about unintended side effects. It can also help you write code that is easier to understand, because you know that subtypes can be used in the same way as the base type.

- here is a simple Java code example illustrating the Liskov Substitution Principle (LSP):

```java
public abstract class Shape {
  public abstract double getArea();
}

public class Rectangle extends Shape {
  private double width;
  private double height;

  public Rectangle(double width, double height) {
    this.width = width;
    this.height = height;
  }

  @Override
  public double getArea() {
    return width * height;
  }
}

public class Square extends Shape {
  private double sideLength;

  public Square(double sideLength) {
    this.sideLength = sideLength;
  }

  @Override
  public double getArea() {
    return sideLength * sideLength;
  }
}

public class ShapeCalculator {
  public double calculateTotalArea(List<Shape> shapes) {
    double totalArea = 0;
    for (Shape shape : shapes) {
      totalArea += shape.getArea();
    }
    return totalArea;
  }
}
```

- In this example, the Square class is a subclass of the Shape class and adheres to the Liskov Substitution Principle because it can be used in the same way as the Rectangle class without affecting the correctness of the program. Both classes have the same getArea() method and can be used interchangeably in the ShapeCalculator class.

### Interface Segregation Principle (ISP)

- The Interface Segregation Principle states that clients should not be forced to depend on interfaces they do not use. This means that you should create small, specific interfaces rather than large, general ones.

- Adhering to the Interface Segregation Principle can help you write code that is more flexible and easier to understand, because you can create specialized interfaces that are easier to implement and use. It can also help you avoid unnecessary dependencies and improve the modularity of your software.

- here is a simple Java code example illustrating the Interface Segregation Principle (ISP):

```java
public interface Animal {
  void makeSound();
  void eat();
}

public interface Carnivore {
  void eatMeat();
}

public interface Herbivore {
  void eatPlants();
}

public class Lion implements Animal, Carnivore {
  @Override
  public void makeSound() {
    System.out.println("Roar");
  }

  @Override
  public void eat() {
    eatMeat();
  }

  @Override
  public void eatMeat() {
    System.out.println("Eating a zebra");
  }
}

public class Gazelle implements Animal, Herbivore {
  @Override
  public void makeSound() {
    System.out.println("Bleat");
  }

  @Override
  public void eat() {
    eatPlants();
  }

  @Override
  public void eatPlants() {
    System.out.println("Eating grass");
  }
}
```

- In this example, the Lion class implements the Animal and Carnivore interfaces, and the Gazelle class implements the Animal and Herbivore interfaces. This adheres to the Interface Segregation Principle because the Lion class only has to implement the methods it needs (makeSound() and eatMeat()) and the Gazelle class only has to implement the methods it needs (makeSound() and eatPlants()). This allows us to create more specialized interfaces that are easier to implement and use.

### Dependency Inversion Principle (DIP)

- Dependency Inversion Principle (DIP) states that high-level modules should not depend on low-level modules, but rather both should depend on abstractions. This means that you should depend on abstractions (such as interfaces or abstract classes) rather than on concrete implementations when writing code.

- Adhering to the Dependency Inversion Principle can help you write code that is more flexible and easier to maintain, because you can change the concrete implementation of a dependency without affecting the code that depends on it. It can also help you improve the modularity of your software, because high-level modules are not tightly coupled to low-level ones.

- here is a simple Java code example illustrating the Dependency Inversion Principle (DIP):

```java
public interface Animal {
  void makeSound();
}

public class Cat implements Animal {
  @Override
  public void makeSound() {
    System.out.println("Meow");
  }
}

public class Dog implements Animal {
  @Override
  public void makeSound() {
    System.out.println("Woof");
  }
}

public class AnimalSoundMaker {
  private Animal animal;

  public AnimalSoundMaker(Animal animal) {
    this.animal = animal;
  }

  public void makeSound() {
    animal.makeSound();
  }
}

public class Main {
  public static void main(String[] args) {
    Animal cat = new Cat();
    Animal dog = new Dog();
    AnimalSoundMaker catSoundMaker = new AnimalSoundMaker(cat);
    AnimalSoundMaker dogSoundMaker = new AnimalSoundMaker(dog);
    catSoundMaker.makeSound();
    dogSoundMaker.makeSound();
  }
}
```

- In this example, the AnimalSoundMaker class depends on the abstraction (Animal interface) rather than on concrete implementations (Cat and Dog classes). This adheres to the Dependency Inversion Principle because it allows us to change the concrete implementation of the Animal interface without affecting the AnimalSoundMaker class. For example, if we wanted to add a new type of animal, we could create a new class that implements the Animal interface and pass an instance of the new class to the AnimalSoundMaker constructor, without having to modify the AnimalSoundMaker class.

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