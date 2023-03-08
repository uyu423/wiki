---
title: 062: Implementación de cargas y descargas de archivos en Nest.js
description: 
published: true
date: 2023-02-04T00:18:00.719Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:17:59.007Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [062: Implementing file uploads and downloads in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/062-implementing-file-uploads-and-downloads-in-nest-js)
{.links-list}


# 062: Implementación de carga y descarga de archivos en Nest.js

## Introducción

En muchas aplicaciones web, existe la necesidad de permitir que los usuarios carguen y descarguen archivos. Por ejemplo, un usuario puede querer cargar una imagen para usarla como imagen de perfil o descargar un documento PDF generado por la aplicación.

En esta publicación, veremos cómo implementar cargas y descargas de archivos en una aplicación Nest.js. Comenzaremos viendo cómo cargar archivos, luego veremos cómo descargarlos.

## Subiendo archivos

Hay dos formas principales de cargar archivos en Nest.js: usando el módulo `multer` o el método `Nest.js uploadFile`.

### Usando el módulo `multer`

El módulo `multer` es una opción popular para manejar cargas de archivos en aplicaciones Node.js. Es fácil de usar y tiene una amplia gama de funciones.

Para usar `multer`, primero debe instalarlo desde npm:

```
npm install multer
```

Una vez que `multer` está instalado, puede usarlo en su aplicación Nest.js de esta manera:

```javascript
// src/app.controller.ts

import { Controller, Post, UseInterceptors, UploadedFile } from '@nestjs/common';
import { FileInterceptor } from '@nestjs/platform-express';

@Controller()
export class AppController {

  @Post('/upload')
  @UseInterceptors(FileInterceptor('file'))
  uploadFile(@UploadedFile() file) {
    console.log(file);
  }
}
```

En el código anterior, hemos definido un controlador con un punto final `/upload` que acepta cargas de archivos. También agregamos el decorador `@UseInterceptors` para usar el interceptor Nest.js `FileInterceptor`, que se usa para procesar las cargas de archivos.

El interceptor `FileInterceptor` acepta un parámetro `name`, que es el nombre del campo de formulario que contiene el archivo. En nuestro ejemplo, el nombre del campo de formulario es `archivo`.

Finalmente, hemos agregado el decorador `@UploadedFile` al parámetro `file` del método `uploadFile`. Este decorador se utiliza para obtener información sobre el archivo cargado.

Si ejecutamos la aplicación y cargamos un archivo, deberíamos ver el siguiente resultado:

```
{ fieldname: 'file',
  originalname: 'test.txt',
  encoding: '7bit',
  mimetype: 'text/plain',
  buffer: <Buffer 74 65 73 74 0d 0a>,
  size: 9 }
```

Como puede ver, el decorador `@UploadedFile` nos brinda información sobre el archivo cargado, como el nombre original y el tipo MIME.

### Usando el método `Nest.js uploadFile`

Otra opción para cargar archivos en Nest.js es utilizar el método `Nest.js uploadFile`. Este método es parte del paquete `@nestjs/common`, lo que significa que no necesitas instalar ninguna dependencia adicional.

Para usar el método `Nest.js uploadFile`, primero debe crear un método `uploadFile` en su controlador:

```javascript
// src/app.controller.ts

import { Controller, Post, Body, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Post('/upload')
  @HttpCode(HttpStatus.OK)
  uploadFile(@Body() body) {
    console.log(body);
  }
}
```

En el código anterior, hemos definido un controlador con un punto final `/upload` que acepta cargas de archivos. También agregamos el decorador `@HttpCode` para establecer el código de estado HTTP en `200` y el decorador `@Body` para obtener el cuerpo de la solicitud.

