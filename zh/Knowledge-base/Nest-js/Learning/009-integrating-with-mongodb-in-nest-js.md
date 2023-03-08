---
title: 009: 在 Nest.js 中与 MongoDB 集成
description: 
published: true
date: 2023-02-14T20:32:21.851Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:32:19.965Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [009: Integrating with MongoDB in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}


# 介绍
在这篇文章中，我们将研究如何将 MongoDB 与 Nest.js 集成。我们将使用 Mongoose 库来帮助我们解决这个问题。 Mongoose 是一种 MongoDB 对象建模工具，旨在在异步环境中工作。

Nest.js 是一个用于构建可扩展的服务器端应用程序的 Node.js 框架。它使用 TypeScript 并受到 Angular 的启发。

# 入门
首先，我们需要安装 Mongoose 库。我们可以使用 npm 来做到这一点：

```
npm install mongoose
```

接下来，我们需要为 Mongoose 连接创建一个文件。我们将这个文件称为```mongoose.ts```：

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

在文件中，我们使用 ```useFactory``` 函数返回解析为我们的 Mongoose 连接的承诺。我们还将全局 ```Promise``` 属性设置为 Mongoose ```Promise``` 属性，以便 Mongoose 使用与 Nest.js 相同的 promise 库。

# 在 Nest.js 中使用 Mongoose
现在我们已经安装了 Mongoose 并设置了连接文件，让我们看看如何将 Mongoose 与 Nest.js 一起使用。

首先，我们需要创建一个 Nest.js 模块。我们将这个模块称为 ```MongooseModule```：

```typescript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [MongooseModule.forRoot('mongodb://localhost/nest')],
})
export class MongooseModule {}
```

在模块中，我们使用```forRoot``` 函数来创建一个MongooseModule 实例。此函数将 MongoDB 连接字符串作为其唯一参数。

接下来，我们需要创建一个 Nest.js 服务。我们将此服务称为 ```MongoService```：

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

在服务中，我们使用“@InjectModel”装饰器将 Mongoose 模型注入到服务中。我们还使用 ```find``` 函数来查询所有用户的数据库。

最后，我们需要创建一个 Nest.js 控制器。我们称这个控制器为```MongoController```：

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

在控制器中，我们使用 ```@Get``` 装饰器来创建响应 GET 请求的路由。我们还使用 MongoService 中的```findAll``` 函数来查询数据库并返回所有用户。

# 结论
在这篇文章中，我们研究了如何将 MongoDB 与 Nest.js 集成。我们已经安装了 Mongoose 库并使用它来创建 Nest.js 模块、服务和控制器。