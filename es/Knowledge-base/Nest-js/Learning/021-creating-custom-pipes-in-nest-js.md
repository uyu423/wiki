---
title: 021: Creación de tuberías personalizadas en Nest.js
description: 
published: true
date: 2023-02-15T02:32:18.900Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:32:17.104Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [021: Creating custom pipes in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}


# Creación de tuberías personalizadas en Nest.js

Las tuberías son una excelente manera de transformar datos en Nest.js. En esta publicación, aprenderemos cómo crear tuberías personalizadas.

## ¿Qué son las tuberías?

Las tuberías son una característica de Nest.js que permite transformar los datos a medida que fluyen a través de la aplicación. Por ejemplo, se podría usar una canalización para convertir una cadena a mayúsculas o para dar formato a una fecha.

Las tuberías se pueden usar en muchos lugares diferentes en Nest.js, que incluyen:

- En controladores, para transformar datos antes de que se usen en una ruta
- En servicios, para transformar datos antes de que se conserven en una base de datos
- En tuberías, para transformar los datos antes de devolverlos al cliente

## Cómo crear una tubería personalizada

Crear una tubería personalizada es simple. Primero, necesitamos crear un nuevo archivo en el directorio `pipes`. El nombre del archivo debe terminar en `.pipe.ts`.

A continuación, necesitamos importar la interfaz `PipeTransform` desde `@nestjs/common`:

```typescript
import { PipeTransform } from '@nestjs/common';
```

La interfaz `PipeTransform` define un único método, `transform`. Este método se utiliza para transformar los datos. El método acepta dos argumentos:

- `valor`: Los datos a transformar. Esto puede ser cualquier tipo de datos.
- `metadata`: metadatos sobre el valor. Este es un objeto con las siguientes propiedades:
  - `tipo`: El tipo de datos del valor. Esto es útil para garantizar que los datos sean del tipo correcto.
  - `data`: Cualquier otro dato que esté asociado con el valor. Esto es útil para proporcionar contexto a la transformación.

El método `transform` debería devolver los datos transformados.

Veamos un ejemplo. Supongamos que tenemos una lista de cadenas y queremos convertirlas a mayúsculas. Podríamos hacer esto con la siguiente tubería:

```typescript
import { PipeTransform } from '@nestjs/common';

export class StringToUppercasePipe implements PipeTransform {
  transform(value: string, metadata: PipeTransformMetadata) {
    return value.toUpperCase();
  }
}
```

## Cómo usar una tubería personalizada

Una vez que hayamos creado una tubería personalizada, podemos usarla en nuestra aplicación decorando el controlador o el método de servicio con el decorador `@UsePipes`:

```typescript
import { Controller, Get, UsePipes } from '@nestjs/common';
import { StringToUppercasePipe } from './string-to-uppercase.pipe';

@Controller('/')
export class AppController {
  @Get('/')
  @UsePipes(StringToUppercasePipe)
  getHello(): string {
    return 'Hello, world!';
  }
}
```

En el ejemplo anterior, el decorador `@UsePipes` se usa para aplicar `StringToUppercasePipe` al método `getHello`. Esto significa que cualquier cadena devuelta por el método se convertirá a mayúsculas.

## Resumen

En esta publicación, aprendimos cómo crear tuberías personalizadas en Nest.js. Las tuberías son una excelente manera de transformar los datos a medida que fluyen a través de la aplicación.