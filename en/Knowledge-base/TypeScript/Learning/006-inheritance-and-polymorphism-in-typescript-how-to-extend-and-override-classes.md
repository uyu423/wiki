---
title: 006: Inheritance and Polymorphism in TypeScript: How to Extend and Override Classes
description: 
published: true
date: 2023-03-06T15:32:59.828Z
tags: 
editor: markdown
dateCreated: 2023-03-06T15:32:58.466Z
---

- [006: TypeScript의 상속과 다형성: 클래스를 확장하고 재정의하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/006-inheritance-and-polymorphism-in-typescript-how-to-extend-and-override-classes)
{.links-list}



Inheritance and Polymorphism in TypeScript: How to Extend and Override Classes

TypeScript is an object-oriented programming language that extends JavaScript by adding optional static typing and class-based object-oriented programming. One of the most important features of object-oriented programming is inheritance. Inheritance allows us to create a new class based on an existing class, inheriting all the properties and methods of the parent class. In this post, we will explore inheritance and polymorphism in TypeScript, and learn how to extend and override classes.

## Inheritance in TypeScript

Inheritance is a mechanism that allows us to create a new class from an existing class. The new class is called a derived class or subclass, and the existing class is called a base class or superclass. The derived class inherits all the properties and methods of the base class, and can also add new properties and methods of its own.

To create a derived class in TypeScript, we use the `extends` keyword. Here's an example:

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Dog extends Animal {
  bark() {
    console.log('Woof! Woof!');
  }
}
```

In this example, we have a base class `Animal` with a `name` property and a `move` method. We also have a derived class `Dog` that extends `Animal` and adds a `bark` method. The `Dog` class inherits the `name` property and the `move` method from the `Animal` class.

We can create instances of the `Dog` class and call its methods like this:

```typescript
let dog = new Dog('Fido');
dog.move(10);
dog.bark();
```

This will output:

```
Fido moved 10m.
Woof! Woof!
```

## Polymorphism in TypeScript

Polymorphism is a concept in object-oriented programming that allows objects of different classes to be treated as if they were objects of the same class. In TypeScript, polymorphism is achieved through inheritance and method overriding.

Method overriding is a technique that allows a derived class to provide a specific implementation of a method that is already defined in its base class. The overridden method in the derived class has the same name and signature as the method in the base class, but a different implementation.

Here's an example of method overriding in TypeScript:

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Snake extends Animal {
  move(distanceInMeters = 5) {
    console.log(`${this.name} slithered ${distanceInMeters}m.`);
  }
}

class Horse extends Animal {
  move(distanceInMeters = 45) {
    console.log(`${this.name} galloped ${distanceInMeters}m.`);
  }
}

let sam = new Snake('Sammy the Python');
let tom: Animal = new Horse('Tommy the Palomino');

sam.move();
tom.move(34);
```

In this example, we have a base class `Animal` with a `name` property and a `move` method. We also have two derived classes, `Snake` and `Horse`, that override the `move` method with their own implementations.

We create instances of both classes and call their `move` methods. The `Snake` instance calls its overridden `move` method, which outputs `"Sammy the Python slithered 5m."`. The `Horse` instance calls its overridden `move` method, which outputs `"Tommy the Palomino galloped 34m."`.

## Extending and Overriding Classes

In TypeScript, we can extend and override classes to create more specialized classes. Extending a class allows us to inherit all the properties and methods of the base class, while overriding a method allows us to provide a more specific implementation of that method in the derived class.

Here's an example of extending and overriding classes in TypeScript:

```typescript
class Person {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

class Programmer extends Person {
  greet() {
    console.log(`Hello, my name is ${this.name} and I'm a programmer.`);
  }
  code() {
    console.log(`${this.name} is coding...`);
  }
}

let john = new Person('John');
let jane = new Programmer('Jane');

john.greet();
jane.greet();
jane.code();
```

In this example, we have a base class `Person` with a `name` property and a `greet` method. We also have a derived class `Programmer` that extends `Person` and overrides the `greet` method with a more specific implementation. The `Programmer` class also adds a new `code` method.

We create instances of both classes and call their `greet` and `code` methods. The `Person` instance calls its own `greet` method, which outputs `"Hello, my name is John."`. The `Programmer` instance calls its overridden `greet` method, which outputs `"Hello, my name is Jane and I'm a programmer."`. The `Programmer` instance also calls its own `code` method, which outputs `"Jane is coding..."`.

## Additional Information

In TypeScript, we can also use interfaces to define the shape of an object. Interfaces can be used to describe the public API of a class, or to define the type of a function parameter or return value.

## Conclusion

Inheritance and polymorphism are important concepts in object-oriented programming, and TypeScript provides powerful mechanisms for implementing them. By extending and overriding classes, we can create more specialized classes that inherit and modify the behavior of their parent classes. In addition, interfaces provide a way to define the shape of an object and ensure type safety in our code.

## External Resources

- [TypeScript Handbook: Inheritance](https://www.typescriptlang.org/docs/handbook/2/objects.html#inheritance)
- [TypeScript Handbook: Polymorphism](https://www.typescriptlang.org/docs/handbook/2/classes.html#polymorphism)
- [TypeScript Handbook: Interfaces](https://www.typescriptlang.org/docs/handbook/interfaces.html)