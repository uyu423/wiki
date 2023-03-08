---
title: 038: Building and deploying serverless applications with Nest.js
description: 
published: true
date: 2023-02-12T14:17:57.534Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:17:55.776Z
---

- [038: Creación e implementación de aplicaciones sin servidor con Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}
- [038：使用 Nest.js 构建和部署无服务器应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}
- [038: Nest.js로 서버리스 애플리케이션 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}


# 038: Building and deploying serverless applications with Nest.js

In this post, we'll learn how to build and deploy serverless applications with Nest.js.

Nest.js is a Node.js framework for building scalable server-side applications. It uses modern JavaScript, is built with TypeScript (which provides strong typing), and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

Nest.js is a great choice for building serverless applications. It is lightweight and fast, and it offers a wide range of features, such as support for TypeScript, an easy-to-use dependency injection system, and a powerful module system.

Building a serverless application with Nest.js is quick and easy. In this post, we'll walk through the steps of creating a simple serverless Nest.js application and deploying it to AWS Lambda.

## Creating a Nest.js application

First, we need to create a new Nest.js application. We can use the Nest CLI to generate a new project:

```
nest new serverless-app
```

This will create a new folder called `serverless-app` with the basic files and folders needed for a Nest.js application.

Next, we need to install the `@nestjs/serverless` package. This package provides the necessary modules and dependencies for building a serverless Nest.js application:

```
npm install --save @nestjs/serverless
```

Now that we have the `@nestjs/serverless` package installed, we can create a new serverless Nest.js application.

We'll start by creating a new file called `main.ts` in the `src` folder. This file will be the entry point for our serverless Nest.js application.

In `main.ts`, we need to import the `NestFactory` class from the `@nestjs/core` package. This class will be used to create a new Nest.js application:

```typescript
import { NestFactory } from '@nestjs/core';
```

Next, we need to import the `ServerlessApplicationModule` from the `@nestjs/serverless` package. This module will be used to bootstrap our Nest.js application:

```typescript
import { ServerlessApplicationModule } from '@nestjs/serverless';
```

Now that we have imported the `NestFactory` and `ServerlessApplicationModule` classes, we can use them to create a new Nest.js application:

```typescript
async function bootstrap() {
  const app = await NestFactory.create(ServerlessApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

In the code above, we are using the `NestFactory` class to create a new Nest.js application. We are passing the `ServerlessApplicationModule` into the `create` method to bootstrap the application.

Finally, we are using the `listen` method to start the application on port 3000.

## Creating a controller

Now that we have our Nest.js application created, let's create a controller. Controllers are responsible for handling incoming HTTP requests and returning responses.

In Nest.js, controllers are created as classes. Let's create a new file called `hello.controller.ts` in the `src/controllers` folder.

In `hello.controller.ts`, we need to import the `Controller` decorator from the `@nestjs/common` package. This decorator is used to mark a class as a controller:

```typescript
import { Controller } from '@nestjs/common';
```

Next, we need to import the `Get` decorator from the `@nestjs/common` package. This decorator is used to mark a controller method as a handler for an HTTP `GET` request:

```typescript
import { Get } from '@nestjs/common';
```

Now that we have imported the `Controller` and `Get` decorators, we can use them to create a controller:

```typescript
@Controller('hello')
export class HelloController {
  @Get()
  hello() {
    return 'Hello, world!';
  }
}
```

In the code above, we have created a controller called `HelloController`. This controller has one method called `hello` which returns the string `Hello, world!`.

We have also used the `Controller` decorator to specify the path for this controller. In this case, we have specified the path as `hello`. This means that the `hello` method will be invoked when a `GET` request is made to the `/hello` path.

## Registering the controller

Now that we have our controller created, we need to register it with our Nest.js application.

We can do this by importing the controller in `main.ts` and passing it into the `NestFactory.create` method:

```typescript
import { HelloController } from './controllers/hello.controller';

async function bootstrap() {
  const app = await NestFactory.create(
    ServerlessApplicationModule,
    {
      controllers: [HelloController],
    },
  );
  await app.listen(3000);
}
bootstrap();
```

In the code above, we have imported the `HelloController` from `hello.controller.ts`. We have then passed it into the `controllers` array in the `NestFactory.create` method.

This will register the `HelloController` with our Nest.js application.

## Deploying the application

Now that we have our Nest.js application created and our controller registered, we are ready to deploy our application.

We'll be deploying our application to AWS Lambda. Lambda is a serverless platform that allows us to run code without provisioning or managing servers.

To deploy our application to Lambda, we'll use the `nest deploy` command. This command will package our application and deploy it to Lambda:

```
nest deploy
```

This command will create a new Lambda function and deploy our Nest.js application to it.

Once the deployment is complete, we can test our application by making a `GET` request to the `/hello` path. We should see the `Hello, world!` string returned.

## Conclusion

In this post, we've learned how to build and deploy serverless applications with Nest.js.

Nest.js is a great choice for building serverless applications. It is lightweight and fast, and it offers a wide range of features, such as support for TypeScript, an easy-to-use dependency injection system, and a powerful module system.

Building a serverless application with Nest.js is quick and easy. In this post, we've walked through the steps of creating a simple serverless Nest.js application and deploying it to AWS Lambda.