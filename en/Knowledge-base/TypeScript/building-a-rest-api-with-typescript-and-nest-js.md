---
title: Building a REST API with TypeScript and Nest.js
description: 
published: true
date: 2023-02-17T18:12:52.705Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:44:00.603Z
---

- [TypeScript 및 Nest.js로 REST API 빌드***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}
- [TypeScript と Nest.js を使用して REST API を構築する***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}
- [使用 TypeScript 和 Nest.js 构建 REST API***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/building-a-rest-api-with-typescript-and-nest-js)
{.links-list}


# Building a REST API with TypeScript and Nest.js

Nest.js is a Node.js framework for building efficient, scalable, and enterprise-grade server-side applications on top of TypeScript and JavaScript (ES6, 7, 8). 

## Why use Nest.js?

There are many reasons why you might want to use Nest.js for building your REST API. 

Nest.js is built on TypeScript, and thus benefits from all of TypeScript's benefits, including static type-checking. This is in contrast to JavaScript, which is dynamically typed. 

In addition, Nest.js leverages the JavaScript Express framework. Express is a fast, unopinionated, minimalist web framework for Node.js. By using Express, Nest.js can take advantage of the numerous Express plugins and middlewares that are available. 

Nest.js is also very modular. The Nest.js architecture is based on the CRNA (Common Root Name Architecture). This architecture enables each module in Nest.js to be used independently of each other. 

## The benefits of using TypeScript

As Nest.js is built on TypeScript, it benefits from all of TypeScript's features. TypeScript is a superset of JavaScript that adds optional static types to your code. 

The benefits of using TypeScript over JavaScript include: 

- TypeScript is a superset of JavaScript, which means that any valid JavaScript code is also valid TypeScript code. This makes it easy for JavaScript developers to get started with TypeScript. 

- TypeScript code is compiled to JavaScript, which means that it runs in any JavaScript environment. This makes it easy to deploy TypeScript code to servers or web browsers. 

- TypeScript is statically typed. This means that the TypeScript compiler can check for errors in your code before it is executed. This can help to prevent errors from being introduced into your code. 

- The TypeScript compiler can generate JavaScript code that is compatible with older versions of JavaScript. This is known as "targeting" a specific JavaScript version. This can be helpful when you need to support older browsers or servers. 

- TypeScript comes with its own type definition files. These files can be used to give TypeScript information about the types of values that are expected in your code. This is especially helpful when using third-party libraries that are written in JavaScript. 

## Installing TypeScript and Nest.js

In order to use TypeScript and Nest.js, you need to install them. The TypeScript compiler can be installed using the npm package manager. 

```
npm install -g typescript
```

The Nest.js framework can be installed using the npm package manager. 

```
npm install -g @nestjs/cli
```

## Using TypeScript with Nest.js

Nest.js uses TypeScript as its programming language. This means that you need to use TypeScript when developing Nest.js applications. 

TypeScript is a superset of JavaScript. This means that any valid JavaScript code is also valid TypeScript code. TypeScript adds optional static types to your code. 

The benefits of using TypeScript over JavaScript include: 

- TypeScript is statically typed. This means that the TypeScript compiler can check for errors in your code before it is executed. This can help to prevent errors from being introduced into your code. 

- The TypeScript compiler can generate JavaScript code that is compatible with older versions of JavaScript. This is known as "targeting" a specific JavaScript version. This can be helpful when you need to support older browsers or servers. 

- TypeScript comes with its own type definition files. These files can be used to give TypeScript information about the types of values that are expected in your code. This is especially helpful when using third-party libraries that are written in JavaScript. 

Nest.js uses the TypeScript language throughout its codebase. This means that you need to be familiar with TypeScript in order to use Nest.js effectively. 

If you are not familiar with TypeScript, you can check out the TypeScript tutorial on the TypeScript website. 

## Creating a Nest.js Application

Now that you have TypeScript and Nest.js installed, you can create a Nest.js application. 

The Nest.js CLI can be used to create a new Nest.js application. 

```
nest new my-api
```

This will create a new Nest.js application in a directory called "my-api". 

## Defining Routes

Routes are defined in the Nest.js router. The router is a module that is used to define the routes for an application. 

A route is defined by a path and a handler function. The path is a string that is used to match the URL of an incoming request. The handler function is used to process the incoming request and generate a response. 

In Nest.js, routes are defined in the file ```app.routing.ts```. 

```typescript
import { ModuleWithProviders, RouterModule, Routes } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

const routes: Routes = [
  { path: '/', controller: AppController, method: 'get' },
];

export const AppRoutingModule: ModuleWithProviders = RouterModule.forRoot(routes);
```

In the code above, a route is defined for the path ```/```. This route will match the URL ```/``` and will use the ```AppController``` to handle the request. 

The ```AppController``` is a Nest.js controller. Controllers are responsible for handling requests and generating responses. 

```typescript
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

In the code above, the ```AppController``` is annotated with the ```@Controller``` decorator. This decorator tells Nest.js that this class is a controller. 

The ```AppController``` has a single route handler. This handler is annotated with the ```@Get``` decorator. This decorator tells Nest.js that this handler will process GET requests. 

The ```getHello()``` handler is a simple handler that returns the string "Hello World!". 

## Defining Services

Services are used to encapsulate business logic in Nest.js applications. Services are injected into controllers and are used to process requests and generate responses. 

Services are defined in the file ```app.service.ts```. 

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

In the code above, the ```AppService``` is annotated with the ```@Injectable``` decorator. This decorator tells Nest.js that this class is a service. 

The ```AppService``` has a single method, ```getHello()```. This method returns the string "Hello World!". 

## Injecting Services

Services are injected into controllers using the ```@Inject()``` decorator. 

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(
    @Inject('APP_SERVICE')
    private readonly appService: AppService,
  ) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

In the code above, the ```AppService``` is injected into the ```AppController``` using the ```@Inject()``` decorator. The ```@Inject()``` decorator takes a service token as a parameter. The service token is used to identify the service that is being injected. 

The ```@Inject()``` decorator can be used to inject services into controller methods as well as controller constructor methods. 

## Running the Application

The Nest.js CLI can be used to run the application. 

```
nest start
```

This will start the Nest.js application on port 3000.