A continuación, debemos crear un método ` uploadFile` en nuestro servicio:

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async uploadFile(file: any) {
    const formData = new FormData();
    formData.append('file', file);

    try {
      const response = await this.httpService.post(
        `${this.configService.get('API_URL')}/upload`,
        formData,
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

En el código anterior, hemos inyectado `HttpService` y `ConfigService` en nuestro `AppService`. También hemos creado un método `uploadFile` que acepta un parámetro `file`.

Este método crea un objeto `FormData`, que se utiliza para enviar el archivo al extremo `/upload`. También hemos agregado un bloque try/catch para detectar cualquier error que ocurra.

Finalmente, necesitamos llamar al método `uploadFile` desde nuestro controlador:

```javascript
// src/app.controller.ts

import { Controller, Post, Body, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Post('/upload')
  @HttpCode(HttpStatus.OK)
  uploadFile(@Body() body) {
    this.appService.uploadFile(body);
  }
}
```

En el código anterior, hemos inyectado `AppService` en nuestro controlador. También hemos creado un método `uploadFile` que llama al método `uploadFile` desde nuestro servicio.

Si ejecutamos la aplicación y cargamos un archivo, deberíamos ver el siguiente resultado:

```
{ file:
   { fieldname: 'file',
     originalname: 'test.txt',
     encoding: '7bit',
     mimetype: 'text/plain',
     buffer: <Buffer 74 65 73 74 0d 0a>,
     size: 9 } }
```

Como puede ver, el método `Nest.js uploadFile` nos brinda información sobre el archivo cargado, como el nombre original y el tipo MIME.

## Descargando archivos

Hay dos formas principales de descargar archivos en Nest.js: usando el método `Nest.js downloadFile` o el método `Nest.js sendFile`.

### Usando el método `Nest.js downloadFile`

El método `Nest.js downloadFile` es parte del paquete `@nestjs/common`, lo que significa que no necesita instalar ninguna dependencia adicional.

Para usar el método `DownloadFile` de Nest.js, primero debe crear un método `downloadFile` en su controlador:

```javascript
// src/app.controller.ts

import { Controller, Get, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile() {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.downloadFile(file);
  }
}
```

En el código anterior, hemos definido un controlador con un punto final `/download` que devuelve un archivo. También hemos agregado el decorador `@HttpCode` para establecer el código de estado HTTP en `200`.

A continuación, debemos crear un método `downloadFile` en nuestro servicio:

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async downloadFile(file: string) {
    try {
      const response = await this.httpService.get(
        `${this.configService.get('API_URL')}/download?file=${file}`,
        {
          responseType: 'arraybuffer',
          headers: {
            'Content-Type': 'application/octet-stream',
            'Content-Disposition': `attachment; filename=${file}`,
          },
        },
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

En el código anterior, hemos inyectado `HttpService` y `ConfigService` en nuestro `AppService`. También hemos creado un método `downloadFile` que acepta un parámetro `file`.

Este método realiza una solicitud GET al extremo `/download` con el parámetro de consulta `file`. También hemos agregado un bloque try/catch para detectar cualquier error que ocurra.

Finalmente, necesitamos llamar al método `downloadFile` desde nuestro controlador:

```javascript
// src/app.controller.ts

import { Controller, Get, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile() {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.downloadFile(file);
  }
}
```

En el código anterior, hemos inyectado `AppService` en nuestro controlador. También hemos creado un método `downloadFile` que llama al método `downloadFile` desde nuestro servicio.

Si ejecutamos la aplicación y visitamos el punto final `/download`, deberíamos ver el contenido del archivo `test.txt`.

### Usando el método `Nest.js sendFile`

Otra opción para descargar archivos en Nest.js es usar el método `Nest.js sendFile`. Este método es parte del paquete `@nestjs/common`, lo que significa que no necesitas instalar ninguna dependencia adicional.

Para usar el método `Nest.js sendFile`, primero debe crear un método `sendFile` en su controlador:

```javascript
// src/app.controller.ts

import { Controller, Get, Res, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile(@Res() res) {
    const file = `${__dirname}/../../test.txt`;
    return res.sendFile(file);
  }
}
```

En el código anterior, hemos definido un controlador con un punto final `/download` que devuelve un archivo. También agregamos el decorador `@HttpCode` para establecer el código de estado HTTP en `200` y el decorador `@Res` para obtener el objeto de respuesta.

A continuación, necesitamos crear un método `sendFile` en nuestro servicio:

```javascript
// src/app.service.ts

import { Injectable } from '@nestjs/common';
import { HttpService, HttpStatus, } from '@nestjs/common';
import { ConfigService } from '@nestjs/config';

@Injectable()
export class AppService {
  constructor(
    private readonly httpService: HttpService,
    private readonly configService: ConfigService,
  ) {}

  async sendFile(file: string) {
    try {
      const response = await this.httpService.get(
        `${this.configService.get('API_URL')}/download?file=${file}`,
        {
          responseType: 'arraybuffer',
          headers: {
            'Content-Type': 'application/octet-stream',
            'Content-Disposition': `attachment; filename=${file}`,
          },
        },
      ).toPromise();

      return response.data;
    } catch (error) {
      throw new HttpException('Internal server error', HttpStatus.INTERNAL_SERVER_ERROR);
    }
  }
}
```

En el código anterior, hemos inyectado `HttpService` y `ConfigService` en nuestro `AppService`. También hemos creado un método `sendFile` que acepta un parámetro `file`.

Este método realiza una solicitud GET al extremo `/download` con el parámetro de consulta `file`. También hemos agregado un bloque try/catch para detectar cualquier error que ocurra.

Finalmente, necesitamos llamar al método `sendFile` desde nuestro controlador:

```javascript
// src/app.controller.ts

import { Controller, Get, Res, HttpCode, HttpStatus } from '@nestjs/common';

@Controller()
export class AppController {

  constructor(private readonly appService: AppService) {}

  @Get('/download')
  @HttpCode(HttpStatus.OK)
  downloadFile(@Res() res) {
    const file = `${__dirname}/../../test.txt`;
    return this.appService.sendFile(file);
  }
}
```

En el código anterior, hemos inyectado `AppService` en nuestro controlador. También hemos creado un método `downloadFile` que llama al método `sendFile` desde nuestro servicio.

Si ejecutamos la aplicación y visitamos el punto final `/download`, deberíamos ver el contenido del archivo `test.txt`.

## Conclusión

En esta publicación, hemos visto cómo implementar cargas y descargas de archivos en una aplicación Nest.js.

Hemos analizado dos formas diferentes de cargar archivos: usando el módulo `multer` o el método `Nest.js uploadFile`. También hemos visto dos formas diferentes de descargar archivos: usando el método `Nest.js downloadFile` o el método `Nest.js sendFile`.

El método que elija dependerá de sus necesidades específicas.