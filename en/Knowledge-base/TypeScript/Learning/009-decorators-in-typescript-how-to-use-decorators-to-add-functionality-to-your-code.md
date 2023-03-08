---
title: 009: Decorators in TypeScript: How to Use Decorators to Add Functionality to Your Code
description: 
published: true
date: 2023-03-07T04:32:40.095Z
tags: 
editor: markdown
dateCreated: 2023-03-07T04:32:38.725Z
---

- [009: TypeScript의 데코레이터: 데코레이터를 사용하여 코드에 기능을 추가하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/009-decorators-in-typescript-how-to-use-decorators-to-add-functionality-to-your-code)
{.links-list}



Decorators in TypeScript: How to Use Decorators to Add Functionality to Your Code

If you're a TypeScript developer, you've probably heard of decorators. Decorators are a powerful feature that allow you to add functionality to your code without modifying the original code. In this post, we'll explore what decorators are, how to use them, and some practical examples.

### What are Decorators?

Decorators are a design pattern that allows you to add functionality to an object or a function at runtime. They are similar to annotations in Java and attributes in C#. Decorators are a language feature that is available in TypeScript and is also being proposed for ECMAScript.

In TypeScript, decorators are functions that can be applied to classes, methods, properties, and parameters. When a decorator is applied to a class, it receives the constructor function of the class as its only argument. When a decorator is applied to a method, property, or parameter, it receives the target object, the name of the method, property or parameter, and optionally the descriptor of the method, property, or parameter.

### How to Use Decorators?

To use decorators in TypeScript, you need to enable the `experimentalDecorators` flag in your `tsconfig.json` file. Here's an example:

```json
{
  "compilerOptions": {
    "experimentalDecorators": true
  }
}
```

Once you have enabled the `experimentalDecorators` flag, you can start using decorators in your code.

### Practical Examples

#### Class Decorators

Let's start with an example of a class decorator. Suppose we have a class `Person`:

```typescript
class Person {
  constructor(public name: string) {}
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

We can add a decorator to this class that logs the name of the class:

```typescript
function logName(constructor: Function) {
  console.log(`Class name: ${constructor.name}`);
}

@logName
class Person {
  constructor(public name: string) {}
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

When we create an instance of the `Person` class, we will see the following output in the console:

```
Class name: Person
```

#### Method Decorators

Now let's look at an example of a method decorator. Suppose we have a class `Calculator`:

```typescript
class Calculator {
  add(a: number, b: number) {
    return a + b;
  }
}
```

We can add a decorator to the `add` method that logs the arguments and return value of the method:

```typescript
function logMethod(target: any, methodName: string, descriptor: PropertyDescriptor) {
  const originalMethod = descriptor.value;
  descriptor.value = function(...args: any[]) {
    const result = originalMethod.apply(this, args);
    console.log(`Method ${methodName} called with arguments ${JSON.stringify(args)} and returned ${result}`);
    return result;
  }
  return descriptor;
}

class Calculator {
  @logMethod
  add(a: number, b: number) {
    return a + b;
  }
}
```

When we call the `add` method, we will see the following output in the console:

```
Method add called with arguments [1,2] and returned 3
```

#### Property Decorators

Finally, let's look at an example of a property decorator. Suppose we have a class `Person`:

```typescript
class Person {
  @readonly
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

We can add a decorator to the `name` property that makes it read-only:

```typescript
function readonly(target: any, propertyName: string) {
  Object.defineProperty(target, propertyName, {
    writable: false
  });
}

class Person {
  @readonly
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

When we try to modify the `name` property, we will get a runtime error:

```typescript
const person = new Person('Alice');
person.name = 'Bob'; // runtime error: Cannot assign to read only property 'name' of object '#<Person>'
```

### Conclusion

Decorators are a powerful feature that can help you add functionality to your code in a clean and modular way. In this post, we've explored what decorators are, how to use them, and some practical examples. If you're interested in learning more, check out the external resources below.

### External Resources

- [TypeScript Handbook: Decorators](https://www.typescriptlang.org/docs/handbook/decorators.html)
- [ECMAScript proposal: Decorators](https://github.com/tc39/proposal-decorators)