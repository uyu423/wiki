---
title: 032: Uso de Nest.js con TypeScript
description: 
published: true
date: 2023-02-12T09:55:33.730Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:55:32.034Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [032: Using Nest.js with TypeScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/032-using-nest-js-with-typescript)
{.links-list}


# Uso de Nest.js con TypeScript

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza TypeScript, un superconjunto escrito de JavaScript que se compila en JavaScript simple.

En esta publicación, le mostraremos cómo usar Nest.js con TypeScript. Seguiremos los pasos para configurar un proyecto Nest.js, configurar TypeScript y escribir un controlador simple.

## Configuración de un proyecto Nest.js

Primero, creemos un nuevo proyecto Nest.js. Usaremos la CLI de Nest para generar un esqueleto de proyecto:

```
$ nest new project-name
```

Esto creará un nuevo directorio llamado `nombre-del-proyecto` con la siguiente estructura:

```
project-name
├── README.md
├── node_modules
├── package-lock.json
├── package.json
├── tsconfig.json
└── tslint.json
```

A continuación, instalemos las dependencias para nuestro proyecto:

```
$ cd project-name
$ npm install
```

## Configuración de mecanografiado

Nest.js usa TypeScript de forma predeterminada, por lo que no es necesario instalarlo por separado. Sin embargo, necesitamos configurarlo.

Abra `tsconfig.json` y agregue las siguientes opciones:

```js
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "outDir": "dist",
    "strict": true
  }
}
```

Estas opciones compilarán nuestro código TypeScript en ES6 y usarán el formato del módulo CommonJS. La opción `outDir` especifica el directorio de salida para los archivos JavaScript compilados. Y la opción 'estricta' habilita la verificación estricta de tipos.

## Escribiendo un controlador

Ahora que nuestro proyecto está configurado, podemos escribir un controlador. Los controladores son responsables de manejar las solicitudes HTTP y devolver las respuestas.

Vamos a crear un archivo llamado `src/controllers/hello.controller.ts`:

```ts
import { Controller, Get } from '@nestjs/common';

@Controller('hello')
export class HelloController {
  @Get()
  public async index(): Promise<string> {
    return 'Hello, world!';
  }
}
```

Este controlador tiene una única ruta `@Get`, que devuelve la cadena `'¡Hola, mundo!'`.

Para registrar este controlador con Nest.js, necesitamos crear un módulo. Vamos a crear un archivo llamado `src/modules/hello.module.ts`:

```ts
import { Module } from '@nestjs/common';
import { HelloController } from '../controllers/hello.controller';

@Module({
  controllers: [HelloController]
})
export class HelloModule {}
```

Este módulo importa `HelloController` y lo registra con Nest.js.

Finalmente, debemos decirle a Nest.js que use este módulo. Podemos hacer esto agregándolo al archivo `app.module.ts`:

```ts
import { Module } from '@nestjs/common';
import { HelloModule } from './modules/hello.module';

@Module({
  imports: [HelloModule]
})
export class AppModule {}
```

Ahora que nuestro controlador está registrado, podemos iniciar el servidor Nest.js:

```
$ npm start
```

Y abra http://localhost:3000/hello en su navegador. Deberías ver la cadena `'¡Hola, mundo!'`.

## Conclusión

En esta publicación, le mostramos cómo usar Nest.js con TypeScript. Configuramos un proyecto Nest.js, configuramos TypeScript y escribimos un controlador simple.