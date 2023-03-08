---
title: 055：使用 Nest.js 和 PWA 实现实时更新
description: 
published: true
date: 2023-02-10T06:18:27.163Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:18:25.424Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [055: Implementing real-time updates with Nest.js and PWA***English** document is available*](/en/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}


# 使用 Nest.js 和 PWA 实现实时更新

在这篇文章中，我们将研究如何使用渐进式 Web 应用程序 (PWA) 在 Nest.js 应用程序中实现实时更新。

我们将从设置一个简单的 Nest.js 服务器开始，然后将其连接到 PWA。然后，我们将添加一些代码来实现实时更新。

## 设置 Nest.js 服务器

首先，让我们创建一个新的 Nest.js 项目。我们可以使用 Nest CLI 来执行此操作：

```
nest new realtime-nest-pwa
```

现在我们有了一个项目，我们需要安装一些依赖项。我们需要以下内容：

- @nestjs/平台快递
- @nestjs/typeorm
- 类型规则
- PG

我们可以使用以下命令安装这些依赖项：

```
npm install --save @nestjs/platform-express @nestjs/typeorm typeorm pg
```

接下来，我们需要创建几个文件：

-`.env`
-`ormconfig.json`
-`nest-cli.json`

在 .env 文件中，我们需要添加以下内容：

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa
```

这将告诉 Nest.js 如何连接到我们的数据库。

在 ormconfig.json 文件中，我们需要添加以下内容：

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "postgres",
  "database": "realtime_nest_pwa",
  "entities": ["src/**/**.entity{.links-list}"],
  "migrations": ["src/migrations/**/*{.ts,.js}"],
  "cli": {
    "migrationsDir": "src/migrations"
  }
}
```

这将告诉 TypeORM 如何连接到我们的数据库。

最后，在 nest-cli.json 文件中，我们需要添加以下内容：

```json
{
  "collection": "@nestjs/schematics",
  "sourceRoot": "src",
  "compilerOptions": {
    "emitDecoratorMetadata": true,
    "experimentalDecorators": true,
    "target": "es2015",
    "module": "commonjs"
  }
}
```

这将告诉 Nest CLI 如何为我们的项目生成代码。

## 将 Nest.js 服务器连接到 PWA

现在我们已经设置了一个 Nest.js 项目，我们需要将它连接到一个 PWA。我们可以使用 `create-react-app` CLI 来做到这一点。

首先，我们需要安装 `create-react-app` CLI：

```
npm install -g create-react-app
```

接下来，我们需要创建一个新的 React 项目：

```
create-react-app realtime-nest-pwa
```

现在我们有了一个 React 项目，我们需要安装一些依赖项。我们需要以下内容：

- 反应
- 反应域
- 反应路由器域
- @类型/反应
- @类型/反应-dom
- @types/react-router-dom

我们可以使用以下命令安装这些依赖项：

```
npm install --save react react-dom react-router-dom @types/react @types/react-dom @types/react-router-dom
```

## 实现实时更新

现在我们已经设置了 Nest.js 服务器和 React 客户端，我们可以开始实施实时更新了。

我们将从在我们的 Nest.js 项目中创建一个新文件开始：`src/websockets.ts`。该文件将包含我们的 WebSocket 服务器的代码。

在 websockets.ts 文件中，我们需要添加以下内容：

```typescript
import * as WebSocket from 'ws';

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws: WebSocket) => {
  ws.on('message', (message: string) => {
    console.log(`Received message => ${message}`);
  });

  ws.send('Hello!');
});
```

此代码将在端口 8080 上设置一个 WebSocket 服务器。建立连接后，服务器将记录它收到的所有消息并将消息发送回客户端。

接下来，我们需要更新我们的 .env 文件：

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa

WS_PORT=8080
```

我们添加了一个新的 `WS_PORT` 变量来指定 WebSocket 服务器的端口。

现在，我们需要更新我们的 main.ts 文件：

```typescript
import { NestFactory } from '@nestjs/core';
import { ApplicationModule } from './app.module';
import { NestExpressApplication } from '@nestjs/platform-express';
import { join } from 'path';
import * as cookieParser from 'cookie-parser';
import * as session from 'express-session';
import * as connectRedis from 'connect-redis';
import * as redis from 'redis';

async function bootstrap() {
  const app = await NestFactory.create<NestExpressApplication>(
    ApplicationModule,
  );

  const RedisStore = connectRedis(session);
  const redisClient = redis.createClient();

  app.use(
    cookieParser(),
    session({
      store: new RedisStore({
        client: redisClient,
      }),
      secret: 'secret',
      resave: false,
      saveUninitialized: false,
      cookie: {
        secure: false,
      },
    }),
  );

  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');

  await app.listen(process.env.PORT || 3000);
}
bootstrap();
```

我们导入了 `cookieParser`、`session`、`connect-redis` 和 `redis`。我们还添加了一些代码来设置 `cookieParser` 和 `session`。此代码将允许我们将信息存储在 cookie 和会话中。

接下来，我们需要更新我们的 `app.module.ts` 文件：

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { UserModule } from './user/user.module';
import { join } from 'path';
import { ConfigModule } from '@nestjs/config';

@Module({
  imports: [
    TypeOrmModule.forRoot(),
    ConfigModule.forRoot({
      isGlobal: true,
      envFilePath: join(__dirname, '..', '.env'),
    }),
    UserModule,
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

我们导入了 `ConfigModule` 和 `join`。我们还添加了一些代码来设置“ConfigModule”。此代码将允许我们从 .env 文件访问环境变量。

现在，我们需要更新我们的 app.controller.ts 文件：

```typescript
import { Controller, Get } from '@nestjs/common';
import { UserService } from './user/user.service';

@Controller()
export class AppController {
  constructor(private userService: UserService) {}

  @Get()
  getHello(): string {
    return this.userService.getHello();
  }
}
```

我们已经导入了 `UserService`。我们还添加了一个构造函数和一个 getHello 方法。这段代码将允许我们从我们的控制器访问 `UserService`。

最后，我们需要更新我们的 app.service.ts 文件：

```typescript
import { Injectable } from '@nestjs/common';
import { User } from './user/user.entity';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';

@Injectable()
export class AppService {
  constructor(
    @InjectRepository(User)
    private userRepository: Repository<User>,
  ) {}

  getHello(): string {
    return 'Hello World!';
  }
}
```

我们导入了 `User` 和 `Repository`。我们还添加了一个构造函数和一个 getHello 方法。此代码将允许我们从我们的服务访问 `User` 存储库。

## 结论

在这篇文章中，我们研究了如何使用渐进式 Web 应用程序 (PWA) 在 Nest.js 应用程序中实现实时更新。

我们首先设置一个简单的 Nest.js 服务器，然后将其连接到 PWA。然后，我们添加了一些代码来实现实时更新。