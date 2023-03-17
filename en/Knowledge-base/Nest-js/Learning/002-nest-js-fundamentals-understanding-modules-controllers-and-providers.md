---
title: 002: Nest.js Fundamentals: Understanding Modules, Controllers, and Providers
description: 
published: true
date: 2023-03-17T19:27:24.068Z
tags: 
editor: markdown
dateCreated: 2023-03-17T19:27:24.068Z
---

- [002: Nest.js 기초: 모듈, 컨트롤러 및 공급자 이해***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/002-nest-js-fundamentals-understanding-modules-controllers-and-providers)
{.links-list}

Welcome to the second post in our series on Nest.js fundamentals! In this post, we'll dive deeper into the core concepts of Nest.js, specifically focusing on **Modules**, **Controllers**, and **Providers**. By the end of this post, you should have a solid understanding of how these building blocks work together to create a well-structured and scalable Nest.js application.

## Table of Contents

- [Introduction to Nest.js](#introduction-to-nestjs)
- [Understanding Modules](#understanding-modules)
  - [Creating a Module](#creating-a-module)
  - [Importing and Exporting Modules](#importing-and-exporting-modules)
- [Understanding Controllers](#understanding-controllers)
  - [Creating a Controller](#creating-a-controller)
  - [Defining Routes](#defining-routes)
  - [Using Request and Response Objects](#using-request-and-response-objects)
- [Understanding Providers](#understanding-providers)
  - [Creating a Provider](#creating-a-provider)
  - [Injecting Providers](#injecting-providers)
- [Conclusion](#conclusion)
- [Additional Resources](#additional-resources)

## Introduction to Nest.js

Nest.js is a powerful framework for building efficient, scalable, and maintainable server-side applications. It is built on top of Node.js and is heavily inspired by Angular. Nest.js provides a set of abstractions and conventions that make it easy to structure your code and manage dependencies, making it an excellent choice for large-scale applications and teams.

In the previous post, we covered the basics of setting up a Nest.js application and creating a simple RESTful API. In this post, we will explore the core building blocks of Nest.js in more detail, focusing on **Modules**, **Controllers**, and **Providers**.

## Understanding Modules

Modules are the fundamental building blocks of Nest.js applications. They allow you to organize your code into logical units, making it easier to manage and scale your application as it grows. A module is simply a class annotated with the `@Module()` decorator, which provides metadata about the module, such as its imports, exports, controllers, and providers.

### Creating a Module

To create a new module, simply create a new TypeScript file and define a class annotated with the `@Module()` decorator. For example, let's create a module for managing users:

```typescript
import { Module } from '@nestjs/common';

@Module({
  controllers: [],
  providers: [],
})
export class UsersModule {}
```

In this example, we've created a new module called `UsersModule`. The `@Module()` decorator takes an object with the following properties:

- `controllers`: An array of controllers that belong to this module.
- `providers`: An array of providers that belong to this module.
- `imports`: An array of other modules that this module depends on.
- `exports`: An array of providers that should be available to other modules that import this module.

For now, we've left the `controllers` and `providers` arrays empty, but we'll fill them in as we progress through this post.

### Importing and Exporting Modules

Modules can import other modules to gain access to their exported providers. This allows you to create a modular and decoupled architecture, where each module is responsible for a specific feature or domain.

To import a module, simply add it to the `imports` array of your module's `@Module()` decorator. For example, let's say we have a `DatabaseModule` that exports a `DatabaseService` provider. We can import this module in our `UsersModule` like so:

```typescript
import { Module } from '@nestjs/common';
import { DatabaseModule } from './database.module';

@Module({
  imports: [DatabaseModule],
  controllers: [],
  providers: [],
})
export class UsersModule {}
```

Now, we have access to the `DatabaseService` provider within our `UsersModule`. Note that we don't need to explicitly import the `DatabaseService` class itself; the `DatabaseModule` takes care of that for us.

To export a provider from a module, simply add it to the `exports` array of your module's `@Module()` decorator. This makes the provider available to other modules that import your module. For example, let's say we want to make our `DatabaseService` available to other modules:

```typescript
import { Module } from '@nestjs/common';
import { DatabaseService } from './database.service';

@Module({
  providers: [DatabaseService],
  exports: [DatabaseService],
})
export class DatabaseModule {}
```

Now, any module that imports the `DatabaseModule` will have access to the `DatabaseService` provider.

## Understanding Controllers

Controllers are responsible for handling incoming HTTP requests and returning responses. They define the routes for your application and contain the logic for processing requests and returning data to the client.

### Creating a Controller

To create a new controller, simply create a new TypeScript file and define a class annotated with the `@Controller()` decorator. The `@Controller()` decorator takes a single argument, which is the base path for the routes defined in this controller. For example, let's create a controller for managing users:

```typescript
import { Controller } from '@nestjs/common';

@Controller('users')
export class UsersController {}
```

In this example, we've created a new controller called `UsersController` with a base path of `/users`. This means that any routes we define in this controller will be prefixed with `/users`.

Next, let's register our new controller in our `UsersModule`. Simply add the controller class to the `controllers` array of your module's `@Module()` decorator:

```typescript
import { Module } from '@nestjs/common';
import { UsersController } from './users.controller';

@Module({
  controllers: [UsersController],
  providers: [],
})
export class UsersModule {}
```

Now, our `UsersController` is registered with Nest.js and ready to handle incoming requests.

### Defining Routes

To define a route in a controller, simply create a method on your controller class and annotate it with one of the following decorators:

- `@Get()`
- `@Post()`
- `@Put()`
- `@Delete()`
- `@Patch()`

These decorators correspond to the HTTP methods (GET, POST, PUT, DELETE, and PATCH), and they take a single argument, which is the path for the route. The path is relative to the base path defined in the `@Controller()` decorator.

For example, let's define a simple route for fetching all users:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('users')
export class UsersController {
  @Get()
  findAll(): string {
    return 'This action returns all users';
  }
}
```

In this example, we've created a new method called `findAll()` and annotated it with the `@Get()` decorator. Since we did not provide a path argument, the route will be available at the base path of our controller, which in this case is `/users`.

### Using Request and Response Objects

Nest.js automatically handles converting your method's return value into an HTTP response. By default, it will set the response status code to 200 and the content type to `application/json`. If your method returns an object or an array, Nest.js will automatically serialize it to JSON.

However, sometimes you may need more control over the response, such as setting custom headers, status codes, or cookies. In these cases, you can use the `@Res()` decorator to inject the native Express or Fastify response object into your route handler.

For example, let's say we want to return a custom status code and set a cookie when fetching all users:

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';

@Controller('users')
export class UsersController {
  @Get()
  findAll(@Res() res: Response): void {
    res.status(201).cookie('token', '12345').json({ message: 'This action returns all users' });
  }
}
```

In this example, we've injected the native Express `Response` object using the `@Res()` decorator. We can now use the `Response` object's methods to set the status code, set a cookie, and send the JSON response.

## Understanding Providers

Providers are classes that can be used to encapsulate and share logic across your application. They can be injected into your controllers, other providers, and even modules using Nest.js's built-in dependency injection system. Providers are a powerful way to create reusable, testable, and decoupled code.

### Creating a Provider

To create a new provider, simply create a new TypeScript file and define a class. There is no special decorator required for providers; any class can be used as a provider. For example, let's create a provider for managing users:

```typescript
export class UsersService {
  findAll(): string {
    return 'This action returns all users';
  }
}
```

In this example, we've created a new provider called `UsersService` with a single method called `findAll()`.

Next, let's register our new provider in our `UsersModule`. Simply add the provider class to the `providers` array of your module's `@Module()` decorator:

```typescript
import { Module } from '@nestjs/common';
import { UsersController } from './users.controller';
import { UsersService } from './users.service';

@Module({
  controllers: [UsersController],
  providers: [UsersService],
})
export class UsersModule {}
```

Now, our `UsersService` is registered with Nest.js and ready to be injected into our controllers or other providers.

### Injecting Providers

To inject a provider into a controller or another provider, simply add a constructor parameter with the type of the provider you want to inject. Nest.js will automatically handle creating and injecting an instance of the provider for you.

For example, let's inject our `UsersService` into our `UsersController`:

```typescript
import { Controller, Get } from '@nestjs/common';
import { UsersService } from './users.service';

@Controller('users')
export class UsersController {
  constructor(private readonly usersService: UsersService) {}

  @Get()
  findAll(): string {
    return this.usersService.findAll();
  }
}
```

In this example, we've added a constructor to our `UsersController` with a single parameter of type `UsersService`. Nest.js will automatically create an instance of the `UsersService` and inject it into our controller. We can now use the `usersService` to fetch all users in our `findAll()` route handler.

## Conclusion

In this post, we've explored the core building blocks of Nest.js applications: **Modules**, **Controllers**, and **Providers**. We've learned how to create and register these components, as well as how to define routes, handle requests and responses, and inject dependencies.

By understanding these core concepts, you should now have a solid foundation for building scalable and maintainable Nest.js applications. In the next post in this series, we'll dive deeper into Nest.js features, such as middleware, guards, and interceptors.

## Additional Resources

- [Nest.js Official Documentation](https://docs.nestjs.com/)
- [Nest.js GitHub Repository](https://github.com/nestjs/nest)
- [Nest.js CLI](https://github.com/nestjs/nest-cli)
- [Nest.js Courses and Tutorials](https://nestjs.com/resources/courses)