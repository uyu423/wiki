---
title: 001: An Introduction to TypeScript: Getting Started with Strongly Typed JavaScript
description: 
published: true
date: 2023-03-02T08:40:46.552Z
tags: 
editor: markdown
dateCreated: 2023-03-02T08:40:46.552Z
---

- [001: TypeScript 소개: 강력한 형식의 JavaScript 시작하기***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/001-an-introduction-to-typescript-getting-started-with-strongly-typed-javascript)
{.links-list}


Introduction

Have you ever written JavaScript code and wished you could catch some errors before running the code? Do you want to write more scalable and maintainable code in JavaScript? If yes, then TypeScript might be the solution you are looking for. TypeScript is a superset of JavaScript that adds optional static typing and other features to the language. In this post, we'll cover the basics of TypeScript and how to get started with it.

What is TypeScript?

TypeScript is a programming language developed and maintained by Microsoft. It is a superset of JavaScript, which means that any valid JavaScript code is also valid TypeScript code. TypeScript adds optional static typing to JavaScript, which allows for catching errors at compile-time instead of runtime. It also adds features like classes, interfaces, modules, and more.

Getting Started with TypeScript

To get started with TypeScript, you need to install the TypeScript compiler. You can do this using npm, which is a package manager for Node.js. Open your terminal or command prompt and execute the following command:

```npm install -g typescript```

This command installs the TypeScript compiler globally on your machine. To check if the installation was successful, run the following command:

```tsc --version```

This command should output the version number of the TypeScript compiler.

Creating a TypeScript File

To create a TypeScript file, you need to create a file with the `.ts` extension. Let's create a file called `app.ts` and add the following code:

```
function greet(name: string) {
    console.log("Hello, " + name);
}

greet("TypeScript");
```

In this code, we define a function called `greet` that takes a string parameter called `name`. The `: string` syntax after the parameter name indicates that the parameter is of type `string`. We then call the `greet` function with the string "TypeScript".

Compiling a TypeScript File

To compile the `app.ts` file, run the following command in your terminal or command prompt:

```tsc app.ts```

This command compiles the TypeScript code into JavaScript code and creates a file called `app.js`. You can now run the `app.js` file using Node.js by executing the following command:

```node app.js```

This command should output "Hello, TypeScript" in your terminal or command prompt.

TypeScript Types

TypeScript adds several types to JavaScript, including:

- `string`: represents a string value
- `number`: represents a numeric value
- `boolean`: represents a boolean value (true or false)
- `any`: represents any type (similar to JavaScript's dynamic typing)
- `void`: represents the absence of any type (usually used for functions that don't return a value)
- `null` and `undefined`: represent null and undefined values respectively
- `object`: represents any non-primitive type (e.g. arrays, functions, objects, etc.)
- `array`: represents an array of values of a specific type

Let's look at some examples of using these types in TypeScript:

```
let name: string = "John";
let age: number = 30;
let isMarried: boolean = true;
let anything: any = "anything";
let nothing: void = undefined;
let nothing2: void = null;
let obj: object = { name: "John", age: 30 };
let nums: number[] = [1, 2, 3];
```

In this code, we define variables of different types, including `string`, `number`, `boolean`, `any`, `void`, `object`, and `array`.

TypeScript Interfaces

TypeScript interfaces allow you to define the structure of an object. You can define an interface using the `interface` keyword, followed by the name of the interface and the properties it should have. Let's look at an example:

```
interface Person {
    name: string;
    age: number;
    isMarried?: boolean;
}

function greet(person: Person) {
    console.log("Hello, " + person.name);
}

let john: Person = { name: "John", age: 30 };
greet(john);
```

In this code, we define an interface called `Person` that has three properties: `name` of type `string`, `age` of type `number`, and `isMarried` of type `boolean` (optional). We then define a function called `greet` that takes a parameter of type `Person` and logs a greeting to the console. We create an object called `john` that matches the `Person` interface and call the `greet` function with the `john` object.

TypeScript Classes

TypeScript classes allow you to define blueprints for objects. You can define a class using the `class` keyword, followed by the name of the class and the properties and methods it should have. Let's look at an example:

```
class Person {
    name: string;
    age: number;
    isMarried?: boolean;

    constructor(name: string, age: number, isMarried?: boolean) {
        this.name = name;
        this.age = age;
        this.isMarried = isMarried;
    }

    greet() {
        console.log("Hello, " + this.name);
    }
}

let john: Person = new Person("John", 30);
john.greet();
```

In this code, we define a class called `Person` that has three properties: `name` of type `string`, `age` of type `number`, and `isMarried` of type `boolean` (optional). We also define a constructor that takes three parameters and assigns them to the properties of the class. We define a method called `greet` that logs a greeting to the console. We create an object called `john` using the `new` keyword and call the `greet` method on it.

Additional Information

- TypeScript is open source and is actively maintained by Microsoft and the community.
- TypeScript can be used with various IDEs and editors, including Visual Studio Code, WebStorm, and Atom.
- TypeScript can be used to write frontend and backend code, as well as Node.js applications.

Conclusion

In this post, we covered the basics of TypeScript and how to get started with it. We looked at creating a TypeScript file, compiling it, and running it. We also looked at TypeScript types, interfaces, and classes. TypeScript is a powerful tool that can help you write more scalable and maintainable code in JavaScript. If you are interested in learning more about TypeScript, be sure to check out the official TypeScript documentation and other resources listed below.

External Resources

- Official TypeScript Documentation: https://www.typescriptlang.org/docs/
- TypeScript Playground: https://www.typescriptlang.org/play
- TypeScript Deep Dive: https://basarat.gitbook.io/typescript/
- TypeScript Handbook: https://www.typescriptlang.org/docs/handbook/