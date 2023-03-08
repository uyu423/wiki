---
title: 002: Configuración de un entorno de desarrollo para Nest.js
description: 
published: true
date: 2023-02-14T14:32:30.568Z
tags: 
editor: markdown
dateCreated: 2023-02-14T14:32:28.919Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [002: Setting up a development environment for Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/002-setting-up-a-development-environment-for-nest-js)
{.links-list}


# Configuración de un entorno de desarrollo para Nest.js

Nest.js es un marco para crear aplicaciones del lado del servidor Node.js eficientes y escalables. Utiliza JavaScript moderno, está construido con TypeScript (https://www.typescriptlang.org/) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

## Requisitos previos

Antes de comenzar, asegúrese de tener instalado lo siguiente en su máquina de desarrollo:

* Node.js (https://nodejs.org/en/)
* Mecanografiado (https://www.typescriptlang.org/)
* Un editor de código como Visual Studio Code (https://code.visualstudio.com/)

## Crear un nuevo proyecto Nest.js

Abra una terminal y cree un nuevo proyecto Nest.js ejecutando el siguiente comando:

```
nest new <project name>
```

Esto creará un nuevo directorio con el nombre del proyecto e inicializará el proyecto con una estructura básica de Nest.js.

## Inicie el servidor Nest.js

Navegue hasta el directorio del proyecto recién creado y ejecute el siguiente comando para iniciar el servidor Nest.js:

```
npm run start
```

Esto iniciará el servidor Nest.js en http://localhost:3000 de forma predeterminada. Puede cambiar el número de puerto configurando la variable de entorno `PORT`.

## Crear un nuevo controlador Nest.js

Ahora que el servidor Nest.js está funcionando, creemos un nuevo controlador. En el directorio raíz del proyecto, cree un nuevo directorio llamado `controladores` y un nuevo archivo llamado `<nombre del controlador>.controller.ts` dentro de él.

El archivo del controlador debería verse así:

```typescript
import { Controller } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {}
```

Reemplace `<ruta del controlador>` con la ruta en la que desea que se pueda acceder al controlador y `<Nombre del controlador>` con el nombre del controlador.

## Crear una nueva ruta Nest.js

Dentro del archivo del controlador, cree una nueva ruta agregando lo siguiente:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('<controller path>')
export class <Controller Name>Controller {

  @Get()
  getHello(): string {
    return 'Hello World!';
  }

}
```

El decorador `@Get()` define el método `getHello()` como una ruta GET. También puede definir rutas POST, PUT y DELETE utilizando los decoradores `@Post()`, `@Put()` y `@Delete()` respectivamente.

## Probar la ruta Nest.js

Abra http://localhost:3000/<ruta del controlador> en un navegador web y debería ver el mensaje `Hello World!`.

## Conclusión

En este tutorial, aprendió a configurar un entorno de desarrollo para Nest.js y a crear un nuevo controlador Nest.js con una ruta.