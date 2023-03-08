---
title: 005: Enrutamiento y controladores en Nest.js
description: 
published: true
date: 2023-02-14T16:32:32.708Z
tags: 
editor: markdown
dateCreated: 2023-02-14T16:32:24.574Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [005: Routing and controllers in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/005-routing-and-controllers-in-nest-js)
{.links-list}


# Introducción

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor. Se basa en Express.js y utiliza TypeScript, que es un superconjunto de JavaScript que agrega escritura estática al lenguaje.

Nest.js es un marco relativamente nuevo y, como tal, no tiene tanta documentación ni soporte comunitario como Express.js. Sin embargo, está creciendo en popularidad y es utilizado por empresas como Microsoft, Google y Amazon.

En esta publicación, veremos cómo configurar el enrutamiento y los controladores en Nest.js. También veremos algunos de los beneficios de usar Nest.js sobre Express.js.

# Configuración de enrutamiento y controladores en Nest.js

Lo primero que debemos hacer es instalar el marco Nest.js. Podemos hacer esto usando el administrador de paquetes de Node.js, npm.

```
npm install --save @nestjs/common
```

Una vez que se instala Nest.js, podemos crear un nuevo archivo en nuestro proyecto llamado `app.controller.ts`. Este archivo contendrá nuestra lógica de controlador.

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/')
export class AppController {
  @Get()
  root() {
    return 'Hello, world!';
  }
}
```

En el código anterior, hemos importado los decoradores `Controller` y `Get` de `@nestjs/common`. Luego hemos usado el decorador `@Controller` para crear un nuevo controlador en la ruta `/`.

Finalmente, hemos creado un nuevo método `root` y lo hemos decorado con el decorador `@Get`. Se llamará a este método cuando se realice una solicitud GET a la ruta `/`.

Ahora podemos crear un nuevo archivo llamado `main.ts`. Este archivo se usará para iniciar nuestra aplicación Nest.js.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

En el código anterior, hemos importado `NestFactory` y `AppModule` desde `@nestjs/core`. Luego usamos `NestFactory` para crear una nueva aplicación Nest.js y pasamos nuestro `AppModule`.

Finalmente, hemos llamado al método `listen` para iniciar la aplicación en el puerto 3000.

Si ahora ejecutamos la aplicación usando `node main.ts`, deberíamos ver el siguiente resultado:

```
$ node main.ts
[Nest] 7100   - 2020-03-22 10:54:54   [NestFactory] Starting Nest application...
[Nest] 7100   - 2020-03-22 10:54:54   [InstanceLoader] AppModule dependencies initialized +0ms
[Nest] 7100   - 2020-03-22 10:54:54   [RouterExplorer] Mapped {,GET} route +2ms
[Nest] 7100   - 2020-03-22 10:54:54   [NestApplication] Nest application successfully started +2ms
```

Si ahora abrimos nuestro navegador y navegamos a `http://localhost:3000/`, deberíamos ver el siguiente resultado:

```
Hello, world!
```

# Conclusión

En esta publicación, hemos visto cómo configurar el enrutamiento y los controladores en Nest.js. También analizamos algunos de los beneficios de usar Nest.js sobre Express.js.

Si está buscando un marco Node.js que utilice TypeScript, definitivamente vale la pena considerar Nest.js.