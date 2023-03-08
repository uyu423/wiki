---
title: Kotlin y Express.js: creación de una aplicación web con un marco de Node.js
description: 
published: true
date: 2023-02-05T12:55:28.085Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:55:22.668Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Express.js: Building a Web Application with a Node.js Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-express-js-building-a-web-application-with-a-node-js-framework)
{.links-list}


# Kotlin y Express.js: creación de una aplicación web con un marco Node.js

Kotlin es un lenguaje JVM que se puede usar para crear aplicaciones web utilizando una variedad de marcos. En este artículo, nos centraremos en el uso de Kotlin con el marco Express.js. Express.js es un marco de Node.js que proporciona un conjunto de herramientas para crear aplicaciones web. También es posible usar Kotlin con otros frameworks de Node.js, como Hapi.js y Koa.js.

## Configuración del proyecto

Para comenzar, necesitamos crear un nuevo proyecto Kotlin utilizando el marco Express.js. Podemos hacer esto usando la herramienta express-generator.

Primero, necesitamos instalar la herramienta usando npm:

```
npm install -g express-generator
```

A continuación, podemos usar la herramienta para generar un nuevo proyecto:

```
express --view=pug my-app
```

Esto creará un nuevo proyecto en el directorio my-app con el motor de plantillas Pug configurado.

## Ejecutando la aplicación

Ahora que tenemos un nuevo proyecto, podemos iniciar la aplicación ejecutando el siguiente comando en el directorio del proyecto:

```
npm start
```

Esto iniciará la aplicación en http://localhost:3000. Podemos acceder a la aplicación en nuestro navegador y deberíamos ver la página de bienvenida predeterminada de Express.js.

## Hola Mundo

Vamos a crear una ruta simple de "Hola mundo" para comenzar. Podemos hacer esto editando el archivo route/index.js.

Primero, necesitamos importar el enrutador Express.js:

```javascript
var express = require('express');
var router = express.Router();
```

A continuación, podemos agregar una nueva ruta para la ruta "/":

```javascript
router.get('/', function(req, res, next) {
  res.send('Hello world');
});
```

Esta ruta representará la cadena "Hola mundo" cuando accedamos a la ruta "/" en nuestro navegador.

## Conclusión

En este artículo, hemos visto cómo usar Kotlin y el marco Express.js para crear una aplicación web. También hemos visto cómo crear rutas y renderizar plantillas.

Para obtener más información sobre Kotlin y el desarrollo web, consulte los siguientes recursos:

- [Kotlin para el desarrollo del lado del servidor] (https://kotlinlang.org/docs/reference/server-overview.html)
- [Creación de una aplicación web con Kotlin, Spring Boot y MongoDB](https://www.baeldung.com/kotlin-mongodb-spring-boot)
- [Full-Stack Kotlin: desarrollo de aplicaciones web con React y Spring Boot](https://www.baeldung.com/kotlin-react-spring-boot)