---
title: 022: Implementando la internacionalización en Nest.js
description: 
published: true
date: 2023-02-15T03:32:43.672Z
tags: 
editor: markdown
dateCreated: 2023-02-15T03:32:36.012Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [022: Implementing internationalization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/022-implementing-internationalization-in-nest-js)
{.links-list}


# Implementando la internacionalización en Nest.js

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza TypeScript, un superconjunto de JavaScript, y combina elementos de programación orientada a objetos, programación funcional y programación reactiva funcional.

En esta publicación, veremos cómo implementar la internacionalización en Nest.js. La internacionalización es el proceso de diseñar y desarrollar un producto, aplicación o sitio web para múltiples mercados. Nest.js proporciona un módulo integrado para i18n que facilita agregar la internacionalización a sus aplicaciones Nest.js.

## Empezando

Antes de comenzar, asegurémonos de tener todo lo que necesitamos. Primero, necesitamos instalar el módulo @nestjs/i18n. Esto lo podemos hacer con el siguiente comando:

```
npm install @nestjs/i18n
```

Una vez instalado el módulo, necesitamos crear un archivo de configuración para i18n. Llamaremos a este archivo i18n.options.ts e irá en el directorio src de nuestro proyecto Nest.js. El archivo debería verse así:

```typescript
import {
  I18nModuleOptions,
  I18nCoreModule,
} from '@nestjs/i18n';

const i18nModuleOptions: I18nModuleOptions = {
  fallbacks: {
    'en-US': 'en',
  },
  defaultLocale: 'en',
  path: __dirname,
};

export { i18nModuleOptions };
```

En este archivo, estamos configurando el módulo i18n para usar el inglés como idioma predeterminado. También le estamos diciendo al módulo que busque archivos de idioma en el directorio src.

## Creando archivos de idioma

Ahora que tenemos configurado nuestro archivo de configuración i18n, necesitamos crear nuestros archivos de idioma. Para este ejemplo, crearemos dos archivos de idioma: uno para inglés y otro para español. Llamaremos a estos archivos en.json y es.json, respectivamente.

El archivo en.json debería verse así:

```json
{
  "hello": "Hello, world!"
}
```

Y el archivo es.json debería verse así:

```json
{
  "hello": "¡Hola, mundo!"
}
```

Estos archivos contienen nuestras traducciones para la tecla "hola". Observe que la estructura de los archivos es la misma, independientemente del idioma. Esto se debe a que el módulo i18n usa el formato de módulo CommonJS.

## Uso de archivos de idioma en nuestra aplicación Nest.js

Ahora que tenemos nuestros archivos de idioma configurados, podemos comenzar a usarlos en nuestra aplicación Nest.js.

Primero, necesitamos importar el I18nModule en nuestro módulo de aplicación. Esto lo podemos hacer con el siguiente código:

```typescript
import { Module } from '@nestjs/common';
import { I18nModule } from '@nestjs/i18n';

@Module({
  imports: [
    I18nModule.forRoot(),
  ],
})
export class ApplicationModule {}
```

A continuación, debemos crear un servicio que se encargue de gestionar nuestras traducciones. Llamaremos a este servicio I18nService. El servicio debería verse así:

```typescript
import { Injectable } from '@nestjs/common';
import { I18nService as I18n } from '@nestjs/i18n';

@Injectable()
export class I18nService {
  constructor(private readonly i18n: I18n) {}

  translate(key: string, params?: any) {
    return this.i18n.translate(key, params);
  }
}
```

En este servicio, inyectamos el I18nService desde el módulo @nestjs/i18n. También estamos creando un método translate() que será responsable de manejar nuestras traducciones.

Ahora que tenemos nuestro servicio configurado, podemos usarlo en nuestros controladores. Para este ejemplo, crearemos un controlador simple que devuelva un saludo en el idioma preferido del usuario. El controlador debería verse así:

```typescript
import { Controller, Get, Res } from '@nestjs/common';
import { Response } from 'express';
import { I18nService } from './i18n.service';

@Controller()
export class AppController {
  constructor(private readonly i18nService: I18nService) {}

  @Get()
  getHello(@Res() res: Response) {
    const message = this.i18nService.translate('hello');
    res.send(message);
  }
}
```

En este controlador, estamos inyectando nuestro I18nService. También estamos creando un método getHello() que devuelve un saludo en el idioma preferido del usuario.

## Probando nuestra aplicación Nest.js

Ahora que tenemos nuestra aplicación Nest.js configurada, probémosla para asegurarnos de que todo funciona como se esperaba. Esto lo podemos hacer con el siguiente comando:

```
npm test
```

Si todo funciona como se esperaba, debería ver el siguiente resultado:

```
> nestjs-i18n@0.0.1 test /Users/username/projects/nestjs-i18n
> jest

 PASS  src/app.controller.spec.ts
  AppController
    GET /
      ✓ should return "Hello, world!" (5ms)

Test Suites: 1 passed, 1 total
Tests:       1 passed, 1 total
Snapshots:   0 total
Time:        1.548s
Ran all test suites.
```

## Conclusión

En esta publicación, analizamos cómo implementar la internacionalización en Nest.js. Hemos creado archivos de idioma y un servicio para manejar nuestras traducciones. También hemos creado un controlador que devuelve un saludo en el idioma preferido del usuario.