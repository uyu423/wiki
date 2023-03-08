---
title: 009: Integración con MongoDB en Nest.js
description: 
published: true
date: 2023-02-14T20:32:21.827Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:32:19.966Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [009: Integrating with MongoDB in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/009-integrating-with-mongodb-in-nest-js)
{.links-list}


# Introducción
En esta publicación, veremos cómo integrar MongoDB con Nest.js. Usaremos la biblioteca Mongoose para ayudarnos con esto. Mongoose es una herramienta de modelado de objetos MongoDB diseñada para trabajar en un entorno asíncrono.

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript y está inspirado en Angular.

# Empezando
Primero, necesitamos instalar la biblioteca Mongoose. Podemos hacer esto usando npm:

```
npm install mongoose
```

A continuación, debemos crear un archivo para nuestra conexión Mongoose. Llamaremos a este archivo ```mongoose.ts```:

```typescript
import * as mongoose from 'mongoose';

export const databaseProviders = [
  {
    provide: 'DbConnectionToken',
    useFactory: async () => {
      (mongoose as any).Promise = global.Promise;
      return await mongoose.connect('mongodb://localhost/nest');
    },
  },
];
```

En el archivo, estamos usando la función ```useFactory``` para devolver una promesa que se resuelve en nuestra conexión Mongoose. También estamos configurando la propiedad ```Promise``` global en la propiedad ```Promise``` de Mongoose para que Mongoose use la misma biblioteca de promesas que Nest.js.

# Uso de Mongoose con Nest.js
Ahora que tenemos Mongoose instalado y nuestro archivo de conexión configurado, veamos cómo usar Mongoose con Nest.js.

Primero, necesitamos crear un módulo Nest.js. Llamaremos a este módulo ```MongooseModule```:

```typescript
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';

@Module({
  imports: [MongooseModule.forRoot('mongodb://localhost/nest')],
})
export class MongooseModule {}
```

En el módulo, usamos la función ```forRoot``` para crear una instancia de MongooseModule. Esta función toma una cadena de conexión MongoDB como su único parámetro.

A continuación, debemos crear un servicio Nest.js. Llamaremos a este servicio ```MongoService```:

```typescript
import { Injectable } from '@nestjs/common';
import { InjectModel } from '@nestjs/mongoose';
import { Model } from 'mongoose';

@Injectable()
export class MongoService {
  constructor(
    @InjectModel('User') private readonly userModel: Model<any>,
  ) {}

  async findAll(): Promise<any[]> {
    return await this.userModel.find().exec();
  }
}
```

En el servicio, usamos el decorador ```@InjectModel``` para inyectar un modelo Mongoose en el servicio. También estamos usando la función ```find``` para consultar la base de datos para todos los usuarios.

Finalmente, necesitamos crear un controlador Nest.js. Llamaremos a este controlador ```MongoController```:

```typescript
import { Controller, Get } from '@nestjs/common';
import { MongoService } from './mongo.service';

@Controller('mongo')
export class MongoController {
  constructor(private readonly mongoService: MongoService) {}

  @Get()
  async findAll() {
    return await this.mongoService.findAll();
  }
}
```

En el controlador, usamos el decorador ```@Get``` para crear una ruta que responda a las solicitudes GET. También estamos usando la función ```findAll``` de nuestro MongoService para consultar la base de datos y devolver todos los usuarios.

# Conclusión
En esta publicación, analizamos cómo integrar MongoDB con Nest.js. Instalamos la biblioteca Mongoose y la usamos para crear un módulo, un servicio y un controlador Nest.js.