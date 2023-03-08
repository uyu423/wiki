---
title: Creación de API RESTful con Nest.js y TypeScript
description: 
published: true
date: 2023-02-15T14:55:40.868Z
tags: 
editor: markdown
dateCreated: 2023-02-15T14:55:39.210Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building RESTful APIs with Nest.js and TypeScript***English** document is available*](/en/Knowledge-base/TypeScript/building-restful-apis-with-nest-js-and-typescript)
{.links-list}


# Creación de API RESTful con Nest.js y TypeScript

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor. Utiliza TypeScript, un superconjunto de JavaScript que agrega verificación de tipos estáticos y otras funciones, y proporciona una buena plataforma para crear API RESTful.

En este artículo, veremos cómo crear una API RESTful con Nest.js y TypeScript. Comenzaremos observando la estructura del proyecto y luego pasaremos a crear los puntos finales de la API. También veremos cómo usar TypeScript con Nest.js.

## Estructura del proyecto

La estructura de un proyecto de Nest.js es similar a la de un proyecto de Node.js. Hay un directorio src para el código fuente y un directorio de prueba para las pruebas. El directorio src contiene un archivo main.ts, que es el punto de entrada para la aplicación. El directorio de pruebas contiene un archivo main.spec.ts, que es el punto de entrada para las pruebas.

El proyecto también tiene un archivo tsconfig.json, que se usa para configurar el compilador de TypeScript. El archivo contiene opciones para el compilador, como la versión de JavaScript de destino y el tipo de módulo.

El proyecto también tiene un archivo package.json, que contiene metadatos para el proyecto, como las dependencias y las secuencias de comandos.

## Creación de los puntos finales de la API

Lo primero que debemos hacer es crear los puntos finales de la API. Haremos esto en el archivo src/main.ts.

Comenzaremos importando el módulo Express y creando una aplicación Express. También importaremos el módulo body-parser y el módulo cors.

```javascript
import * as express from 'express';
import * as bodyParser from 'body-parser';
import * as cors from 'cors';

const app = express();
```

A continuación, configuraremos la aplicación Express. Estableceremos el puerto en 3000 y habilitaremos el analizador de cuerpo y el middleware cors.

```javascript
app.set('port', 3000);
app.use(bodyParser.json());
app.use(cors());
```

Ahora, crearemos los puntos finales de la API. Comenzaremos con un punto final GET para recuperar una lista de usuarios.

```javascript
app.get('/users', (req, res) => {
  // ...
});
```

A continuación, crearemos un punto final POST para crear un nuevo usuario.

```javascript
app.post('/users', (req, res) => {
  // ...
});
```

Finalmente, crearemos un punto final PUT para actualizar un usuario existente.

```javascript
app.put('/users/:id', (req, res) => {
  // ...
});
```

## Uso de TypeScript con Nest.js

Nest.js y TypeScript funcionan bien juntos. Nest.js proporciona decoradores que facilitan el uso de TypeScript con Nest.js.

Por ejemplo, el decorador @Controller se puede usar para crear un controlador. El decorador @Get se puede usar para crear un punto final GET. El decorador @Post se puede usar para crear un punto final POST.

```typescript
import { Controller, Get, Post, Put } from '@nestjs/common';

@Controller('/users')
export class UserController {

  @Get()
  getUsers() {
    // ...
  }

  @Post()
  createUser() {
    // ...
  }

  @Put(':id')
  updateUser() {
    // ...
  }

}
```