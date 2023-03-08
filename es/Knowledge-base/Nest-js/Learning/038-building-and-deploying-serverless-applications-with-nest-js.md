---
title: 038: Creación e implementación de aplicaciones sin servidor con Nest.js
description: 
published: true
date: 2023-02-12T14:18:02.637Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:17:55.775Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [038: Building and deploying serverless applications with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/038-building-and-deploying-serverless-applications-with-nest-js)
{.links-list}


# 038: Creación e implementación de aplicaciones sin servidor con Nest.js

En esta publicación, aprenderemos cómo crear e implementar aplicaciones sin servidor con Nest.js.

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (que proporciona escritura sólida) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Nest.js es una excelente opción para crear aplicaciones sin servidor. Es liviano y rápido, y ofrece una amplia gama de funciones, como soporte para TypeScript, un sistema de inyección de dependencia fácil de usar y un poderoso sistema de módulos.

Crear una aplicación sin servidor con Nest.js es rápido y fácil. En esta publicación, veremos los pasos para crear una aplicación Nest.js sin servidor simple e implementarla en AWS Lambda.

## Crear una aplicación Nest.js

Primero, necesitamos crear una nueva aplicación Nest.js. Podemos usar la CLI de Nest para generar un nuevo proyecto:

```
nest new serverless-app
```

Esto creará una nueva carpeta llamada `serverless-app` con los archivos y carpetas básicos necesarios para una aplicación Nest.js.

A continuación, debemos instalar el paquete `@nestjs/serverless`. Este paquete proporciona los módulos y las dependencias necesarios para crear una aplicación Nest.js sin servidor:

```
npm install --save @nestjs/serverless
```

Ahora que tenemos instalado el paquete `@nestjs/serverless`, podemos crear una nueva aplicación Nest.js sin servidor.

Comenzaremos creando un nuevo archivo llamado `main.ts` en la carpeta `src`. Este archivo será el punto de entrada para nuestra aplicación Nest.js sin servidor.

En `main.ts`, necesitamos importar la clase `NestFactory` del paquete `@nestjs/core`. Esta clase se usará para crear una nueva aplicación Nest.js:

```typescript
import { NestFactory } from '@nestjs/core';
```

A continuación, debemos importar el `ServerlessApplicationModule` del paquete `@nestjs/serverless`. Este módulo se usará para iniciar nuestra aplicación Nest.js:

```typescript
import { ServerlessApplicationModule } from '@nestjs/serverless';
```

Ahora que hemos importado las clases `NestFactory` y `ServerlessApplicationModule`, podemos usarlas para crear una nueva aplicación Nest.js:

```typescript
async function bootstrap() {
  const app = await NestFactory.create(ServerlessApplicationModule);
  await app.listen(3000);
}
bootstrap();
```

En el código anterior, usamos la clase `NestFactory` para crear una nueva aplicación Nest.js. Estamos pasando `ServerlessApplicationModule` al método `create` para iniciar la aplicación.

Finalmente, estamos usando el método `listen` para iniciar la aplicación en el puerto 3000.

## Creando un controlador

Ahora que hemos creado nuestra aplicación Nest.js, creemos un controlador. Los controladores son responsables de manejar las solicitudes HTTP entrantes y devolver las respuestas.

En Nest.js, los controladores se crean como clases. Vamos a crear un nuevo archivo llamado `hello.controller.ts` en la carpeta `src/controllers`.

En `hello.controller.ts`, necesitamos importar el decorador `Controller` del paquete `@nestjs/common`. Este decorador se usa para marcar una clase como controlador:

```typescript
import { Controller } from '@nestjs/common';
```

A continuación, debemos importar el decorador `Get` del paquete `@nestjs/common`. Este decorador se utiliza para marcar un método de controlador como controlador para una solicitud HTTP `GET`:

```typescript
import { Get } from '@nestjs/common';
```

Ahora que hemos importado los decoradores `Controller` y `Get`, podemos usarlos para crear un controlador:

```typescript
@Controller('hello')
export class HelloController {
  @Get()
  hello() {
    return 'Hello, world!';
  }
}
```

En el código anterior, hemos creado un controlador llamado `HelloController`. Este controlador tiene un método llamado `hola` que devuelve la cadena `¡Hola, mundo!`.

También hemos usado el decorador `Controller` para especificar la ruta de este controlador. En este caso, hemos especificado la ruta como `hola`. Esto significa que el método `hello` se invocará cuando se realice una solicitud `GET` en la ruta `/hello`.

## Registro del controlador

Ahora que hemos creado nuestro controlador, debemos registrarlo con nuestra aplicación Nest.js.

Podemos hacer esto importando el controlador en `main.ts` y pasándolo al método `NestFactory.create`:

```typescript
import { HelloController } from './controllers/hello.controller';

async function bootstrap() {
  const app = await NestFactory.create(
    ServerlessApplicationModule,
    {
      controllers: [HelloController],
    },
  );
  await app.listen(3000);
}
bootstrap();
```

En el código anterior, hemos importado `HelloController` desde `hello.controller.ts`. Luego lo pasamos a la matriz `controllers` en el método `NestFactory.create`.

Esto registrará `HelloController` con nuestra aplicación Nest.js.

## Desplegando la aplicación

Ahora que hemos creado nuestra aplicación Nest.js y registrado nuestro controlador, estamos listos para implementar nuestra aplicación.

Implementaremos nuestra aplicación en AWS Lambda. Lambda es una plataforma sin servidor que nos permite ejecutar código sin aprovisionar ni administrar servidores.

Para implementar nuestra aplicación en Lambda, usaremos el comando `nest deployment`. Este comando empaquetará nuestra aplicación y la implementará en Lambda:

```
nest deploy
```

Este comando creará una nueva función Lambda e implementará nuestra aplicación Nest.js en ella.

Una vez que se completa la implementación, podemos probar nuestra aplicación haciendo una solicitud `GET` a la ruta `/hello`. Deberíamos ver la cadena `Hello, world!` devuelta.

## Conclusión

En esta publicación, aprendimos cómo crear e implementar aplicaciones sin servidor con Nest.js.

Nest.js es una excelente opción para crear aplicaciones sin servidor. Es liviano y rápido, y ofrece una amplia gama de funciones, como soporte para TypeScript, un sistema de inyección de dependencia fácil de usar y un poderoso sistema de módulos.

Crear una aplicación sin servidor con Nest.js es rápido y fácil. En esta publicación, repasamos los pasos para crear una aplicación Nest.js sin servidor simple e implementarla en AWS Lambda.