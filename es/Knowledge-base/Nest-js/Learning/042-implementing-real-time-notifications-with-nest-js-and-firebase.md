---
title: 042: Implementación de notificaciones en tiempo real con Nest.js y Firebase
description: 
published: true
date: 2023-02-12T03:17:53.986Z
tags: 
editor: markdown
dateCreated: 2023-02-12T03:17:52.267Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [042: Implementing real-time notifications with Nest.js and Firebase***English** document is available*](/en/Knowledge-base/Nest-js/Learning/042-implementing-real-time-notifications-with-nest-js-and-firebase)
{.links-list}


# Implementando notificaciones en tiempo real con Nest.js y Firebase

En esta publicación, veremos cómo configurar notificaciones en tiempo real en una aplicación Nest.js usando el servicio Firebase Cloud Messaging (FCM).

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (que se compila en JavaScript) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Firebase es una plataforma de desarrollo de aplicaciones móviles y web desarrollada por Google. Proporciona una serie de servicios, uno de los cuales es FCM. FCM es una solución de mensajería multiplataforma que le permite entregar mensajes de manera confiable sin costo alguno.

## Configuración de un proyecto Nest.js

Comenzaremos configurando un nuevo proyecto Nest.js. Usaremos la CLI de Nest para esto. Si no lo tiene instalado, puede hacerlo ejecutando el siguiente comando:

```
$ npm install -g @nestjs/cli
```

Una vez instalada la CLI de Nest, podemos crear un nuevo proyecto ejecutando el siguiente comando:

```
$ nest new project-name
```

Esto creará un nuevo directorio con los archivos del proyecto.

## Instalando las dependencias

Necesitamos instalar las siguientes dependencias para nuestro proyecto:

- @nestjs/común
- @nestjs/plataforma-express
- firebase-admin

Podemos instalar estas dependencias ejecutando el siguiente comando:

```
$ npm install --save @nestjs/common @nestjs/platform-express firebase-admin
```

## Configuración de base de fuego

Necesitamos crear un nuevo proyecto de Firebase para usar FCM. Podemos hacerlo yendo a [Firebase console](https://console.firebase.google.com/) y haciendo clic en el botón "Crear un proyecto".

Asigne un nombre a su proyecto y haga clic en el botón "Crear proyecto".

Una vez creado el proyecto, haga clic en el botón "Agregar Firebase a su aplicación web".

Esto abrirá una ventana emergente con su configuración de Firebase. Necesitamos copiar el objeto de configuración y agregarlo al archivo `environment.ts` en nuestro proyecto. El archivo debería verse así:

```javascript
export const environment = {
  production: false,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

También necesitamos agregar la siguiente línea al archivo `environment.prod.ts`:

```javascript
export const environment = {
  production: true,
  firebase: {
    apiKey: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    authDomain: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    databaseURL: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    projectId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    storageBucket: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    messagingSenderId: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
  }
};
```

## Creando el servicio FCM

Necesitamos crear un nuevo servicio que maneje el envío de mensajes FCM. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ nest generate service fcm
```

Esto creará un nuevo archivo de servicio en el directorio `src/fcm`. Necesitamos importar el módulo `firebase-admin` y el archivo `environment`. También necesitamos crear una nueva instancia de la clase `admin.messaging.Messaging`. El servicio debería verse así:

```javascript
import { Injectable } from '@nestjs/common';
import * as admin from 'firebase-admin';
import { environment } from '../../environments/environment';

@Injectable()
export class FcmService {
  private readonly messaging = admin.messaging();

  constructor() {
    admin.initializeApp({
      credential: admin.credential.applicationDefault(),
      databaseURL: environment.firebase.databaseURL,
      projectId: environment.firebase.projectId
    });
  }

  // ...
}
```

## Envío de mensajes FCM

Necesitamos agregar un nuevo método a `FcmService` que enviará mensajes FCM. El método debe tomar un parámetro `to` que especifique el destinatario del mensaje y un parámetro `data` que contenga los datos que se enviarán.

El método debe devolver una `Promesa` que se resuelve cuando se envía el mensaje.

```javascript
  async send(to: string, data: any): Promise<void> {
    const message = {
      to,
      data
    };

    await this.messaging.send(message);
  }
```

## Creando el controlador

Necesitamos crear un nuevo controlador que llamará al método `send` de `FcmService`. Esto lo podemos hacer ejecutando el siguiente comando:

```
$ nest generate controller fcm
```

Esto creará un nuevo archivo de controlador en el directorio `src/fcm`. Necesitamos importar los módulos `FcmService` y `@nestjs/common`. También necesitamos inyectar `FcmService` en el controlador. El controlador debería verse así:

```javascript
import { Controller, Post, Body } from '@nestjs/common';
import { FcmService } from './fcm.service';

@Controller('fcm')
export class FcmController {
  constructor(private readonly fcmService: FcmService) {}

  @Post()
  async send(@Body('to') to: string, @Body('data') data: any): Promise<void> {
    await this.fcmService.send(to, data);
  }
}
```

## Probando el controlador

Podemos probar el controlador enviando una solicitud POST al punto final `/fcm` con un parámetro `to` y `data`. Podemos hacer esto usando la herramienta [Postman](https://www.getpostman.com/).

Deberíamos ver un mensaje de éxito en la consola de Postman si el mensaje se envió correctamente.

## Conclusión

En esta publicación, hemos visto cómo configurar notificaciones en tiempo real en una aplicación Nest.js usando el servicio Firebase Cloud Messaging (FCM).