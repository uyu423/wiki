---
title: 041: Using Nest.js with Firebase Functions
description: 
published: true
date: 2023-02-15T13:33:27.011Z
tags: 
editor: markdown
dateCreated: 2023-02-15T13:33:19.109Z
---

- [041: Uso de Nest.js con funciones de Firebase***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}
- [041：将 Nest.js 与 Firebase 函数结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}
- [041: Firebase 기능과 함께 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}


# Using Nest.js with Firebase Functions

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (which provides typed JavaScript) and combines elements of Object-Oriented Programming, Functional Programming, and Functional Reactive Programming.

Firebase Functions is a serverless platform that lets you run your JavaScript code in the cloud without having to provision or manage any servers. Functions can be triggered by events from Firebase products, such as changes in data in the Firebase Realtime Database, new user signups via Firebase Authentication, or incoming messages via Firebase Cloud Messaging.

In this post, we'll learn how to use Nest.js with Firebase Functions. We'll build a simple Nest.js serverless application that runs on Firebase Functions and responds to HTTP requests.

## Setting up the project

First, let's create a new Nest.js project. We'll use the Nest CLI to generate a new project. Run the following command to generate a new project:

```
$ nest new nest-firebase-functions
```

This will create a new Nest.js project in a folder called ```nest-firebase-functions```.

Next, we need to install the Firebase Functions SDK for Node.js. We can do this by running the following command:

```
$ npm install firebase-functions@latest firebase-admin@latest --save
```

This will install the latest versions of the Firebase Functions SDK and the Firebase Admin SDK.

## Writing the code

Now that we have a Nest.js project and the Firebase SDKs installed, we can write some code.

Open the ```src/main.ts``` file and replace the contents with the following:

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import * as functions from 'firebase-functions';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(() => console.log('Nest.js is listening'));
}

export const api = functions.https.onRequest(bootstrap);
```

Let's take a look at what's going on here.

First, we import the ```NestFactory``` and ```AppModule``` from ```@nestjs/core```.

Next, we import the entire ```firebase-functions``` namespace. This gives us access to the ```functions``` object, which we'll use to configure our HTTP function.

Then, we define an ```async``` function called ```bootstrap```. This function will be called when our HTTP function is invoked. The ```await``` keyword is used to wait for asynchronous operations to complete.

Inside the ```bootstrap``` function, we create a new ```NestFactory``` instance and pass in our ```AppModule```. We then start the Nest.js server by calling the ```listen``` method.

Finally, we export a ```functions.https.onRequest``` function that invokes our ```bootstrap``` function. This will cause our Nest.js application to be invoked when an HTTP request is made to the ```/api``` endpoint.

Now that we have the code, let's take a look at the ```app.module.ts``` file. This is the file that defines our Nest.js module.

Open the ```app.module.ts``` file and replace the contents with the following:

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

This file defines our ```AppModule```, which is the root module of our Nest.js application.

Our module imports the ```Module``` decorator from ```@nestjs/common```. This decorator is used to define a Nest.js module.

Our module also imports the ```AppController``` and ```AppService``` from the ```./app``` folder. We'll take a look at these files in a moment.

The ```@Module``` decorator is used to configure our module. The ```imports``` property is used to import other modules. The ```controllers``` property is used to specify the controllers that are defined in our module. The ```providers``` property is used to specify the providers that are defined in our module.

Now that we've seen the ```app.module.ts``` file, let's take a look at the ```app.controller.ts``` file. This file defines our ```AppController```.

Open the ```app.controller.ts``` file and replace the contents with the following:

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

Our controller imports the ```Controller``` and ```Get``` decorators from ```@nestjs/common```. These decorators are used to define a controller and a controller action respectively.

Our controller also imports the ```AppService``` from the ```./app``` folder. We'll take a look at this file in a moment.

The ```@Controller``` decorator is used to define a controller. The ```@Controller('/')``` syntax specifies the path that our controller actions will be accessible at. In our case, the controller actions will be accessible at the root path (```/```).

The ```@Get()``` decorator is used to define a controller action. The ```@Get('/')``` syntax specifies the path that our controller action will be accessible at. In our case, the controller action will be accessible at the root path (```/```).

The ```getHello``` method is our controller action. This method is invoked when an HTTP GET request is made to the ```/``` endpoint. The ```getHello``` method returns a string, which will be sent back to the client in the HTTP response.

Now that we've seen the ```app.controller.ts``` file, let's take a look at the ```app.service.ts``` file. This file defines our ```AppService```.

Open the ```app.service.ts``` file and replace the contents with the following:

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

Our service imports the ```Injectable``` decorator from ```@nestjs/common```. This decorator is used to define a service.

The ```@Injectable()``` decorator is used to configure our service.

The ```getHello``` method is a simple method that returns a string. This method is invoked by our controller action.

## Deploying the code

Now that we have written our code, we need to deploy it to Firebase.

First, we need to create a Firebase project. We can do this by running the following command:

```
$ firebase init
```

This will create a new Firebase project in the current directory.

Next, we need to deploy our code to Firebase. We can do this by running the following command:

```
$ firebase deploy
```

This will deploy our code to Firebase.

## Testing the code

Now that our code is deployed, let's test it.

We can test our code by making an HTTP request to the ```/api``` endpoint. We can do this using the ```curl``` command. Run the following command to make an HTTP request:

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```

This will make an HTTP request to the ```/api``` endpoint and print the response to the console.

## Conclusion

In this post, we've learned how to use Nest.js with Firebase Functions. We've built a simple Nest.js serverless application that runs on Firebase Functions and responds to HTTP requests.