---
title: 050: funciones y técnicas avanzadas de Nest.js
description: 
published: true
date: 2023-02-15T18:33:02.615Z
tags: 
editor: markdown
dateCreated: 2023-02-15T18:33:00.851Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [050: Advanced Nest.js features and techniques***English** document is available*](/en/Knowledge-base/Nest-js/Learning/050-advanced-nest-js-features-and-techniques)
{.links-list}


050: funciones y técnicas avanzadas de Nest.js

Nest.js es un poderoso marco web para Node.js. Se basa en Express.js y utiliza TypeScript, lo que facilita el desarrollo y la implementación de aplicaciones de nivel empresarial.

En esta publicación, veremos algunas de las funciones y técnicas avanzadas que ofrece Nest.js.

Cubriremos los siguientes temas:

- Enrutamiento
- Autenticacion y autorizacion
- Acceso a la base de datos
- Pruebas

## Enrutamiento

En Nest.js, las rutas se definen mediante el decorador @Controller(). Por ejemplo:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Como puede ver, el decorador @Controller() define la ruta base para todas las rutas definidas dentro del controlador. Los decoradores @Get(), @Post(), @Put() y @Delete() se utilizan para definir los métodos HTTP para cada ruta.

## Autenticacion y autorizacion

Nest.js proporciona soporte listo para usar para autenticación y autorización.

Para autenticar a un usuario, Nest.js proporciona el decorador @Authenticate(). Este decorador se puede utilizar a nivel de controlador o de método.

Por ejemplo, para autenticar todas las rutas definidas en UserController, podemos usar el decorador @Authenticate() en el controlador:

```typescript
@Controller('/users')
@Authenticate()
export class UserController {
  // ...
}
```

Para autenticar solo ciertas rutas, podemos usar el decorador @Authenticate() en los métodos:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authenticate()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Nest.js también proporciona el decorador @Authorize() para la autorización. Este decorador se puede utilizar a nivel de controlador o de método.

Por ejemplo, para autorizar todas las rutas definidas en el UserController, podemos usar el decorador @Authorize() en el controlador:

```typescript
@Controller('/users')
@Authorize()
export class UserController {
  // ...
}
```

Para autorizar solo ciertas rutas, podemos usar el decorador @Authorize() en los métodos:

```typescript
@Controller('/users')
export class UserController {

  @Get('/')
  @Authorize()
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

## Acceso a la base de datos

Nest.js proporciona varias formas de acceder a las bases de datos.

La forma más común es usar el decorador @Inject() para inyectar un cliente de base de datos en su controlador o servicio.

Por ejemplo, para inyectar un cliente MongoDB en su controlador, puede usar el siguiente código:

```typescript
@Controller('/users')
export class UserController {

  constructor(
    @Inject('MONGODB_CLIENT') private mongodb: MongoClient,
  ) {}

  // ...

}
```

Otra forma de acceder a las bases de datos es usar el decorador @UseDatabases(). Este decorador se puede utilizar en un nivel de controlador o de servicio.

Por ejemplo, para usar MongoDB y PostgreSQL en su controlador, puede usar el siguiente código:

```typescript
@Controller('/users')
@UseDatabases(['MONGODB', 'POSTGRESQL'])
export class UserController {

  // ...

}
```

## Pruebas

Nest.js proporciona varias formas de probar sus aplicaciones.

La forma más común es usar el decorador @Test(). Este decorador se puede utilizar en un nivel de controlador o de servicio.

Por ejemplo, para probar UserController, puede usar el siguiente código:

```typescript
@Test()
export class UserController {

  @Get('/')
  index() {
    // ...
  }

  @Get('/:id')
  show() {
    // ...
  }

  @Post('/')
  store() {
    // ...
  }

  @Put('/:id')
  update() {
    // ...
  }

  @Delete('/:id')
  destroy() {
    // ...
  }

}
```

Otra forma de probar su aplicación es usar el decorador @TestModule(). Este decorador se puede utilizar a nivel de módulo.

Por ejemplo, para probar UserModule, puede usar el siguiente código:

```typescript
@TestModule()
export class UserModule {}
```

## Conclusión

En esta publicación, hemos cubierto algunas de las funciones y técnicas avanzadas que ofrece Nest.js.

Hemos visto cómo definir rutas, cómo autenticar y autorizar usuarios, cómo acceder a bases de datos y cómo probar aplicaciones Nest.js.

Si desea obtener más información sobre Nest.js, le recomiendo consultar la documentación oficial.