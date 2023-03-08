---
title: 033: This Types in TypeScript: How to Work with the 'this' Keyword in Classes and Functions
description: 
published: true
date: 2023-03-04T02:32:46.847Z
tags: 
editor: markdown
dateCreated: 2023-03-04T02:32:39.554Z
---

- [033: TypeScript의 This 유형: 클래스와 함수에서 'this' 키워드로 작업하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/033-this-types-in-typescript-how-to-work-with-the-this-keyword-in-classes-and-functions)
{.links-list}


This Types in TypeScript: How to Work with the 'this' Keyword in Classes and Functions

When working with TypeScript, you may have come across the 'this' keyword. The 'this' keyword is used to refer to the current instance of an object or class. It can be a bit confusing to work with, especially when dealing with functions and classes. In this post, we will explore the 'this' keyword and how to work with it in TypeScript.

## Understanding 'this' in TypeScript

In TypeScript, the 'this' keyword is used to refer to the current instance of an object or class. When used inside a function or method of a class, 'this' refers to the instance of that class. When used inside a function that is not part of a class, 'this' refers to the global object (window in a browser or global in Node.js).

For example, consider the following class:

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

const person = new Person('John', 30);
person.greet(); // Output: Hello, my name is John and I am 30 years old.
```

In this example, we have a Person class with a constructor and a greet method. Inside the greet method, we use the 'this' keyword to refer to the current instance of the Person class. When we create a new instance of the Person class and call the greet method, the output is "Hello, my name is John and I am 30 years old."

## Using 'this' in Functions

When using the 'this' keyword inside a function that is not part of a class, it refers to the global object. This can be problematic if you want to use 'this' to refer to a specific object. To solve this problem, you can use the call, apply, or bind methods.

### The call Method

The call method is used to call a function with a specified 'this' value and arguments provided individually.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

greet.call(person); // Output: Hello, my name is John and I am 30 years old.
```

In this example, we have a greet function that uses the 'this' keyword to refer to the name and age properties of an object. We create a person object with name and age properties, and then use the call method to call the greet function with the person object as the 'this' value.

### The apply Method

The apply method is similar to the call method, but it takes arguments as an array.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

greet.apply(person); // Output: Hello, my name is John and I am 30 years old.
```

In this example, we have the same greet function and person object as before, but we use the apply method instead of the call method.

### The bind Method

The bind method is used to create a new function with a specified 'this' value.

```typescript
function greet() {
  console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
}

const person = {
  name: 'John',
  age: 30
};

const greetPerson = greet.bind(person);
greetPerson(); // Output: Hello, my name is John and I am 30 years old.
```

In this example, we create a new function called greetPerson using the bind method. The greetPerson function has a 'this' value of the person object.

## Using 'this' in Classes

When using the 'this' keyword inside a class, it refers to the instance of that class. However, there are some cases where 'this' can be problematic, such as when using event listeners or passing methods as callbacks.

### Using Arrow Functions

One way to avoid problems with 'this' in classes is to use arrow functions. Arrow functions do not have their own 'this' value, so they use the 'this' value of the enclosing lexical scope.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;

    document.addEventListener('click', () => {
      this.greet();
    });
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person('John', 30);
```

In this example, we have a Person class with a constructor that adds an event listener to the document. Inside the event listener, we use an arrow function to call the greet method of the Person class, which uses the 'this' keyword to refer to the instance of the Person class.

### Using bind

Another way to solve problems with 'this' in classes is to use the bind method.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;

    document.addEventListener('click', this.greet.bind(this));
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person = new Person('John', 30);
```

In this example, we use the bind method to bind the 'this' value of the greet method to the instance of the Person class.

## Conclusion

In this post, we have explored the 'this' keyword in TypeScript and how to work with it in functions and classes. We have seen how to use call, apply, and bind to specify the 'this' value of a function, and how to use arrow functions and bind to avoid problems with 'this' in classes. By understanding how to work with 'this' in TypeScript, you can write more effective and efficient code.

## Additional Information

- [MDN Web Docs - this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
- [TypeScript Documentation - Classes](https://www.typescriptlang.org/docs/handbook/classes.html)
- [TypeScript Documentation - Functions](https://www.typescriptlang.org/docs/handbook/functions.html)

## Warnings

- Be careful when using 'this' inside functions that are not part of a class, as it refers to the global object by default.
- When using arrow functions in classes, be aware that they do not have their own 'this' value and use the 'this' value of the enclosing lexical scope.

## Dangers

- Using 'this' incorrectly can lead to unexpected behavior and bugs in your code. Always make sure you understand how 'this' works before using it.