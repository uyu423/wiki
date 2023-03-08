---
title: 003: Creating your first Nest.js application
description: 
published: true
date: 2023-02-14T15:34:21.356Z
tags: 
editor: markdown
dateCreated: 2023-02-14T15:34:13.204Z
---

- [003: Creando tu primera aplicación Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}
- [003：创建你的第一个 Nest.js 应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}
- [003: 첫 번째 Nest.js 애플리케이션 만들기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}


# Creating your first Nest.js application

This guide will walk you through the steps of creating your first Nest.js application. Nest.js is a framework for building Node.js applications. It is based on Express.js and uses TypeScript, which is a superset of JavaScript.

## Prerequisites

Before you begin, you will need to have the following installed on your machine:

- Node.js
- npm
- TypeScript

## Getting started

First, create a new directory for your project. Then, initialize your project by running the following command:

```
npm init
```

This will create a `package.json` file in your project directory. Next, you need to install the Nest.js framework. You can do this by running the following command:

```
npm install --save @nestjs/core
```

## Hello world

Now that you have Nest.js installed, you can create your first Nest.js application. Create a new file called `app.ts` in your project directory and add the following code to it:

```typescript
import { NestFactory } from '@nestjs/core';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

This code imports the `NestFactory` class from the `@nestjs/core` package and uses it to create an instance of the `AppModule` class. The `AppModule` class is a Nest.js module. Nest.js modules are used to organize your code.

Next, the code calls the `listen()` method on the `app` object. This tells the Nest.js application to start listening for incoming HTTP requests on port 3000.

## Conclusion

In this guide, you have created your first Nest.js application. You have also learned about some of the key concepts in Nest.js, such as modules and the NestFactory class.