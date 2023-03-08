---
title: 039: Uso de Nest.js con AWS Lambda
description: 
published: true
date: 2023-02-09T03:17:45.418Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:17:43.709Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [039: Using Nest.js with AWS Lambda***English** document is available*](/en/Knowledge-base/Nest-js/Learning/039-using-nest-js-with-aws-lambda)
{.links-list}


# 039: Uso de Nest.js con AWS Lambda

AWS Lambda es una plataforma informática sin servidor que le permite ejecutar código sin aprovisionar ni administrar servidores. Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables.

En esta publicación, le mostraremos cómo usar Nest.js con AWS Lambda. Crearemos una aplicación Nest.js simple y la implementaremos en AWS Lambda.

## Crear una aplicación Nest.js

Primero, necesitamos crear una aplicación Nest.js. Podemos usar la CLI de Nest.js para generar un nuevo proyecto.

```
$ nest new nest-lambda
```

Esto creará un nuevo proyecto Nest.js en una carpeta llamada `nest-lambda`.

A continuación, debemos instalar el paquete `@nestjs/aws-lambda`. Este paquete proporciona un adaptador Nest.js para AWS Lambda.

```
$ cd nest-lambda
$ npm install --save @nestjs/aws-lambda
```

Ahora que tenemos instalado el paquete `@nestjs/aws-lambda`, podemos crear un nuevo archivo llamado `main.ts` en la carpeta `src`. Este archivo contendrá nuestra aplicación Nest.js.

```typescript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

En este archivo, importamos `NestFactory` y `AppModule` de Nest.js. Luego usamos `NestFactory` para crear una nueva aplicación Nest.js. Pasamos nuestro `AppModule` a `NestFactory`. Finalmente, llamamos al método `listen` para iniciar la aplicación Nest.js en el puerto 3000.

## Implementación en AWS Lambda

Ahora que tenemos una aplicación Nest.js, podemos implementarla en AWS Lambda. Primero, necesitamos crear una cuenta de AWS. Una vez que tenga una cuenta, puede crear una nueva función de AWS Lambda.

En la consola de Lambda, haga clic en el botón "Crear función".

![crear-función](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-create-function.png)

En la página "Crear función", seleccione la opción "Crear desde cero".

![autor desde cero](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-author-from-scratch.png)

En la página "Configurar función", ingrese un nombre para su función y seleccione el tiempo de ejecución "Node.js 12.x". Luego, desplácese hacia abajo y haga clic en el botón "Crear función".

![configurar-función](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-function.png)

Una vez que se haya creado la función, debería ver el editor "Código de función". En este editor, agregaremos nuestro código de aplicación Nest.js.

Primero, necesitamos instalar el paquete `@nestjs/aws-lambda`. Podemos hacer esto usando el comando `npm`.

```
$ npm install --save @nestjs/aws-lambda
```

A continuación, agregaremos nuestro archivo `main.ts` al editor de "Código de función".

![código de función](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-function-code.png)

Una vez que hayamos agregado nuestro código, debemos seleccionar el "Manejador" para nuestra función. El controlador es el punto de entrada para nuestra función Lambda. En nuestro caso, el controlador es `main.handler`.

![manejador](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-handler.png)

Ahora que hemos configurado nuestra función, podemos desplazarnos hacia abajo y hacer clic en el botón "Guardar".

![guardar](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-save.png)

Una vez que se ha guardado la función, podemos probarla haciendo clic en el botón "Test".

![prueba](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test.png)

En la página "Configurar evento de prueba", podemos crear un nuevo evento de prueba. En este caso, estableceremos `httpMethod` en `GET` y `path` en `/`. Luego, haremos clic en el botón "Crear".

![configurar-evento-de-prueba](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-configure-test-event.png)

Una vez que se ha creado el evento de prueba, podemos hacer clic en el botón "Probar" para ejecutar nuestra función.

![prueba-2](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-test-2.png)

Si todo salió bien, debería ver la sección "Resultado de la ejecución" con un código de estado `200`.

![resultado de ejecución](https://raw.githubusercontent.com/nestjs/nest/master/docs/assets/lambda-execution-result.png)

## Conclusión

En esta publicación, le mostramos cómo usar Nest.js con AWS Lambda. Creamos una aplicación Nest.js simple y la implementamos en AWS Lambda.