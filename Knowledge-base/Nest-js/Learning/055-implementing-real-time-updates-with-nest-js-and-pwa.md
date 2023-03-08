---
title: 055: Nest.js 및 PWA로 실시간 업데이트 구현
description: 
published: true
date: 2023-02-10T06:18:27.194Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:18:25.421Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [055: Implementing real-time updates with Nest.js and PWA***English** document is available*](/en/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}


# Nest.js 및 PWA로 실시간 업데이트 구현

이 게시물에서는 PWA(Progressive Web App)를 사용하여 Nest.js 애플리케이션에서 실시간 업데이트를 구현하는 방법을 살펴보겠습니다.

간단한 Nest.js 서버를 설정한 다음 PWA에 연결하는 것으로 시작하겠습니다. 그런 다음 실시간 업데이트를 구현하는 코드를 추가합니다.

## Nest.js 서버 설정

먼저 새로운 Nest.js 프로젝트를 생성해 보겠습니다. 이를 위해 Nest CLI를 사용할 수 있습니다.

```
nest new realtime-nest-pwa
```

이제 프로젝트가 있으므로 몇 가지 종속 항목을 설치해야 합니다. 다음이 필요합니다.

- @nestjs/platform-express
- @nestjs/typeorm
- 활자체
-pg

다음 명령을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install --save @nestjs/platform-express @nestjs/typeorm typeorm pg
```

다음으로 몇 가지 파일을 만들어야 합니다.

- `.env`
- `ormconfig.json`
- `nest-cli.json`

`.env` 파일에서 다음을 추가해야 합니다.

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa
```

이는 Nest.js가 데이터베이스에 연결하는 방법을 알려줍니다.

`ormconfig.json` 파일에서 다음을 추가해야 합니다.

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

이것은 TypeORM에게 데이터베이스에 연결하는 방법을 알려줍니다.

마지막으로 `nest-cli.json` 파일에 다음을 추가해야 합니다.

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

이것은 Nest CLI에 프로젝트에 대한 코드를 생성하는 방법을 알려줍니다.

## Nest.js 서버를 PWA에 연결

이제 Nest.js 프로젝트가 설정되었으므로 PWA에 연결해야 합니다. 우리는 `create-react-app` CLI로 이것을 할 수 있습니다.

먼저 `create-react-app` CLI를 설치해야 합니다.

```
npm install -g create-react-app
```

다음으로 새로운 React 프로젝트를 만들어야 합니다.

```
create-react-app realtime-nest-pwa
```

이제 React 프로젝트가 있으므로 몇 가지 종속성을 설치해야 합니다. 다음이 필요합니다.

- 반응
-반응 돔
- 반응 라우터 돔
- @유형/반응
- @types/react-dom
- @types/react-router-dom

다음 명령을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install --save react react-dom react-router-dom @types/react @types/react-dom @types/react-router-dom
```

## 실시간 업데이트 구현

이제 Nest.js 서버와 React 클라이언트가 설정되었으므로 실시간 업데이트 구현을 시작할 수 있습니다.

Nest.js 프로젝트에서 `src/websockets.ts`라는 새 파일을 생성하는 것으로 시작하겠습니다. 이 파일에는 WebSocket 서버용 코드가 포함됩니다.

`websockets.ts` 파일에서 다음을 추가해야 합니다.

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

이 코드는 포트 8080에서 WebSocket 서버를 설정합니다. 일단 연결되면 서버는 수신한 모든 메시지를 기록하고 메시지를 다시 클라이언트로 보냅니다.

다음으로 `.env` 파일을 업데이트해야 합니다.

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa

WS_PORT=8080
```

WebSocket 서버의 포트를 지정하기 위해 새로운 `WS_PORT` 변수를 추가했습니다.

이제 `main.ts` 파일을 업데이트해야 합니다.

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

`cookieParser`, `session`, `connect-redis` 및 `redis`를 가져왔습니다. 또한 `cookieParser` 및 `session`을 설정하는 코드를 추가했습니다. 이 코드를 사용하면 쿠키와 세션에 정보를 저장할 수 있습니다.

다음으로 `app.module.ts` 파일을 업데이트해야 합니다.

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

`ConfigModule`과 `join`을 가져왔습니다. 또한 `ConfigModule`을 설정하는 코드를 추가했습니다. 이 코드를 사용하면 `.env` 파일에서 환경 변수에 액세스할 수 있습니다.

이제 `app.controller.ts` 파일을 업데이트해야 합니다.

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

`UserService`를 가져왔습니다. 생성자와 `getHello` 메서드도 추가했습니다. 이 코드를 사용하면 컨트롤러에서 `UserService`에 액세스할 수 있습니다.

마지막으로 `app.service.ts` 파일을 업데이트해야 합니다.

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

`User` 및 `Repository`를 가져왔습니다. 생성자와 `getHello` 메서드도 추가했습니다. 이 코드를 사용하면 서비스에서 `User` 리포지토리에 액세스할 수 있습니다.

## 결론

이 게시물에서는 PWA(Progressive Web App)를 사용하여 Nest.js 애플리케이션에서 실시간 업데이트를 구현하는 방법을 살펴보았습니다.

간단한 Nest.js 서버를 설정한 다음 PWA에 연결하는 것으로 시작했습니다. 그런 다음 실시간 업데이트를 구현하는 코드를 추가했습니다.