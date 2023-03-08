---
title: 033: Uso de Nest.js con JavaScript
description: 
published: true
date: 2023-02-15T11:32:41.933Z
tags: 
editor: markdown
dateCreated: 2023-02-15T11:32:40.168Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [033: Using Nest.js with JavaScript***English** document is available*](/en/Knowledge-base/Nest-js/Learning/033-using-nest-js-with-javascript)
{.links-list}


# Uso de Nest.js con JavaScript

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza JavaScript moderno, está construido con TypeScript (opcional) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Nest.js es un excelente marco para desarrolladores que tienen experiencia en JavaScript. Es fácil de usar y tiene una sintaxis familiar. En esta publicación, veremos cómo usar Nest.js con JavaScript.

## Instalación

Para instalar Nest.js, deberá tener Node.js y npm instalados en su máquina. Luego puede instalar Nest.js usando el siguiente comando:

```
npm install -g @nestjs/cli
```

## Creación de un proyecto Nest.js

Una vez que se instala Nest.js, puede crear un nuevo proyecto utilizando la CLI de Nest.js. Para hacerlo, ejecute el siguiente comando:

```
nest new project-name
```

Esto creará un nuevo proyecto Nest.js con el nombre que especificó.

## nombre-del-proyecto/src/app.controller.js

El primer archivo que veremos es el archivo app.controller.js. Este es el archivo donde definiremos nuestros controladores. Un controlador es una clase que contiene uno o más métodos. Cada método es responsable de manejar una solicitud.

Echemos un vistazo a un controlador simple:

```javascript
import { Controller, Get, Post, Body } from '@nestjs/common';

@Controller('/api/v1/todos')
export class TodosController {
  @Get()
  findAll() {
    return [];
  }

  @Post()
  create(@Body() createTodoDto) {
    return [];
  }
}
```

En el código anterior, hemos definido un controlador con dos métodos: findAll y create. El método findAll es responsable de manejar las solicitudes GET. El método create es responsable de manejar las solicitudes POST.

## nombre-del-proyecto/src/app.service.js

El siguiente archivo que veremos es el archivo app.service.js. Este es el archivo donde definiremos nuestros servicios. Un servicio es una clase que contiene lógica empresarial.

Echemos un vistazo a un servicio simple:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class TodosService {
  getAll() {
    return [];
  }

  create(createTodoDto) {
    return [];
  }
}
```

En el código anterior, hemos definido un servicio con dos métodos: getAll y create. El método getAll devuelve todos los todos. El método create crea un nuevo todo.

## nombre-del-proyecto/src/app.module.js

El siguiente archivo que veremos es el archivo app.module.js. Este es el archivo donde definiremos nuestros módulos. Un módulo es una clase que contiene controladores y servicios.

Echemos un vistazo a un módulo simple:

```javascript
import { Module } from '@nestjs/common';
import { TodosController } from './app.controller';
import { TodosService } from './app.service';

@Module({
  controllers: [TodosController],
  providers: [TodosService],
})
export class TodosModule {}
```

En el código anterior, hemos definido un módulo con un controlador y un servicio. El controlador es responsable de manejar las solicitudes. El servicio es responsable de la lógica empresarial.

## nombre-del-proyecto/src/main.js

El siguiente archivo que veremos es el archivo main.js. Este es el archivo donde iniciaremos nuestra aplicación Nest.js.

Echemos un vistazo al código:

```javascript
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

En el código anterior, hemos importado NestFactory y AppModule. Luego creamos una nueva aplicación Nest.js y la iniciamos en el puerto 3000.

## Conclusión

En esta publicación, hemos analizado cómo usar Nest.js con JavaScript. Hemos visto cómo instalar Nest.js y crear un nuevo proyecto. También hemos visto cómo definir controladores, servicios y módulos.