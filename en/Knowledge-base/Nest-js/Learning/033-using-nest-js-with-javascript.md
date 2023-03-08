---
title: 033: Using Nest.js with JavaScript
description: 
published: true
date: 2023-02-15T11:32:47.656Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:32:40.172Z
---

- [033: Uso de Nest.js con JavaScript***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}
- [033：将 Nest.js 与 JavaScript 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}
- [033: 자바스크립트로 Nest.js 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}


# Using Nest.js with JavaScript

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (optional) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

Nest.js is a great framework for developers coming from a JavaScript background. It is easy to use and has a familiar syntax. In this post, we will take a look at how to use Nest.js with JavaScript.

## Installation

To install Nest.js, you will need to have Node.js and npm installed on your machine. You can then install Nest.js using the following command:

```
npm install -g @nestjs/cli
```

## Creating a Nest.js Project

Once Nest.js is installed, you can create a new project using the Nest.js CLI. To do so, run the following command:

```
nest new project-name
```

This will create a new Nest.js project with the name you specified.

## project-name/src/app.controller.js

The first file we will take a look at is the app.controller.js file. This is the file where we will define our controllers. A controller is a class that contains one or more methods. Each method is responsible for handling a request.

Let's take a look at a simple controller:

```javascript
import { Controller, Get, Post, Body } from '@nestjs/common';

@Controller('/api/v1/todos')
export class TodosController {
  @Get()
  findAll() {
    return [];
  }

  @Post()
  create(@Body() createTodoDto) {
    return [];
  }
}
```

In the code above, we have defined a controller with two methods: findAll and create. The findAll method is responsible for handling GET requests. The create method is responsible for handling POST requests.

## project-name/src/app.service.js

The next file we will take a look at is the app.service.js file. This is the file where we will define our services. A service is a class that contains business logic.

Let's take a look at a simple service:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class TodosService {
  getAll() {
    return [];
  }

  create(createTodoDto) {
    return [];
  }
}
```

In the code above, we have defined a service with two methods: getAll and create. The getAll method returns all of the todos. The create method creates a new todo.

## project-name/src/app.module.js

The next file we will take a look at is the app.module.js file. This is the file where we will define our modules. A module is a class that contains controllers and services.

Let's take a look at a simple module:

```javascript
import { Module } from '@nestjs/common';
import { TodosController } from './app.controller';
import { TodosService } from './app.service';

@Module({
  controllers: [TodosController],
  providers: [TodosService],
})
export class TodosModule {}
```

In the code above, we have defined a module with a controller and a service. The controller is responsible for handling requests. The service is responsible for business logic.

## project-name/src/main.js

The next file we will take a look at is the main.js file. This is the file where we will start our Nest.js application.

Let's take a look at the code:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

In the code above, we have imported the NestFactory and the AppModule. We have then created a new Nest.js application and started it on port 3000.

## Conclusion

In this post, we have taken a look at how to use Nest.js with JavaScript. We have seen how to install Nest.js and create a new project. We have also seen how to define controllers, services, and modules.