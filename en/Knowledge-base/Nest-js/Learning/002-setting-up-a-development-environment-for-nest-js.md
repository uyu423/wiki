---
title: 002: Setting up a development environment for Nest.js
description: 
published: true
date: 2023-02-14T14:32:36.570Z
tags: 
editor: markdown
dateCreated: 2023-02-14T14:32:28.924Z
---

- [002: Configuración de un entorno de desarrollo para Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}
- [002: 为 Nest.js 设置开发环境***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}
- [002: Nest.js용 개발 환경 설정***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}


# Setting up a development environment for Nest.js

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (https://www.typescriptlang.org/) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

## Prerequisites

Before you begin, make sure you have the following installed on your development machine:

* Node.js (https://nodejs.org/en/)
* TypeScript (https://www.typescriptlang.org/)
* A code editor like Visual Studio Code (https://code.visualstudio.com/)

## Create a new Nest.js project

Open a terminal and create a new Nest.js project by running the following command:

```
nest new <project name>
```

This will create a new directory with the project name and initializes the project with a basic Nest.js structure.

## Start the Nest.js server

Navigate to the newly created project directory and run the following command to start the Nest.js server:

```
npm run start
```

This will start the Nest.js server on http://localhost:3000 by default. You can change the port number by setting the `PORT` environment variable.

## Create a new Nest.js controller

Now that the Nest.js server is up and running, let's create a new controller. In the project root directory, create a new directory named `controllers` and a new file named `<controller name>.controller.ts` within it.

The controller file should look like this:

```typescript
import { Controller } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {}
```

Replace `<controller path>` with the path you want the controller to be accessible at and `<Controller Name>` with the name of the controller.

## Create a new Nest.js route

Within the controller file, create a new route by adding the following:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {

  @Get()
  getHello(): string {
    return 'Hello World!';
  }

}
```

The `@Get()` decorator defines the `getHello()` method as a GET route. You can also define POST, PUT, and DELETE routes using the `@Post()`, `@Put()`, and `@Delete()` decorators respectively.

## Test the Nest.js route

Open http://localhost:3000/<controller path> in a web browser and you should see the `Hello World!` message.

## Conclusion

In this tutorial, you've learned how to set up a development environment for Nest.js and create a new Nest.js controller with a route.