---
title: 024: Creación y consumo de API REST en Nest.js
description: 
published: true
date: 2023-02-09T06:55:56.607Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:55:54.963Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [024: Creating and consuming REST APIs in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/024-creating-and-consuming-rest-apis-in-nest-js)
{.links-list}


# Introducción

Nest.js es un marco de Node.js para crear aplicaciones del lado del servidor. Se basa en Express.js y usa TypeScript.

El marco proporciona un conjunto de herramientas y bibliotecas para crear y consumir API REST.

En esta publicación, aprenderemos cómo crear y consumir API REST en Nest.js.

# Creación de API REST en Nest.js

Nest.js proporciona un conjunto de anotaciones y decoradores para crear API REST.

## API basadas en anotaciones

Las anotaciones de Nest.js se basan en los decoradores de la biblioteca de metadatos de reflexión.

Para usar anotaciones, necesitamos instalar la biblioteca reflect-metadata:

```
npm install reflect-metadata --save
```

Luego podemos usar las anotaciones @Controller y @Get para crear una API REST simple:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

La anotación @Controller define la ruta del controlador. La anotación @Get define el método y la ruta del controlador.

En el ejemplo anterior, se podrá acceder al controlador en ```/api/hello```.

También podemos usar las anotaciones @Post, @Put, @Delete y @Patch para crear API REST para crear, actualizar y eliminar recursos.

## API basadas en Decorator

Nest.js también proporciona un conjunto de decoradores para crear API REST.

Para usar decoradores, necesitamos instalar la biblioteca @nestjs/common:

```
npm install @nestjs/common --save
```

Luego podemos usar los decoradores @Controller y @Get para crear una API REST simple:

```typescript
import { Controller, Get } from '@nestjs/common';

@Controller('/api')
export class MyController {
  @Get('/hello')
  public hello(): string {
    return 'Hello World!';
  }
}
```

El decorador @Controller define la ruta del controlador. El decorador @Get define el método y la ruta del controlador.

En el ejemplo anterior, se podrá acceder al controlador en ```/api/hello```.

También podemos usar los decoradores @Post, @Put, @Delete y @Patch para crear API REST para crear, actualizar y eliminar recursos.

# Consumo de API REST en Nest.js

Nest.js proporciona un conjunto de bibliotecas para consumir API REST.

## Cliente HTTP

Nest.js incluye un cliente HTTP integrado basado en la API XMLHttpRequest.

Para usar el cliente HTTP, necesitamos instalar la biblioteca @nestjs/common:

```
npm install @nestjs/common --save
```

Luego podemos inyectar el cliente HTTP en nuestro controlador y usarlo para realizar solicitudes HTTP:

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import { HttpClient } from '@nestjs/common';

@Controller('/api')
export class MyController {
  constructor(private readonly httpClient: HttpClient) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.httpClient.get('https://example.com/api/hello');
    return response.data;
  }
}
```

En el ejemplo anterior, inyectamos el cliente HTTP en nuestro controlador y lo usamos para realizar una solicitud GET a https://example.com/api/hello.

También podemos usar el cliente HTTP para realizar solicitudes POST, PUT, PATCH y DELETE.

## Axios

Nest.js también es compatible con el cliente HTTP de Axios.

Para usar Axios, necesitamos instalar las bibliotecas axios y @nestjs/common:

```
npm install axios @nestjs/common --save
```

Luego podemos inyectar el cliente HTTP de Axios en nuestro controlador y usarlo para realizar solicitudes HTTP:

```typescript
import { Controller, Get, Inject } from '@nestjs/common';
import axios from 'axios';

@Controller('/api')
export class MyController {
  constructor(@Inject('AxiosInstance') private readonly axiosInstance: typeof axios) {}

  @Get('/hello')
  public async hello(): Promise<string> {
    const response = await this.axiosInstance.get('https://example.com/api/hello');
    return response.data;
  }
}
```

En el ejemplo anterior, inyectamos el cliente HTTP de Axios en nuestro controlador y lo usamos para realizar una solicitud GET a https://example.com/api/hello.

También podemos usar el cliente HTTP de Axios para realizar solicitudes POST, PUT, PATCH y DELETE.

# Conclusión

En esta publicación, aprendimos cómo crear y consumir API REST en Nest.js.