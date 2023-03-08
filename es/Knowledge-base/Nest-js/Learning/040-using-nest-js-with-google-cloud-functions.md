---
title: 040: Uso de Nest.js con las funciones de Google Cloud
description: 
published: true
date: 2023-02-15T12:32:37.764Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:32:36.062Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [040: Using Nest.js with Google Cloud Functions***English** document is available*](/en/Knowledge-base/Nest-js/Learning/040-using-nest-js-with-google-cloud-functions)
{.links-list}


# Usar Nest.js con Google Cloud Functions

Google Cloud Functions es una plataforma sin servidor que le permite ejecutar su código sin tener que preocuparse por el aprovisionamiento o la administración de servidores. Puede escribir código en una variedad de lenguajes, incluidos JavaScript, Python y Go.

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza JavaScript moderno, está construido con TypeScript (que trae la verificación de tipo estático a JavaScript) y combina elementos de programación funcional y orientada a objetos.

En esta publicación, le mostraremos cómo usar Nest.js con Google Cloud Functions. Crearemos una función simple que devuelva una lista de usuarios de una base de datos MongoDB.

## 1. Crea un nuevo proyecto

Primero, necesitamos crear un nuevo proyecto. Usaremos la CLI de Nest.js para generar un nuevo proyecto.

```
$ nest new project-name
```

## 2. Instalar dependencias

A continuación, necesitamos instalar las dependencias para nuestro proyecto. Necesitaremos el controlador MongoDB Node.js y el paquete Nest.js MongoDB.

```
$ npm install mongodb @nestjs/mongoose
```

## 3. Crea un módulo Nest.js

A continuación, necesitamos crear un módulo Nest.js. Este es un módulo JavaScript estándar que contendrá nuestro código para interactuar con MongoDB.

```javascript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [
    MongooseModule.forFeature([
      { name: 'User', schema: UserSchema }
    ])
  ],
  providers: [UserService],
  exports: [UserService]
})
export class UserModule {}
```

## 4. Crea un servicio Nest.js

A continuación, debemos crear un servicio Nest.js. Esta es una clase de JavaScript estándar que contendrá nuestro código para interactuar con MongoDB.

```javascript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class UserService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<User>
  ) {}

  async findAll(): Promise<User[]> {
    return await this.userModel.find().exec();
  }
}
```

## 5. Crear una función de nube de Google

A continuación, necesitamos crear una función de Google Cloud. Esta es una función estándar de JavaScript que se activará cuando alguien realice una solicitud a nuestro punto final de API.

```javascript
import * as functions from 'firebase-functions';
import { NestFactory } from '@nestjs/core';
import { UserModule } from './user.module';

export const userApi = functions.https.onRequest(async (req, res) => {
  const app = await NestFactory.create(UserModule);
  await app.init();
  res.send(await app.get(UserService).findAll());
});
```

## 6. Implementa tu función

Finalmente, necesitamos implementar nuestra función. Podemos hacer esto usando Firebase CLI.

```
$ firebase deploy --only functions
```

## 7. Pruebe su punto final de API

Puede probar su punto final de API realizando una solicitud GET a la URL del punto final. Debería ver una respuesta JSON con una lista de usuarios.

```
$ curl https://us-central1-project-name.cloudfunctions.net/userApi
```

## ¡Felicidades!

Ha creado correctamente un punto final de la API de Nest.js que utiliza Google Cloud Functions.