---
title: 053: Uso de Nest.js con WebRTC para comunicación en tiempo real
description: 
published: true
date: 2023-02-06T23:55:58.403Z
tags: 
editor: markdown
dateCreated: 2023-02-06T23:55:56.702Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [053: Using Nest.js with WebRTC for real-time communication***English** document is available*](/en/Knowledge-base/Nest-js/Learning/053-using-nest-js-with-webrtc-for-real-time-communication)
{.links-list}


# 05: Uso de Nest.js con WebRTC para comunicación en tiempo real

WebRTC es una herramienta poderosa que se puede usar para una variedad de aplicaciones, incluida la comunicación en tiempo real. Nest.js es un marco de Node.js que se puede usar para crear aplicaciones escalables. En esta publicación, le mostraremos cómo usar Nest.js con WebRTC para crear una aplicación de comunicación en tiempo real.

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá tener para seguir. Primero, deberá tener instalados Node.js y npm. Puede encontrar instrucciones sobre cómo hacerlo aquí: [Node.js](https://nodejs.org/en/download/) y [npm](https://www.npmjs.com/get-npm).

A continuación, deberá instalar la CLI de Nest.js. Puede hacer esto ejecutando el siguiente comando:

```
npm install -g @nestjs/cli
```

## Crear un proyecto Nest.js

Ahora que tiene instalada la CLI de Nest.js, puede usarla para crear un nuevo proyecto de Nest.js. Para hacer esto, ejecute el siguiente comando:

```
nest new project-name
```

Reemplace "nombre del proyecto" con el nombre de su proyecto. Esto creará un nuevo directorio con el mismo nombre e inicializará un nuevo proyecto Nest.js dentro de él.

## Instalando dependencias

Ahora que tiene un proyecto Nest.js, deberá instalar algunas dependencias. La primera dependencia que necesitará es [Socket.io](https://socket.io/). Socket.io es una biblioteca de comunicación en tiempo real que se utilizará para manejar la comunicación entre el cliente y el servidor. Para instalarlo, ejecute el siguiente comando:

```
npm install socket.io
```

La siguiente dependencia que necesitará es [Express](https://expressjs.com/). Express es un marco de aplicación web para Node.js que se utilizará para servir los archivos estáticos para el cliente. Para instalarlo, ejecute el siguiente comando:

```
npm install express
```

## Configurando Socket.io

Ahora que tiene las dependencias instaladas, deberá configurar Socket.io. Para hacer esto, abra el archivo "src/main.ts" y agregue el siguiente código:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import * as socketIo from 'socket.io';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  const server = app.getHttpServer();
  const io = socketIo(server);

  app.useStaticAssets(join(__dirname, '..', 'public'));
  app.setBaseViewsDir(join(__dirname, '..', 'views'));
  app.setViewEngine('hbs');

  await app.listen(3000);
}
bootstrap();
```

Este código configurará Socket.io para usar el servidor Nest.js. También configurará Express para servir los archivos estáticos del directorio "público" y las vistas del directorio "vistas".

## Creando el controlador

Ahora que ha configurado Socket.io, puede crear el controlador. Para hacer esto, ejecute el siguiente comando:

```
nest generate controller controller-name
```

Reemplace "nombre del controlador" con el nombre de su controlador. Esto generará un nuevo archivo en el directorio "src/controllers" con el nombre "controller-name.controller.ts".

Abra el archivo "src/controllers/controller-name.controller.ts" y agregue el siguiente código:

```javascript
import { Controller, Post, Body, Req, UseGuards } from '@nestjs/common';
import { Socket } from 'socket.io';
import { AuthGuard } from '@nestjs/passport';

@Controller('controller-name')
export class ControllerNameController {

  @UseGuards(AuthGuard())
  @Post('message')
  async message(@Req() req, @Body() body, @Socket() socket: Socket) {
    socket.emit('message', body);
  }

}
```

Este código crea un controlador con un solo punto final. El punto final es una solicitud POST que acepta el cuerpo de un mensaje. Luego, el mensaje se emite al cliente mediante Socket.io.

## Creando la vista

Ahora que ha creado el controlador, puede crear la vista. Para hacer esto, cree un nuevo archivo en el directorio "vistas" con el nombre "index.hbs". Agregue el siguiente código al archivo "index.hbs":

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>WebRTC with Nest.js</title>
  </head>
  <body>
    <form id="form">
      <input type="text" id="message">
      <button type="submit">Send</button>
    </form>
    <div id="messages"></div>
    <script src="/socket.io/socket.io.js"></script>
    <script>
      const socket = io();
      const form = document.getElementById('form');
      const message = document.getElementById('message');
      const messages = document.getElementById('messages');

      form.addEventListener('submit', (e) => {
        e.preventDefault();
        socket.emit('message', message.value);
        message.value = '';
      });

      socket.on('message', (msg) => {
        const li = document.createElement('li');
        li.innerHTML = msg;
        messages.appendChild(li);
      });
    </script>
  </body>
</html>
```

Este código crea un formulario HTML simple que permite al usuario ingresar un mensaje. Luego, el mensaje se emite al servidor utilizando Socket.io. El servidor entonces emitirá el mensaje a todos los clientes. El mensaje se mostrará en la página.

## Ejecutando la aplicación

Ahora que tiene la aplicación creada, puede ejecutarla ejecutando el siguiente comando:

```
npm start
```

Luego puede acceder a la aplicación en http://localhost:3000.

## Conclusión

En esta publicación, le mostramos cómo usar Nest.js con WebRTC para crear una aplicación de comunicación en tiempo real. También le mostramos cómo usar Socket.io para manejar la comunicación entre el cliente y el servidor.