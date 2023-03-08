---
title: 007: Modules in TypeScript: How to Organize Your Code into Modules and Files
description: 
published: true
date: 2023-03-05T05:32:35.182Z
tags: 
editor: markdown
dateCreated: 2023-03-05T05:32:27.986Z
---

- [007: TypeScript의 모듈: 코드를 모듈과 파일로 구성하는 방법***Korean** document is available*](/ko/Knowledge-base/TypeScript/Learning/007-modules-in-typescript-how-to-organize-your-code-into-modules-and-files)
{.links-list}


Modules in TypeScript: How to Organize Your Code into Modules and Files

Are you tired of having all your code in a single file? Do you want to organize it into smaller, more manageable pieces? Look no further than modules in TypeScript! In this post, we'll go over what modules are, how to use them, and how to organize your code into files.

## What are Modules?

Modules are a way of organizing code into separate, reusable components. They allow you to break your code into smaller pieces, making it easier to manage and maintain. In TypeScript, modules are defined using the `export` keyword.

### Exporting a Module

To export a module, you simply need to prefix the module with the `export` keyword. For example, let's say we have a module called `math.ts` that contains a function to add two numbers:

```typescript
export function add(a: number, b: number): number {
  return a + b;
}
```

We can then import this module into another file using the `import` keyword:

```typescript
import { add } from './math';
```

### Default Exports

In addition to named exports, TypeScript also supports default exports. A default export is a single export that is the "default" export for a module. For example, let's say we have a module called `foo.ts` that exports a default function:

```typescript
export default function() {
  console.log('Hello, world!');
}
```

We can then import this module into another file using the `import` keyword, without needing to specify a name:

```typescript
import foo from './foo';
```

### Re-Exporting Modules

Sometimes, you may want to re-export a module from another module. This can be useful for creating a "public API" for your module. To re-export a module, you can use the `export` keyword with the `*` symbol:

```typescript
export * from './math';
```

This will export all named exports from the `math` module.

## Organizing Code into Files

Now that we know how to export modules, let's talk about how to organize our code into files. In general, you should aim to organize your code into files based on functionality. For example, if you have a module for handling user authentication, you might want to put that in a file called `auth.ts`.

### File Naming Conventions

When organizing your code into files, it's important to follow some naming conventions to make it easier to find and manage your code. Here are some common naming conventions:

- Use lowercase file names.
- Use hyphens to separate words in file names (e.g. `user-authentication.ts`).
- Use a descriptive name that reflects the module's purpose.

### Folder Structure

In addition to naming conventions, you should also consider the folder structure of your code. Here are some tips for organizing your code into folders:

- Use a separate folder for each major feature or component of your application.
- Use subfolders to organize related modules.
- Avoid nesting folders too deeply.

Here's an example folder structure for a simple web application:

```
src/
  index.ts
  app/
    app.ts
    routes.ts
    components/
      header.ts
      footer.ts
    auth/
      auth.ts
      login.ts
      register.ts
  utils/
    math.ts
```

## Conclusion

Modules are a powerful tool for organizing your code into reusable components. By using modules, you can break your code into smaller, more manageable pieces, making it easier to maintain and scale. Remember to follow naming conventions and consider your folder structure when organizing your code into files.

### Additional Information

- TypeScript documentation on Modules: https://www.typescriptlang.org/docs/handbook/modules.html

### External Resources

- "Organizing Your React Codebase with Modules" by Tyler McGinnis: https://ui.dev/organizing-your-react-codebase-with-es6-modules/
- "Modular JavaScript: A Beginner's Guide to Modules" by Jonathan Saring: https://www.sitepoint.com/javascript-modules-beginners-guide/