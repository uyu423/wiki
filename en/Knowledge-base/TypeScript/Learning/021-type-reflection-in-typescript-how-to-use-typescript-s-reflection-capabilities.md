---
title: 021: Type Reflection in TypeScript: How to Use TypeScript's Reflection Capabilities
description: 
published: true
date: 2023-03-09T04:32:44.312Z
tags: 
editor: markdown
dateCreated: 2023-03-09T04:32:44.312Z
---

- [021: TypeScript에서 타입 리플렉션: TypeScript의 리플렉션 기능을 사용하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/021-type-reflection-in-typescript-how-to-use-typescript-s-reflection-capabilities)
{.links-list}



Type Reflection in TypeScript: How to Use TypeScript's Reflection Capabilities

TypeScript is a strongly-typed programming language that provides a lot of features to make our code more reliable and maintainable. One of the most powerful features of TypeScript is its reflection capabilities, which allow us to inspect and manipulate the type information at runtime. In this article, we'll explore how to use TypeScript's reflection capabilities to improve our code and make it more flexible.

## What is Type Reflection?

Type Reflection is the ability of a programming language to inspect and manipulate the type information of an object at runtime. In TypeScript, this is achieved through the use of the `Reflect` object, which provides a set of methods and properties for working with type information.

With Type Reflection, we can do things like:

- Inspect the properties of an object at runtime
- Determine the type of an object at runtime
- Create new instances of objects based on their type information
- Modify the type information of an object at runtime

## How to Use Type Reflection in TypeScript

Let's explore some practical examples of how to use TypeScript's reflection capabilities.

### 1. Inspecting Object Properties

Suppose we have an object with some properties:

```typescript
const person = {
  name: 'John',
  age: 30,
  address: {
    city: 'New York',
    state: 'NY'
  }
};
```

We can use the `Reflect` object to inspect the properties of this object at runtime:

```typescript
const propertyNames = Reflect.ownKeys(person);
console.log(propertyNames); // ['name', 'age', 'address']
```

In this example, we're using the `Reflect.ownKeys()` method to get an array of property names for the `person` object. This method returns all own property keys of the given object.

### 2. Determining the Type of an Object

We can also use the `Reflect` object to determine the type of an object at runtime:

```typescript
const person = {
  name: 'John',
  age: 30
};

const type = Reflect.getPrototypeOf(person).constructor.name;
console.log(type); // 'Object'
```

In this example, we're using the `Reflect.getPrototypeOf()` method to get the prototype of the `person` object, and then using the `constructor` property to get the name of the constructor function. This gives us the name of the type of the object, which in this case is `Object`.

### 3. Creating New Instances of Objects

We can also use the `Reflect` object to create new instances of objects based on their type information:

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

const data = {
  name: 'John',
  age: 30
};

const person = Reflect.construct(Person, [data.name, data.age]);
console.log(person); // Person { name: 'John', age: 30 }
```

In this example, we're using the `Reflect.construct()` method to create a new instance of the `Person` class based on the data provided. The first argument is the constructor function, and the second argument is an array of arguments to pass to the constructor.

### 4. Modifying Type Information

We can also use the `Reflect` object to modify the type information of an object at runtime:

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

const person = new Person('John', 30);

Reflect.defineProperty(person, 'address', {
  value: {
    city: 'New York',
    state: 'NY'
  }
});

console.log(person); // Person { name: 'John', age: 30, address: { city: 'New York', state: 'NY' } }
```

In this example, we're using the `Reflect.defineProperty()` method to add a new property called `address` to the `person` object. This method takes three arguments: the object to modify, the name of the property, and an object representing the property descriptor.

## Additional Information

TypeScript's reflection capabilities are based on ECMAScript's Reflect API, which is supported by all modern browsers and Node.js. However, the Reflect API is not a complete replacement for traditional runtime type checking, as it only provides access to the type information that is available at runtime.

## Conclusion

Type Reflection is a powerful feature of TypeScript that allows us to inspect and manipulate the type information of an object at runtime. With Type Reflection, we can create more flexible and maintainable code that adapts to changing requirements. By using the `Reflect` object and its methods, we can inspect object properties, determine object types, create new instances of objects, and modify type information at runtime. This makes TypeScript a great choice for building complex applications that require runtime type checking and manipulation.

## External Resources

- [TypeScript Handbook: Type Reflection](https://www.typescriptlang.org/docs/handbook/2/objects.html#type-reflection)
- [MDN Web Docs: Reflect](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Reflect)