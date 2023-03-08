---
title: 015: manejo de errores en Nest.js
description: 
published: true
date: 2023-02-11T01:17:27.225Z
tags: 
editor: markdown
dateCreated: 2023-02-11T01:17:25.634Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [015: Error handling in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}


# Manejo de errores en Nest.js

El desarrollo de aplicaciones web puede ser complicado, especialmente cuando se trata de la gestión de errores. Hay muchas formas de manejar los errores en Nest.js, y en esta publicación exploraremos algunos de los métodos más comunes.

## Trata de atraparlo

El método try/catch es la forma más básica de manejar errores en Nest.js. Para usar este método, simplemente envuelva su código en un bloque de prueba y luego agregue un bloque de captura para manejar cualquier error que pueda ocurrir.

Aquí hay un ejemplo simple:

```javascript
try {
  // do something that might throw an error
} catch (err) {
  // handle the error
}
```

Si ocurre un error, será capturado por el bloque catch y podrá ser tratado en consecuencia.

## Manejo de errores asincrónicos

Si usa código asíncrono (es decir, código que usa Promises o async/await), aún puede usar el método try/catch. Sin embargo, debe tener en cuenta el hecho de que los errores generados en el código asíncrono son capturados por el siguiente tic del bucle de eventos.

Esto significa que si tiene un bloque try/catch que rodea el código asíncrono, el bloque catch no se ejecutará hasta el próximo tic del bucle de eventos. Esto puede ser confuso, así que echemos un vistazo a un ejemplo:

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}
```

En el ejemplo anterior, el error no se detectará hasta que hayan pasado 1000 ms. Esto se debe a que la función setTimeout es asíncrona y el error solo aparece en el siguiente tic del bucle de eventos.

Para evitar esto, puedes usar el método Promise.catch:

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}

Promise.catch((err) => {
  // this catch block will be executed immediately
});
```

## Error al manejar el middleware

Si desea centralizar su manejo de errores, puede usar el middleware Nest.js. El middleware es una función que se ejecuta antes de que una solicitud llegue al código de su controlador. Esto lo convierte en el lugar perfecto para poner su lógica de manejo de errores.

Para crear una función de middleware, debe usar el decorador @UseMiddleware:

```javascript
import { UseMiddleware, Middleware } from '@nestjs/common';

@Middleware()
export class ErrorHandlerMiddleware implements NestMiddleware {
  // your middleware logic goes here
}
```

Luego, para usar el middleware, debe registrarlo en su módulo Nest.js:

```javascript
@Module({
  imports: [],
  controllers: [],
  providers: [],
  middleware: [ErrorHandlerMiddleware],
})
export class AppModule {}
```

Ahora, cualquier error que ocurra en su aplicación será manejado por la función de middleware.

## Conclusión

Como puede ver, hay muchas formas de manejar los errores en Nest.js. El método que elija dependerá de sus necesidades específicas. Sin embargo, todos los métodos descritos en esta publicación deberían brindarle un buen punto de partida para tratar los errores en sus aplicaciones Nest.js.