---
title: 009: Integrating with MongoDB in Nest.js
description: 
published: true
date: 2023-02-14T20:32:27.494Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:32:19.969Z
---

- [009: Integración con MongoDB en Nest.js***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}
- [009: 在 Nest.js 中与 MongoDB 集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}
- [009: Nest.js에서 MongoDB와 통합***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}


# Introduction 
In this post, we'll be looking at how to integrate MongoDB with Nest.js. We'll be using the Mongoose library to help us with this. Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment.

Nest.js is a Node.js framework for building scalable server-side applications. It uses TypeScript and is inspired by Angular.

# Getting Started 
First, we need to install the Mongoose library. We can do this using npm:

```
npm install mongoose
```

Next, we need to create a file for our Mongoose connection. We'll call this file ```mongoose.ts```:

```typescript
import * as mongoose from 'mongoose';

export const databaseProviders = [
  {
    provide: 'DbConnectionToken',
    useFactory: async () => {
      (mongoose as any).Promise = global.Promise;
      return await mongoose.connect('mongodb://localhost/nest');
    },
  },
];
```

In the file, we're using the ```useFactory``` function to return a promise that resolves to our Mongoose connection. We're also setting the global ```Promise``` property to the Mongoose ```Promise``` property so that Mongoose uses the same promise library as Nest.js.

# Using Mongoose with Nest.js 
Now that we have Mongoose installed and our connection file set up, let's look at how to use Mongoose with Nest.js.

First, we need to create a Nest.js module. We'll call this module ```MongooseModule```:

```typescript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [MongooseModule.forRoot('mongodb://localhost/nest')],
})
export class MongooseModule {}
```

In the module, we're using the ```forRoot``` function to create a MongooseModule instance. This function takes a MongoDB connection string as its only parameter.

Next, we need to create a Nest.js service. We'll call this service ```MongoService```:

```typescript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class MongoService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<any>,
  ) {}

  async findAll(): Promise<any[]> {
    return await this.userModel.find().exec();
  }
}
```

In the service, we're using the ```@InjectModel``` decorator to inject a Mongoose model into the service. We're also using the ```find``` function to query the database for all users.

Finally, we need to create a Nest.js controller. We'll call this controller ```MongoController```:

```typescript
import { Controller, Get } from '@nestjs/common';
import { MongoService } from './mongo.service';

@Controller('mongo')
export class MongoController {
  constructor(private readonly mongoService: MongoService) {}

  @Get()
  async findAll() {
    return await this.mongoService.findAll();
  }
}
```

In the controller, we're using the ```@Get``` decorator to create a route that responds to GET requests. We're also using the ```findAll``` function from our MongoService to query the database and return all users.

# Conclusion 
In this post, we've looked at how to integrate MongoDB with Nest.js. We've installed the Mongoose library and used it to create a Nest.js module, service, and controller.