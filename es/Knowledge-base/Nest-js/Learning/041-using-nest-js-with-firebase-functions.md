---
title: 041: Uso de Nest.js con funciones de Firebase
description: 
published: true
date: 2023-02-15T13:33:20.858Z
tags: 
editor: markdown
dateCreated: 2023-02-15T13:33:19.113Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [041: Using Nest.js with Firebase Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/041-using-nest-js-with-firebase-functions)
{.links-list}


# Uso de Nest.js con funciones de Firebase

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza JavaScript moderno, está construido con TypeScript (que proporciona JavaScript escrito) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva funcional.

Firebase Functions es una plataforma sin servidor que le permite ejecutar su código JavaScript en la nube sin tener que aprovisionar ni administrar ningún servidor. Las funciones pueden ser activadas por eventos de los productos de Firebase, como cambios en los datos en Firebase Realtime Database, registros de nuevos usuarios a través de Firebase Authentication o mensajes entrantes a través de Firebase Cloud Messaging.

En esta publicación, aprenderemos a usar Nest.js con las funciones de Firebase. Crearemos una aplicación sin servidor Nest.js simple que se ejecuta en Firebase Functions y responde a las solicitudes HTTP.

## Configuración del proyecto

Primero, creemos un nuevo proyecto Nest.js. Usaremos la CLI de Nest para generar un nuevo proyecto. Ejecute el siguiente comando para generar un nuevo proyecto:

```
$ nest new nest-firebase-functions
```

Esto creará un nuevo proyecto Nest.js en una carpeta llamada ```nest-firebase-functions```.

A continuación, debemos instalar el SDK de Firebase Functions para Node.js. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ npm install firebase-functions@latest firebase-admin@latest --save
```

Esto instalará las versiones más recientes de Firebase Functions SDK y Firebase Admin SDK.

## Escribiendo el código

Ahora que tenemos un proyecto Nest.js y los SDK de Firebase instalados, podemos escribir algo de código.

Abra el archivo ```src/main.ts``` y reemplace el contenido con lo siguiente:

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

import * as functions from 'firebase-functions';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(() => console.log('Nest.js is listening'));
}

export const api = functions.https.onRequest(bootstrap);
```

Echemos un vistazo a lo que está pasando aquí.

Primero, importamos ```NestFactory``` y ```AppModule``` desde ```@nestjs/core```.

A continuación, importamos todo el espacio de nombres ```firebase-functions```. Esto nos da acceso al objeto ```functions```, que usaremos para configurar nuestra función HTTP.

Luego, definimos una función ```async``` llamada ```bootstrap```. Esta función se llamará cuando se invoque nuestra función HTTP. La palabra clave ```await``` se utiliza para esperar a que se completen las operaciones asincrónicas.

Dentro de la función ```bootstrap```, creamos una nueva instancia ```NestFactory``` y pasamos nuestro ```AppModule```. Luego iniciamos el servidor Nest.js llamando al método ```listen```.

Finalmente, exportamos una función ```functions.https.onRequest``` que invoca nuestra función ```bootstrap```. Esto hará que se invoque nuestra aplicación Nest.js cuando se realice una solicitud HTTP al extremo ```/api```.

Ahora que tenemos el código, echemos un vistazo al archivo ```app.module.ts```. Este es el archivo que define nuestro módulo Nest.js.

Abra el archivo ```app.module.ts``` y reemplace el contenido con lo siguiente:

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

Este archivo define nuestro ```AppModule```, que es el módulo raíz de nuestra aplicación Nest.js.

Nuestro módulo importa el decorador ```Module``` de ```@nestjs/common```. Este decorador se usa para definir un módulo Nest.js.

Nuestro módulo también importa ```AppController``` y ```AppService``` de la carpeta ```./app```. Echaremos un vistazo a estos archivos en un momento.

El decorador ```@Module``` se utiliza para configurar nuestro módulo. La propiedad ```imports``` se usa para importar otros módulos. La propiedad ```controllers``` se usa para especificar los controladores que están definidos en nuestro módulo. La propiedad ```providers``` se usa para especificar los proveedores que están definidos en nuestro módulo.

Ahora que hemos visto el archivo ```app.module.ts```, echemos un vistazo al archivo ```app.controller.ts```. Este archivo define nuestro ```AppController```.

Abra el archivo ```app.controller.ts``` y reemplace el contenido con lo siguiente:

```typescript
import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

Nuestro controlador importa los decoradores ```Controller``` y ```Get``` de ```@nestjs/common```. Estos decoradores se utilizan para definir un controlador y una acción de controlador respectivamente.

Nuestro controlador también importa ```AppService``` de la carpeta ```./app```. Echaremos un vistazo a este archivo en un momento.

El decorador ```@Controller``` se usa para definir un controlador. La sintaxis ```@Controller('/')``` especifica la ruta en la que se podrá acceder a las acciones de nuestro controlador. En nuestro caso, las acciones del controlador serán accesibles en la ruta raíz (```/```).

El decorador ```@Get()``` se utiliza para definir una acción de controlador. La sintaxis ```@Get('/')``` especifica la ruta en la que se podrá acceder a la acción de nuestro controlador. En nuestro caso, la acción del controlador será accesible en la ruta raíz (```/```).

El método ```getHello``` es nuestra acción de controlador. Este método se invoca cuando se realiza una solicitud HTTP GET al extremo ```/```. El método ```getHello``` devuelve una cadena, que se enviará de vuelta al cliente en la respuesta HTTP.

Ahora que hemos visto el archivo ```app.controller.ts```, echemos un vistazo al archivo ```app.service.ts```. Este archivo define nuestro ```AppService```.

Abra el archivo ```app.service.ts``` y reemplace el contenido con lo siguiente:

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```

Nuestro servicio importa el decorador ```Inyectable``` de ```@nestjs/common```. Este decorador se utiliza para definir un servicio.

El decorador ```@Injectable()``` se utiliza para configurar nuestro servicio.

El método ```getHello``` es un método simple que devuelve una cadena. Este método es invocado por nuestra acción de controlador.

## Desplegando el código

Ahora que hemos escrito nuestro código, debemos implementarlo en Firebase.

Primero, necesitamos crear un proyecto de Firebase. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ firebase init
```

Esto creará un nuevo proyecto de Firebase en el directorio actual.

A continuación, debemos implementar nuestro código en Firebase. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ firebase deploy
```

Esto implementará nuestro código en Firebase.

## Probando el código

Ahora que nuestro código está desplegado, vamos a probarlo.

Podemos probar nuestro código haciendo una solicitud HTTP al punto final ```/api```. Podemos hacer esto usando el comando ```curl```. Ejecute el siguiente comando para realizar una solicitud HTTP:

```
$ curl https://{your-firebase-project-id}.firebaseio.com/api
```

Esto hará una solicitud HTTP al extremo ```/api``` e imprimirá la respuesta en la consola.

## Conclusión

En esta publicación, aprendimos a usar Nest.js con las funciones de Firebase. Creamos una aplicación sin servidor Nest.js simple que se ejecuta en Firebase Functions y responde a las solicitudes HTTP.