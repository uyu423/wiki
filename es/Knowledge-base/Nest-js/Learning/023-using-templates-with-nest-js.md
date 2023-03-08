---
title: 023: Uso de plantillas con Nest.js
description: 
published: true
date: 2023-02-15T04:32:32.693Z
tags: 
editor: markdown
dateCreated: 2023-02-15T04:32:31.156Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [023: Using templates with Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/023-using-templates-with-nest-js)
{.links-list}


## Introducción

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript, un lenguaje que proporciona verificación de tipo estático y herramientas potentes para el desarrollo a gran escala.

Las aplicaciones de Nest.js se crean con un enfoque modular, lo que permite a los desarrolladores dividir su código en partes más pequeñas que se pueden reutilizar en toda la aplicación. Nest.js viene con un sistema de inyección de dependencia integrado que facilita la inyección de servicios y otras dependencias en los componentes.

Una de las características más poderosas de Nest.js es el uso de plantillas. Las plantillas de Nest.js se basan en el popular sistema de plantillas AngularJS y proporcionan una forma de modularizar su HTML y reducir la cantidad de código que tiene que escribir.

En esta publicación, veremos cómo usar plantillas con Nest.js. Comenzaremos creando una aplicación Nest.js simple y luego le agregaremos una plantilla. Finalmente, aprenderemos a usar la plantilla para representar datos de una base de datos.

## Crear una aplicación Nest.js

Comencemos por crear una nueva aplicación Nest.js. Usaremos la CLI de Nest.js para generar una nueva aplicación. Primero, asegúrese de tener instalada la CLI de Nest.js. Si no lo tiene instalado, puede instalarlo usando npm:

```
npm install -g @nestjs/cli
```

Una vez que se instala la CLI de Nest.js, podemos usarla para generar una nueva aplicación. Llamaremos a nuestra aplicación "plantilla-aplicación":

```
nest new template-app
```

Esto creará un nuevo directorio llamado "template-app" y generará los archivos necesarios para una aplicación Nest.js básica.

## Agregar una plantilla

Ahora que tenemos una aplicación Nest.js básica, vamos a agregarle una plantilla. Nest.js viene con un motor de plantillas incorporado llamado Nest.js View. Nest.js View se basa en el popular motor de plantillas AngularJS y proporciona una forma de modularizar su HTML y reducir la cantidad de código que tiene que escribir.

Para agregar una plantilla a nuestra aplicación Nest.js, debemos crear un nuevo archivo llamado "template.html" en el directorio "src/views". El directorio "src/views" es donde Nest.js busca plantillas.

En nuestro archivo "template.html", agregaremos una plantilla HTML simple:

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```

Ahora que tenemos nuestra plantilla, usémosla en nuestra aplicación Nest.js.

## Uso de la plantilla

Para usar nuestra plantilla, debemos decirle a Nest.js dónde encontrarla. Podemos hacer esto agregando una propiedad de "plantilla" al objeto "ver" en el archivo "src/main.ts":

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  await app.listen(3000);
}
bootstrap();
```

La propiedad "plantilla" le dice a Nest.js dónde encontrar nuestro archivo de plantilla. En este caso, le estamos diciendo a Nest.js que busque el archivo "template.html" en el directorio "src/views".

Ahora que le hemos dicho a Nest.js dónde encontrar nuestra plantilla, podemos usarla para representar datos.

## Representación de datos

Para renderizar datos en nuestra plantilla, necesitamos usar la función "renderizar". La función "renderizar" toma dos argumentos: un objeto de datos y un objeto de respuesta. El objeto de datos contiene los datos que queremos representar y el objeto de respuesta se utiliza para enviar el HTML representado al cliente.

Echemos un vistazo a un ejemplo. En este ejemplo, mostraremos una lista de usuarios en nuestra plantilla:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  app.setViewEngine({
    type: 'html',
    template: './src/views/template.html',
  });

  app.get('/users', (req, res) => {
    const users = [
      {
        name: 'John Doe',
        age: 30,
      },
      {
        name: 'Jane Doe',
        age: 31,
      },
    ];

    res.render('users', { users });
  });

  await app.listen(3000);
}
bootstrap();
```

En este ejemplo, agregamos una nueva ruta a nuestra aplicación Nest.js que muestra una lista de usuarios. Estamos utilizando la función "renderizar" para representar la plantilla de "usuarios" y pasar un objeto de datos que contiene una lista de usuarios.

Ahora que hemos visto cómo representar datos en una plantilla Nest.js, echemos un vistazo a cómo acceder a los datos en nuestra plantilla.

## Acceso a datos en la plantilla

Para acceder a los datos en la plantilla, usamos el argumento "datos" de la función "renderizar". El argumento "datos" es un objeto que contiene los datos que queremos representar.

En nuestro archivo "template.html", podemos acceder a los datos que pasamos usando la función "render" de esta manera:

```html
<html>
  <head>
    <title>Template App</title>
  </head>
  <body>
    <h1>Users</h1>
    <ul>
      <li>
        {{ users[0].name }} - {{ users[0].age }}
      </li>
      <li>
        {{ users[1].name }} - {{ users[1].age }}
      </li>
    </ul>
  </body>
</html>
```

En este ejemplo, estamos usando el argumento "datos" de la función "renderizar" para acceder a la lista de usuarios que pasamos. Luego estamos recorriendo la lista de usuarios y mostrando su nombre y edad.

Ahora que hemos visto cómo usar plantillas con Nest.js, echemos un vistazo a algunos recursos para leer más.

## Recursos para lecturas adicionales

- [Vista de Nest.js](https://docs.nestjs.com/v/6/view)
- [AngularJS](https://angularjs.org/)
- [Manillares](https://handlebarsjs.com/)