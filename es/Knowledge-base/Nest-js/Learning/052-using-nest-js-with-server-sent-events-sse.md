---
title: 052: uso de Nest.js con eventos enviados por el servidor (SSE)
description: 
published: true
date: 2023-02-05T18:55:21.302Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:55:19.666Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [052: Using Nest.js with Server-Sent Events (SSE)***English** document is available*](/en/Knowledge-base/Nest-js/Learning/052-using-nest-js-with-server-sent-events-sse)
{.links-list}


# Uso de Nest.js con eventos enviados por el servidor (SSE)

En esta publicación, veremos cómo usar Nest.js con eventos enviados por el servidor (SSE). Nest.js es un marco de Node.js que lo ayuda a crear fácilmente aplicaciones del lado del servidor. SSE es una tecnología que le permite enviar datos de un servidor a un cliente en tiempo real.

Comenzaremos configurando un proyecto Nest.js. Luego, crearemos un controlador que enviará datos a nuestro cliente mediante SSE. Finalmente, crearemos un cliente que recibirá los datos del servidor.

## Configuración de un proyecto Nest.js

Primero, creemos un nuevo proyecto Nest.js. Podemos usar Nest CLI para generar un nuevo proyecto. Ejecute el siguiente comando:

```
nest new sse-project
```

Esto creará un nuevo proyecto Nest.js en un directorio llamado `sse-project`.

## Creando un controlador

A continuación, creemos un controlador que enviará datos a nuestro cliente. Cree un nuevo archivo llamado `src/controllers/data.controller.ts` y agregue el siguiente código:

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';

@Controller('data')
export class DataController {
  @Get()
  getData(@Res() res: Response) {
    // Set the content type of the response to "text/event-stream"
    res.setHeader('Content-Type', 'text/event-stream');
    // Push some data to the client
    res.write('data: This is some data\n\n');
    // Close the connection
    res.end();
  }
}
```

En este controlador, tenemos un método `getData` que está decorado con el decorador `@Get`. Se llamará a este método cuando un cliente realice una solicitud `GET` al punto final `/data`.

El decorador `@Res` inyecta el objeto `express` `Response` en el método. Usamos este objeto para establecer el encabezado `Content-Type` de la respuesta a `text/event-stream` y enviar datos al cliente.

## Creando un cliente

Ahora que tenemos un servidor que puede enviar datos a un cliente, creemos un cliente que pueda recibir los datos. Cree un nuevo archivo llamado `client.html` y agregue el siguiente código:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>SSE Client</title>
  </head>
  <body>
    <h1>SSE Client</h1>
    <div id="data">
      <!-- Data from the server will be placed here -->
    </div>
    <script>
      const source = new EventSource('http://localhost:3000/data');
      source.onmessage = (event) => {
        const data = event.data;
        document.getElementById('data').innerHTML = data;
      };
    </script>
  </body>
</html>
```

En este archivo, tenemos un elemento `<div>` con un `id` de `data`. Aquí es donde se colocarán los datos del servidor.

También tenemos un elemento `<script>` que crea un nuevo objeto `EventSource`. Este objeto se conectará al punto final `/data` en nuestro servidor. Luego registramos un controlador de eventos `onmessage` que se llamará cuando el servidor envíe datos al cliente.

## Ejecutando la aplicación

Ahora que tenemos un servidor y un cliente, ejecutemos la aplicación. Primero, inicie el servidor ejecutando el siguiente comando:

```
nest start
```

Luego, abra el archivo `client.html` en un navegador. Debería ver los datos del servidor que se muestran en el navegador.