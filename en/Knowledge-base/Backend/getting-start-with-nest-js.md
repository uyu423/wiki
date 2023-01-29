---
title: Getting Start with Nest.js
description: 
published: true
date: 2023-01-29T19:21:38.104Z
tags: 
editor: markdown
dateCreated: 2023-01-29T19:21:38.104Z
---


Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (that compiles to JavaScript) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

If you have built a Node.js API before, chances are you have used Express. Nest.js builds on top of Express and offers a different way of structuring APIs. In this blog post, we will take a look at how to get started with Nest.js and some of its key concepts.

## Setting up a Nest.js project

The first thing you need to do is install the Nest.js CLI. This will allow you to create new Nest.js projects and generate the necessary files.

```
npm i -g @nestjs/cli
```

Once the Nest.js CLI is installed, you can create a new project using the `nest new` command. This will create a new directory with the necessary files for a Nest.js project.

```
nest new my-project
```

## The Nest.js architecture

Nest.js applications are organized into modules. Modules are like mini-apps within a Nest.js application. Each module can have its own controllers, services, providers, pipes, filters, and middleware.

Modules are a great way to organize your code and keep your project clean and organized. Nest.js also has the concept of shared modules. Shared modules are modules that can be imported into other modules and used across the application.

## Controllers

Controllers are responsible for handling incoming requests and sending responses. In Nest.js, controllers are annotated with the `@Controller()` decorator.

```typescript
@Controller('/todos')
export class TodosController {

}
```

The `@Controller()` decorator accepts a path as an argument. This is the path that the controller will be accessible at. In the example above, the `TodosController` will be accessible at `/todos`.

## Services

Services are responsible for encapsulating business logic. In Nest.js, services are annotated with the `@Injectable()` decorator.

```typescript
@Injectable()
export class TodosService {

}
```

Services can be injected into controllers using the `@Inject()` decorator.

```typescript
@Controller('/todos')
export class TodosController {

  constructor(private readonly todosService: TodosService) {}

}
```

## Routes

Routes are responsible for mapping incoming requests to specific controller methods. In Nest.js, routes are annotated with the `@Controller()` decorator.

```typescript
@Controller('/todos')
export class TodosController {

  @Get('/')
  public getTodos() {
    // ...
  }

}
```

In the example above, the `getTodos()` method will be invoked when a `GET` request is made to `/todos`.

## Dependency Injection

Dependency Injection (DI) is a design pattern that Nest.js makes use of heavily. DI allows developers to inject dependencies into their classes. This is done by annotating constructor parameters with the `@Inject()` decorator.

```typescript
@Controller('/todos')
export class TodosController {

  constructor(private readonly todosService: TodosService) {}

}
```

In the example above, the `TodosService` is injected into the `TodosController` via the constructor. Nest.js will automatically resolve and inject the `TodosService` when the `TodosController` is instantiated.

## Conclusion

In this blog post, we have looked at how to get started with Nest.js. We have also looked at some of its key concepts, such as modules, controllers, services, and dependency injection. Nest.js is a great framework for building Node.js server-side applications.