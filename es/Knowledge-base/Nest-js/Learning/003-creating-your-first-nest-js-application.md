---
title: 003: Creando tu primera aplicación Nest.js
description: 
published: true
date: 2023-02-14T15:34:15.386Z
tags: 
editor: markdown
dateCreated: 2023-02-14T15:34:13.201Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [003: Creating your first Nest.js application***English** document is available*](/en/Knowledge-base/Nest-js/Learning/003-creating-your-first-nest-js-application)
{.links-list}


# Creando tu primera aplicación Nest.js

Esta guía lo guiará a través de los pasos para crear su primera aplicación Nest.js. Nest.js es un marco para crear aplicaciones Node.js. Se basa en Express.js y usa TypeScript, que es un superconjunto de JavaScript.

## Requisitos previos

Antes de comenzar, deberá tener instalado lo siguiente en su máquina:

- Nodo.js
- npm
- Mecanografiado

## Empezando

Primero, cree un nuevo directorio para su proyecto. Luego, inicialice su proyecto ejecutando el siguiente comando:

```
npm init
```

Esto creará un archivo `package.json` en el directorio de su proyecto. A continuación, debe instalar el marco Nest.js. Puede hacer esto ejecutando el siguiente comando:

```
npm install --save @nestjs/core
```

## Hola Mundo

Ahora que tiene Nest.js instalado, puede crear su primera aplicación Nest.js. Cree un nuevo archivo llamado `app.ts` en el directorio de su proyecto y agréguele el siguiente código:

```typescript
import { NestFactory } from '@nestjs/core';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);
  await app.listen(3000);
}
bootstrap();
```

Este código importa la clase `NestFactory` del paquete `@nestjs/core` y lo usa para crear una instancia de la clase `AppModule`. La clase `AppModule` es un módulo Nest.js. Los módulos de Nest.js se utilizan para organizar su código.

A continuación, el código llama al método `listen()` en el objeto `app`. Esto le dice a la aplicación Nest.js que comience a escuchar las solicitudes HTTP entrantes en el puerto 3000.

## Conclusión

En esta guía, ha creado su primera aplicación Nest.js. También ha aprendido sobre algunos de los conceptos clave de Nest.js, como los módulos y la clase NestFactory.