---
title: 035: Namespaces vs. Modules in TypeScript: Understanding the Differences and When to Use Each
description: 
published: true
date: 2023-03-05T09:32:46.175Z
tags: 
editor: markdown
dateCreated: 2023-03-05T09:32:38.739Z
---

- [035: TypeScript의 네임스페이스 대 모듈: 차이점 이해 및 사용 시기***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/035-namespaces-vs-modules-in-typescript-understanding-the-differences-and-when-to-use-each)
{.links-list}



Introduction

TypeScript is a popular programming language that is known for its ability to compile to JavaScript. It has a lot of features that make it a great choice for building large-scale applications. One of these features is the ability to use namespaces and modules. In this post, we will explore the differences between namespaces and modules in TypeScript and when to use each.

Namespaces in TypeScript

Namespaces in TypeScript are used to group related code together. They are similar to modules, but they are not the same thing. Namespaces are declared using the `namespace` keyword.

### Declaring a Namespace

To declare a namespace in TypeScript, we use the `namespace` keyword followed by the name of the namespace. Here is an example:

```typescript
namespace MyNamespace {
  export function myFunction() {
    console.log("Hello from MyNamespace");
  }
}
```

In this example, we have declared a namespace called `MyNamespace` that contains a function called `myFunction`. The `export` keyword is used to make the function available outside of the namespace.

### Using a Namespace

To use a namespace, we simply reference it by its name. Here is an example:

```typescript
MyNamespace.myFunction();
```

In this example, we are calling the `myFunction` function that is defined in the `MyNamespace` namespace.

### Advantages of Namespaces

Namespaces can be useful for organizing code into logical groups. They can also help to prevent naming conflicts between different parts of an application.

Modules in TypeScript

Modules in TypeScript are used to encapsulate code and prevent naming conflicts. They are similar to namespaces, but they are designed to work with external code. Modules are declared using the `module` keyword.

### Declaring a Module

To declare a module in TypeScript, we use the `module` keyword followed by the name of the module. Here is an example:

```typescript
module MyModule {
  export function myFunction() {
    console.log("Hello from MyModule");
  }
}
```

In this example, we have declared a module called `MyModule` that contains a function called `myFunction`. The `export` keyword is used to make the function available outside of the module.

### Using a Module

To use a module, we need to import it into our code. Here is an example:

```typescript
import { MyModule } from "./my-module";

MyModule.myFunction();
```

In this example, we are importing the `MyModule` module from a file called `my-module.ts`. We can then call the `myFunction` function that is defined in the `MyModule` module.

### Advantages of Modules

Modules can be useful for encapsulating code and preventing naming conflicts. They can also be used to break up large applications into smaller, more manageable pieces.

### Differences Between Namespaces and Modules

The main difference between namespaces and modules is that namespaces are designed to work with internal code, while modules are designed to work with external code. Namespaces are useful for organizing code into logical groups and preventing naming conflicts within an application. Modules are useful for encapsulating code and preventing naming conflicts between different parts of an application.

### When to Use Namespaces

Namespaces are useful when we need to organize code into logical groups and prevent naming conflicts within an application. They are also useful when we need to work with internal code that is not going to be used by external applications.

### When to Use Modules

Modules are useful when we need to encapsulate code and prevent naming conflicts between different parts of an application. They are also useful when we need to work with external code that is going to be used by other applications.

### Additional Information

When using namespaces and modules in TypeScript, it is important to choose the right tool for the job. If we need to work with internal code, namespaces are a good choice. If we need to work with external code, modules are a better choice.

### Warnings

Using too many namespaces or modules can make our code difficult to manage. It is important to use them sparingly and only when necessary.

### Dangers

Using namespaces or modules incorrectly can lead to naming conflicts and other issues. It is important to understand how they work before using them in our code.

Conclusion

In this post, we have explored the differences between namespaces and modules in TypeScript and when to use each. We have seen that namespaces are useful for organizing code into logical groups and preventing naming conflicts within an application, while modules are useful for encapsulating code and preventing naming conflicts between different parts of an application. By choosing the right tool for the job, we can write clean, maintainable code that is easy to manage.

External Resources

- [TypeScript Documentation: Namespaces](https://www.typescriptlang.org/docs/handbook/namespaces.html)
- [TypeScript Documentation: Modules](https://www.typescriptlang.org/docs/handbook/modules.html)