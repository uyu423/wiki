---
title: 032: Using Nest.js with TypeScript
description: 
published: true
date: 2023-02-12T09:55:40.051Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:55:32.037Z
---

- [032: Uso de Nest.js con TypeScript***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}
- [032：将 Nest.js 与 TypeScript 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}
- [032: TypeScript와 함께 Nest.js 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}


# Using Nest.js with TypeScript

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses TypeScript, a typed superset of JavaScript that compiles to plain JavaScript.

In this post, we'll show you how to use Nest.js with TypeScript. We'll go through the steps of setting up a Nest.js project, configuring TypeScript, and writing a simple controller.

## Setting up a Nest.js project

First, let's create a new Nest.js project. We'll use the Nest CLI to generate a project skeleton:

```
$ nest new project-name
```

This will create a new directory called `project-name` with the following structure:

```
project-name
├── README.md
├── node_modules
├── package-lock.json
├── package.json
├── tsconfig.json
└── tslint.json
```

Next, let's install the dependencies for our project:

```
$ cd project-name
$ npm install
```

## Configuring TypeScript

Nest.js uses TypeScript by default, so we don't need to install it separately. However, we do need to configure it.

Open `tsconfig.json` and add the following options:

```js
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "strict": true
  }
}
```

These options will compile our TypeScript code to ES6, and use the CommonJS module format. The `outDir` option specifies the output directory for the compiled JavaScript files. And the `strict` option enables strict type checking.

## Writing a controller

Now that our project is set up, we can write a controller. Controllers are responsible for handling HTTP requests and returning responses.

Let's create a file called `src/controllers/hello.controller.ts`:

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('hello')
export class HelloController {
  @Get()
  public async index(): Promise<string> {
    return 'Hello, world!';
  }
}
```

This controller has a single `@Get` route, which returns the string `'Hello, world!'`.

To register this controller with Nest.js, we need to create a module. Let's create a file called `src/modules/hello.module.ts`:

```ts
import { Module } from '@nestjs/common';
import { HelloController } from '../controllers/hello.controller';

@Module({
  controllers: [HelloController]
})
export class HelloModule {}
```

This module imports the `HelloController` and registers it with Nest.js.

Finally, we need to tell Nest.js to use this module. We can do this by adding it to the `app.module.ts` file:

```ts
import { Module } from '@nestjs/common';
import { HelloModule } from './modules/hello.module';

@Module({
  imports: [HelloModule]
})
export class AppModule {}
```

Now that our controller is registered, we can start the Nest.js server:

```
$ npm start
```

And open http://localhost:3000/hello in your browser. You should see the string `'Hello, world!'`.

## Conclusion

In this post, we've shown you how to use Nest.js with TypeScript. We've set up a Nest.js project, configured TypeScript, and written a simple controller.