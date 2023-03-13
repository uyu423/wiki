---
title: 005: Classes in TypeScript: Object-Oriented Programming in TypeScript
description: 
published: true
date: 2023-03-13T13:33:29.479Z
tags: 
editor: markdown
dateCreated: 2023-03-13T13:33:29.479Z
---

- [005: TypeScript의 클래스: TypeScript의 객체 지향 프로그래밍***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/005-classes-in-typescript-object-oriented-programming-in-typescript)
{.links-list}



Classes in TypeScript: Object-Oriented Programming in TypeScript

TypeScript is a superset of JavaScript that allows developers to write code using object-oriented programming (OOP) concepts. In TypeScript, classes are an essential part of OOP, and they allow developers to create objects that have properties and methods.

In this article, we will explore classes in TypeScript and how to use them to create objects. We will also look at inheritance and polymorphism, two important concepts in OOP.

## Creating Classes in TypeScript

To create a class in TypeScript, you use the `class` keyword followed by the name of the class. For example:

```typescript
class Person {
  name: string;
  age: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}
```

In the example above, we have created a `Person` class with two properties: `name` and `age`. We have also defined a constructor that takes in two parameters: `name` and `age`. The constructor assigns the values of `name` and `age` to the corresponding properties.

We have also defined a `greet()` method that logs a message to the console that includes the person's name and age.

## Creating Objects from Classes

Once you have created a class, you can create objects from it. To create an object, you use the `new` keyword followed by the name of the class and any arguments that the constructor requires. For example:

```typescript
const person1 = new Person('John', 30);
person1.greet(); // logs "Hello, my name is John and I am 30 years old."
```

In the example above, we have created a `Person` object named `person1` with the name "John" and age 30. We have then called the `greet()` method on `person1`, which logs a message to the console.

## Inheritance

Inheritance is a key concept in OOP that allows you to create a new class based on an existing class. The new class inherits all the properties and methods of the existing class, and you can add new properties and methods or override existing ones.

To create a class that inherits from an existing class, you use the `extends` keyword followed by the name of the class you want to inherit from. For example:

```typescript
class Employee extends Person {
  salary: number;
  constructor(name: string, age: number, salary: number) {
    super(name, age);
    this.salary = salary;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}, I am ${this.age} years old, and my salary is ${this.salary}.`);
  }
}
```

In the example above, we have created an `Employee` class that inherits from the `Person` class. The `Employee` class has a new property called `salary`, and we have overridden the `greet()` method to include the salary in the message.

We have also called the `super()` method in the constructor to call the constructor of the `Person` class and pass in the `name` and `age` parameters.

## Polymorphism

Polymorphism is another important concept in OOP that allows you to use a single interface to represent multiple types. In TypeScript, you can achieve polymorphism through inheritance and interfaces.

To demonstrate polymorphism, let's create another class that inherits from the `Person` class:

```typescript
class Student extends Person {
  grade: string;
  constructor(name: string, age: number, grade: string) {
    super(name, age);
    this.grade = grade;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}, I am ${this.age} years old, and I am in grade ${this.grade}.`);
  }
}
```

In the example above, we have created a `Student` class that also inherits from the `Person` class. The `Student` class has a new property called `grade`, and we have overridden the `greet()` method to include the grade in the message.

Now, let's create an array of `Person` objects that contains an `Employee` and a `Student`:

```typescript
const people: Person[] = [
  new Employee('John', 30, 50000),
  new Student('Jane', 20, 'A')
];
```

In the example above, we have created an array of `Person` objects that contains an `Employee` and a `Student`. Because both `Employee` and `Student` inherit from `Person`, we can use the `Person` interface to represent both types.

We can then call the `greet()` method on each object in the array:

```typescript
people.forEach(person => {
  person.greet();
});
```

This will log the following messages to the console:

```
Hello, my name is John, I am 30 years old, and my salary is 50000.
Hello, my name is Jane, I am 20 years old, and I am in grade A.
```

## Conclusion

In this article, we have explored classes in TypeScript and how to use them to create objects. We have also looked at inheritance and polymorphism, two important concepts in OOP.

TypeScript's support for OOP concepts makes it a powerful language for building complex applications. By mastering classes, inheritance, and polymorphism, you can write more maintainable and scalable code.

## Additional Information

- [TypeScript Classes](https://www.typescriptlang.org/docs/handbook/classes.html)
- [TypeScript Inheritance](https://www.typescriptlang.org/docs/handbook/inheritance.html)
- [TypeScript Polymorphism](https://www.typescriptlang.org/docs/handbook/polymorphism.html)

## Warnings and Dangers

- Be careful not to overuse inheritance, as it can lead to complex and hard-to-maintain code.
- Polymorphism can be a powerful tool, but it can also make code harder to understand if not used correctly.