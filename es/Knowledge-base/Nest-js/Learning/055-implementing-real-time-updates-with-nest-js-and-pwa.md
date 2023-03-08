---
title: 055: Implementación de actualizaciones en tiempo real con Nest.js y PWA
description: 
published: true
date: 2023-02-10T06:18:27.209Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:18:25.424Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [055: Implementing real-time updates with Nest.js and PWA***English** document is available*](/en/Knowledge-base/Nest-js/Learning/055-implementing-real-time-updates-with-nest-js-and-pwa)
{.links-list}


# Implementando actualizaciones en tiempo real con Nest.js y PWA

En esta publicación, veremos cómo implementar actualizaciones en tiempo real en una aplicación Nest.js con una aplicación web progresiva (PWA).

Comenzaremos configurando un servidor Nest.js simple y luego conectándolo a una PWA. Luego, agregaremos código para implementar las actualizaciones en tiempo real.

## Configuración del servidor Nest.js

Primero, creemos un nuevo proyecto Nest.js. Podemos usar la CLI de Nest para hacer esto:

```
nest new realtime-nest-pwa
```

Ahora que tenemos un proyecto, necesitamos instalar algunas dependencias. Necesitaremos lo siguiente:

- @nestjs/plataforma-express
- @nestjs/typeorm
- tipo
- pág.

Podemos instalar estas dependencias con el siguiente comando:

```
npm install --save @nestjs/platform-express @nestjs/typeorm typeorm pg
```

A continuación, necesitamos crear algunos archivos:

- `.env`
- `ormconfig.json`
- `nest-cli.json`

En el archivo `.env`, necesitaremos agregar lo siguiente:

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa
```

Esto le dirá a Nest.js cómo conectarse a nuestra base de datos.

En el archivo `ormconfig.json`, necesitaremos agregar lo siguiente:

```json
{
  "type": "postgres",
  "host": "localhost",
  "port": 5432,
  "username": "postgres",
  "password": "postgres",
  "database": "realtime_nest_pwa",
  "entities": ["src/**/**.entity{.links-list}"],
  "migrations": ["src/migrations/**/*{.links-list}"],
  "cli": {
    "migrationsDir": "src/migrations"
  }
}
```

Esto le dirá a TypeORM cómo conectarse a nuestra base de datos.

Finalmente, en el archivo `nest-cli.json`, necesitaremos agregar lo siguiente:

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

Esto le dirá a Nest CLI cómo generar código para nuestro proyecto.

## Conexión del servidor Nest.js a una PWA

Ahora que tenemos un proyecto Nest.js configurado, necesitamos conectarlo a una PWA. Podemos hacer esto con la CLI `create-react-app`.

Primero, necesitamos instalar la CLI `create-react-app`:

```
npm install -g create-react-app
```

A continuación, necesitamos crear un nuevo proyecto React:

```
create-react-app realtime-nest-pwa
```

Ahora que tenemos un proyecto React, necesitamos instalar algunas dependencias. Necesitaremos lo siguiente:

- reaccionar
- reaccionar-dom
- reaccionar-enrutador-dom
- @tipos/reaccionar
- @tipos/reaccionar-dom
- @tipos/react-router-dom

Podemos instalar estas dependencias con el siguiente comando:

```
npm install --save react react-dom react-router-dom @types/react @types/react-dom @types/react-router-dom
```

## Implementando las actualizaciones en tiempo real

Ahora que tenemos un servidor Nest.js y un cliente React configurados, podemos comenzar a implementar las actualizaciones en tiempo real.

Comenzaremos creando un nuevo archivo en nuestro proyecto Nest.js: `src/websockets.ts`. Este archivo contendrá el código para nuestro servidor WebSocket.

En el archivo `websockets.ts`, necesitaremos agregar lo siguiente:

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

Este código configurará un servidor WebSocket en el puerto 8080. Una vez que se establezca una conexión, el servidor registrará cualquier mensaje que reciba y enviará un mensaje al cliente.

A continuación, necesitamos actualizar nuestro archivo `.env`:

```
DB_TYPE=postgres
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=postgres
DB_NAME=realtime_nest_pwa

WS_PORT=8080
```

Agregamos una nueva variable `WS_PORT` para especificar el puerto de nuestro servidor WebSocket.

Ahora, necesitamos actualizar nuestro archivo `main.ts`:

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

Hemos importado `cookieParser`, `session`, `connect-redis` y `redis`. También hemos agregado código para configurar `cookieParser` y `session`. Este código nos permitirá almacenar información en cookies y sesiones.

A continuación, debemos actualizar nuestro archivo `app.module.ts`:

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

Hemos importado `ConfigModule` y `join`. También hemos agregado algo de código para configurar `ConfigModule`. Este código nos permitirá acceder a las variables de entorno desde nuestro archivo `.env`.

Ahora, necesitamos actualizar nuestro archivo `app.controller.ts`:

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

Hemos importado `UserService`. También hemos agregado un constructor y un método `getHello`. Este código nos permitirá acceder al `UserService` desde nuestro controlador.

Finalmente, necesitamos actualizar nuestro archivo `app.service.ts`:

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

Hemos importado `Usuario` y `Repositorio`. También hemos agregado un constructor y un método `getHello`. Este código nos permitirá acceder al repositorio `Usuario` desde nuestro servicio.

## Conclusión

En esta publicación, analizamos cómo implementar actualizaciones en tiempo real en una aplicación Nest.js con una aplicación web progresiva (PWA).

Comenzamos configurando un servidor Nest.js simple y luego conectándolo a una PWA. Luego, agregamos código para implementar las actualizaciones en tiempo real.