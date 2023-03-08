---
title: 055: Implementing real-time updates with Nest.js and PWA
description: 
published: true
date: 2023-02-10T06:18:31.950Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:18:25.426Z
---

- [055: Implementación de actualizaciones en tiempo real con Nest.js y PWA***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}
- [055：使用 Nest.js 和 PWA 实现实时更新***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}
- [055: Nest.js 및 PWA로 실시간 업데이트 구현***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}


# Implementing real-time updates with Nest.js and PWA

In this post, we'll be looking at how to implement real-time updates in a Nest.js application with a Progressive Web App (PWA).

We'll start by setting up a simple Nest.js server and then connecting it to a PWA. Then, we'll add some code to implement the real-time updates.

## Setting up the Nest.js server

First, let's create a new Nest.js project. We can use the Nest CLI to do this:

```
nest new realtime-nest-pwa
```

Now that we have a project, we need to install some dependencies. We'll need the following:

- @nestjs/platform-express
- @nestjs/typeorm
- typeorm
- pg

We can install these dependencies with the following command:

```
npm install --save @nestjs/platform-express @nestjs/typeorm typeorm pg
```

Next, we need to create a few files:

- `.env`
- `ormconfig.json`
- `nest-cli.json`

In the `.env` file, we'll need to add the following:

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa
```

This will tell Nest.js how to connect to our database.

In the `ormconfig.json` file, we'll need to add the following:

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "postgres",
  "database": "realtime_nest_pwa",
  "entities": ["src/**/**.entity{.ts,.js}"],
  "migrations": ["src/migrations/**/*{.ts,.js}"],
  "cli": {
    "migrationsDir": "src/migrations"
  }
}
```

This will tell TypeORM how to connect to our database.

Finally, in the `nest-cli.json` file, we'll need to add the following:

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

This will tell the Nest CLI how to generate code for our project.

## Connecting the Nest.js server to a PWA

Now that we have a Nest.js project set up, we need to connect it to a PWA. We can do this with the `create-react-app` CLI.

First, we need to install the `create-react-app` CLI:

```
npm install -g create-react-app
```

Next, we need to create a new React project:

```
create-react-app realtime-nest-pwa
```

Now that we have a React project, we need to install some dependencies. We'll need the following:

- react
- react-dom
- react-router-dom
- @types/react
- @types/react-dom
- @types/react-router-dom

We can install these dependencies with the following command:

```
npm install --save react react-dom react-router-dom @types/react @types/react-dom @types/react-router-dom
```

## Implementing the real-time updates

Now that we have a Nest.js server and a React client set up, we can start implementing the real-time updates.

We'll start by creating a new file in our Nest.js project: `src/websockets.ts`. This file will contain the code for our WebSocket server.

In the `websockets.ts` file, we'll need to add the following:

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

This code will set up a WebSocket server on port 8080. Once a connection is made, the server will log any messages it receives and send a message back to the client.

Next, we need to update our `.env` file:

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa

WS_PORT=8080
```

We've added a new `WS_PORT` variable to specify the port for our WebSocket server.

Now, we need to update our `main.ts` file:

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

We've imported `cookieParser`, `session`, `connect-redis`, and `redis`. We've also added some code to set up `cookieParser` and `session`. This code will allow us to store information in cookies and sessions.

Next, we need to update our `app.module.ts` file:

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

We've imported `ConfigModule` and `join`. We've also added some code to set up `ConfigModule`. This code will allow us to access environment variables from our `.env` file.

Now, we need to update our `app.controller.ts` file:

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

We've imported `UserService`. We've also added a constructor and a `getHello` method. This code will allow us to access the `UserService` from our controller.

Finally, we need to update our `app.service.ts` file:

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

We've imported `User` and `Repository`. We've also added a constructor and a `getHello` method. This code will allow us to access the `User` repository from our service.

## Conclusion

In this post, we've looked at how to implement real-time updates in a Nest.js application with a Progressive Web App (PWA).

We've started by setting up a simple Nest.js server and then connecting it to a PWA. Then, we've added some code to implement the real-time updates.