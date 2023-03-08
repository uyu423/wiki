---
title: 014: Uso de middleware en Nest.js
description: 
published: true
date: 2023-02-15T00:32:32.946Z
tags: 
editor: markdown
dateCreated: 2023-02-15T00:32:25.393Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [014: Using middlewares in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/014-using-middlewares-in-nest-js)
{.links-list}


# Uso de middleware en Nest.js

Nest.js es un marco web para Node.js que lo ayuda a crear aplicaciones escalables del lado del servidor. En esta publicación, veremos cómo usar middlewares en Nest.js.

Los middlewares son funciones que Nest.js invoca cuando se recibe una solicitud entrante. Se pueden utilizar para realizar tareas como el registro, la validación y la autenticación.

Nest.js viene con una fábrica de middleware integrada que facilita la creación de sus propios middlewares. Para crear un middleware, debe crear una clase que implemente la interfaz `NestMiddleware`. Esta interfaz define un método `use()` que toma los objetos `req` y `res` como parámetros.

Aquí hay un ejemplo simple de un middleware que registra la solicitud entrante:

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    console.log(`Incoming request at ${req.url}`);
    next();
  }
}
```

Para usar este middleware, debe registrarlo con Nest.js. Esto se puede hacer en el archivo `app.module.ts`:

```typescript
import { Module } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';

@Module({
  providers: [LoggerMiddleware],
})
export class AppModule {}
```

Una vez que se registra el middleware, Nest.js lo invocará cada vez que se reciba una solicitud entrante.

Los middlewares también se pueden utilizar para realizar tareas como la validación y la autenticación. Por ejemplo, puede crear un middleware que verifique si la solicitud entrante está autenticada:

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';

@Injectable()
export class AuthMiddleware implements NestMiddleware {
  use(req: any, res: any, next: () => void) {
    if (!req.isAuthenticated()) {
      res.status(401).send('You are not authenticated');
    } else {
      next();
    }
  }
}
```

Este middleware verificará si la solicitud entrante está autenticada. Si no es así, devolverá un código de estado `401 No autorizado`. De lo contrario, invocará el siguiente middleware de la cadena.

Los middlewares se pueden encadenar para crear una cadena de operaciones que se ejecuta para cada solicitud entrante. Por ejemplo, puede crear una cadena que registre la solicitud, valide la solicitud y luego autentique la solicitud:

```typescript
import { Injectable, NestMiddleware } from '@nestjs/common';
import { LoggerMiddleware } from './logger.middleware';
import { AuthMiddleware } from './auth.middleware';

@Module({
  providers: [
    LoggerMiddleware,
    AuthMiddleware,
  ],
})
export class AppModule {}
```

En este ejemplo, `LoggerMiddleware` se invocará primero, seguido de `AuthMiddleware`.

Los middlewares se pueden utilizar para realizar una amplia variedad de tareas. Son una herramienta poderosa que se puede utilizar para ampliar la funcionalidad de Nest.js.