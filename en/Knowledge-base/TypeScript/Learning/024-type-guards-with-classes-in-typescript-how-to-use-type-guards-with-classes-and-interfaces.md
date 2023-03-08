---
title: 024: Type Guards with Classes in TypeScript: How to Use Type Guards with Classes and Interfaces
description: 
published: true
date: 2023-03-03T01:32:29.378Z
tags: 
editor: markdown
dateCreated: 2023-03-03T01:32:22.114Z
---

- [024: TypeScript에서 클래스가 있는 Type Guard: 클래스 및 인터페이스에서 Type Guard를 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/024-type-guards-with-classes-in-typescript-how-to-use-type-guards-with-classes-and-interfaces)
{.links-list}
Type Guards with Classes in TypeScript: How to Use Type Guards with Classes and Interfaces

TypeScript is a superset of JavaScript that adds optional static typing to the language. It allows developers to write code that is more robust, maintainable, and easier to understand. One of the features of TypeScript is type guards, which allow developers to write code that checks the type of a variable at runtime. In this article, we will explore how to use type guards with classes and interfaces in TypeScript.

## What are Type Guards?

Type guards are a way to check the type of a variable at runtime. They are used to ensure that a variable is of a certain type before performing an operation on it. This is useful in cases where TypeScript cannot infer the type of a variable, or when the type of a variable changes during runtime.

Type guards can be implemented using the `typeof` operator, the `instanceof` operator, user-defined type guards, and more.

## Type Guards with Classes

Type guards can be used with classes to check whether a variable is an instance of a particular class. This is useful when working with class hierarchies, where a class inherits from another class.

Consider the following example:

```typescript
class Animal {
  name: string;
  constructor(name: string) {
    this.name = name;
  }
}

class Dog extends Animal {
  breed: string;
  constructor(name: string, breed: string) {
    super(name);
    this.breed = breed;
  }
}

function isAnimal(obj: any): obj is Animal {
  return obj instanceof Animal;
}

const dog = new Dog("Fido", "Labrador");
const animal: Animal = dog;

if (isAnimal(animal)) {
  console.log(animal.name); // Output: Fido
}
```

In the above example, we define two classes: `Animal` and `Dog`. We also define a function `isAnimal` that checks whether a given object is an instance of the `Animal` class. The function returns a boolean value, but it also has a type predicate `obj is Animal` that tells TypeScript that if the function returns `true`, the object is an instance of the `Animal` class.

We then create an instance of the `Dog` class and assign it to a variable of type `Animal`. We then use the `isAnimal` function to check whether the variable is an instance of the `Animal` class. If it is, we can safely access the `name` property of the `Animal` class.

## Type Guards with Interfaces

Type guards can also be used with interfaces to check whether a variable conforms to a particular interface. This is useful when working with objects that have a specific shape.

Consider the following example:

```typescript
interface Person {
  name: string;
  age: number;
}

function isPerson(obj: any): obj is Person {
  return obj && typeof obj.name === "string" && typeof obj.age === "number";
}

const person = { name: "Alice", age: 30 };

if (isPerson(person)) {
  console.log(person.name); // Output: Alice
}
```

In the above example, we define an interface `Person` that has two properties: `name` of type `string` and `age` of type `number`. We also define a function `isPerson` that checks whether a given object conforms to the `Person` interface.

We then create an object that has the same shape as the `Person` interface and assign it to a variable. We then use the `isPerson` function to check whether the variable conforms to the `Person` interface. If it does, we can safely access the `name` property of the object.

## Additional Information

Type guards can also be used with union types to narrow down the type of a variable. This is useful when working with variables that can have more than one type.

Consider the following example:

```typescript
interface Square {
  kind: "square";
  size: number;
}

interface Rectangle {
  kind: "rectangle";
  width: number;
  height: number;
}

interface Circle {
  kind: "circle";
  radius: number;
}

type Shape = Square | Rectangle | Circle;

function isSquare(shape: Shape): shape is Square {
  return shape.kind === "square";
}

const square: Square = { kind: "square", size: 10 };

if (isSquare(square)) {
  console.log(square.size); // Output: 10
}
```

In the above example, we define three interfaces: `Square`, `Rectangle`, and `Circle`. We also define a union type `Shape` that can be any of the three interfaces.

We then define a function `isSquare` that checks whether a given `Shape` is a `Square`. The function returns a boolean value, but it also has a type predicate `shape is Square` that tells TypeScript that if the function returns `true`, the variable is a `Square`.

We then create an instance of the `Square` interface and assign it to a variable of type `Shape`. We then use the `isSquare` function to check whether the variable is a `Square`. If it is, we can safely access the `size` property of the `Square`.

## Warnings and Dangers

Type guards can be expensive in terms of performance, especially when used with complex objects. It is important to use them judiciously and only when necessary.

Type guards can also be circumvented by malicious code, so it is important to always validate user input on the server-side.

## Conclusion

TypeScript's type guards provide a powerful way to ensure type safety in your code. They can be used with classes, interfaces, and union types to narrow down the type of a variable. When used correctly, they can make your code more robust, maintainable, and easier to understand.

## External Resources

- [TypeScript Handbook: Type Guards and Differentiating Types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-differentiating-types)
- [TypeScript Deep Dive: Type Guards and Type Assertions](https://basarat.gitbook.io/typescript/type-system/typeguard)
- [TypeScript Playground](https://www.typescriptlang.org/play)