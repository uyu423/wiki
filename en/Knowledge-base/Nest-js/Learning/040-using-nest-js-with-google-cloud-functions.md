---
title: 040: Using Nest.js with Google Cloud Functions
description: 
published: true
date: 2023-02-15T12:32:43.533Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:32:36.062Z
---

- [040: Uso de Nest.js con las funciones de Google Cloud***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}
- [040：将 Nest.js 与 Google Cloud Functions 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}
- [040: Google 클라우드 기능과 함께 Nest.js 사용***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}


# Using Nest.js with Google Cloud Functions

Google Cloud Functions is a serverless platform that lets you run your code without having to worry about provisioning or managing servers. You can write code in a variety of languages, including JavaScript, Python, and Go.

Nest.js is a framework for building efficient, scalable Node.js server-side applications. It uses modern JavaScript, is built with TypeScript (which brings static type-checking to JavaScript), and combines elements of both object-oriented and functional programming.

In this post, we'll show you how to use Nest.js with Google Cloud Functions. We'll create a simple function that returns a list of users from a MongoDB database.

## 1. Create a new project

First, we need to create a new project. We'll use the Nest.js CLI to generate a new project.

```
$ nest new project-name
```

## 2. Install dependencies

Next, we need to install the dependencies for our project. We'll need the MongoDB Node.js driver and the Nest.js MongoDB package.

```
$ npm install mongodb @nestjs/mongoose
```

## 3. Create a Nest.js module

Next, we need to create a Nest.js module. This is a standard JavaScript module that will contain our code for interacting with MongoDB.

```javascript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [
    MongooseModule.forFeature([
      { name: 'User', schema: UserSchema }
    ])
  ],
  providers: [UserService],
  exports: [UserService]
})
export class UserModule {}
```

## 4. Create a Nest.js service

Next, we need to create a Nest.js service. This is a standard JavaScript class that will contain our code for interacting with MongoDB.

```javascript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class UserService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<User>
  ) {}

  async findAll(): Promise<User[]> {
    return await this.userModel.find().exec();
  }
}
```

## 5. Create a Google Cloud Function

Next, we need to create a Google Cloud Function. This is a standard JavaScript function that will be triggered when someone makes a request to our API endpoint.

```javascript
import * as functions from 'firebase-functions';
import { NestFactory } from '@nestjs/core';
import { UserModule } from './user.module';

export const userApi = functions.https.onRequest(async (req, res) => {
  const app = await NestFactory.create(UserModule);
  await app.init();
  res.send(await app.get(UserService).findAll());
});
```

## 6. Deploy your function

Finally, we need to deploy our function. We can do this using the Firebase CLI.

```
$ firebase deploy --only functions
```

## 7. Test your API endpoint

You can test your API endpoint by making a GET request to the endpoint URL. You should see a JSON response with a list of users.

```
$ curl https://us-central1-project-name.cloudfunctions.net/userApi
```

## Congratulations!

You've successfully created a Nest.js API endpoint that uses Google Cloud Functions.