---
title: 042: Implementing real-time notifications with Nest.js and Firebase
description: 
published: true
date: 2023-02-12T03:17:59.025Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:17:52.264Z
---

- [042: Implementación de notificaciones en tiempo real con Nest.js y Firebase***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}
- [042：使用 Nest.js 和 Firebase 实现实时通知***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}
- [042: Nest.js 및 Firebase로 실시간 알림 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}


# Implementing real-time notifications with Nest.js and Firebase

In this post, we'll be looking at how to set up real-time notifications in a Nest.js application using the Firebase Cloud Messaging (FCM) service.

Nest.js is a Node.js framework for building scalable server-side applications. It uses modern JavaScript, is built with TypeScript (that compiles to JavaScript) and combines elements of Object-Oriented Programming, Functional Programming, and Reactive Programming.

Firebase is a mobile and web application development platform developed by Google. It provides a number of services, one of which is FCM. FCM is a cross-platform messaging solution that lets you reliably deliver messages at no cost.

## Setting up a Nest.js project

We'll start by setting up a new Nest.js project. We'll be using the Nest CLI for this. If you don't have it installed, you can do so by running the following command:

```
$ npm install -g @nestjs/cli
```

Once the Nest CLI is installed, we can create a new project by running the following command:

```
$ nest new project-name
```

This will create a new directory with the project files.

## Installing the dependencies

We need to install the following dependencies for our project:

- @nestjs/common
- @nestjs/platform-express
- firebase-admin

We can install these dependencies by running the following command:

```
$ npm install --save @nestjs/common @nestjs/platform-express firebase-admin
```

## Configuring Firebase

We need to create a new Firebase project in order to use FCM. We can do this by going to the [Firebase console](https://console.firebase.google.com/) and clicking on the "Create a Project" button.

Give your project a name and click on the "Create Project" button.

Once the project is created, click on the "Add Firebase to your web app" button.

This will open a popup with your Firebase configuration. We need to copy the config object and add it to the `environment.ts` file in our project. The file should look like this:

```javascript
export const environment = {
  production: false,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

We also need to add the following line to the `environment.prod.ts` file:

```javascript
export const environment = {
  production: true,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

## Creating the FCM service

We need to create a new service that will handle sending FCM messages. We can do this by running the following command:

```
$ nest generate service fcm
```

This will create a new service file in the `src/fcm` directory. We need to import the `firebase-admin` module and the `environment` file. We also need to create a new instance of the `admin.messaging.Messaging` class. The service should look like this:

```javascript
import { Injectable } from '@nestjs/common';
import * as admin from 'firebase-admin';
import { environment } from '../../environments/environment';

@Injectable()
export class FcmService {
  private readonly messaging = admin.messaging();

  constructor() {
    admin.initializeApp({
      credential: admin.credential.applicationDefault(),
      databaseURL: environment.firebase.databaseURL,
      projectId: environment.firebase.projectId
    });
  }

  // ...
}
```

## Sending FCM messages

We need to add a new method to the `FcmService` that will send FCM messages. The method should take a `to` parameter that specifies the recipient of the message and a `data` parameter that contains the data to be sent.

The method should return a `Promise` that resolves when the message has been sent.

```javascript
  async send(to: string, data: any): Promise<void> {
    const message = {
      to,
      data
    };

    await this.messaging.send(message);
  }
```

## Creating the controller

We need to create a new controller that will call the `send` method of the `FcmService`. We can do this by running the following command:

```
$ nest generate controller fcm
```

This will create a new controller file in the `src/fcm` directory. We need to import the `FcmService` and `@nestjs/common` modules. We also need to inject the `FcmService` into the controller. The controller should look like this:

```javascript
import { Controller, Post, Body } from '@nestjs/common';
import { FcmService } from './fcm.service';

@Controller('fcm')
export class FcmController {
  constructor(private readonly fcmService: FcmService) {}

  @Post()
  async send(@Body('to') to: string, @Body('data') data: any): Promise<void> {
    await this.fcmService.send(to, data);
  }
}
```

## Testing the controller

We can test the controller by sending a POST request to the `/fcm` endpoint with a `to` and `data` parameter. We can do this using the [Postman](https://www.getpostman.com/) tool.

We should see a success message in the Postman console if the message was sent successfully.

## Conclusion

In this post, we've seen how to set up real-time notifications in a Nest.js application using the Firebase Cloud Messaging (FCM) service.