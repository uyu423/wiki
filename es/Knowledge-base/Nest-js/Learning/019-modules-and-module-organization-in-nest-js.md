---
title: 019: Módulos y organización de módulos en Nest.js
description: 
published: true
date: 2023-02-06T01:17:53.227Z
tags: 
editor: markdown
dateCreated: 2023-02-06T01:17:47.640Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [019: Modules and module organization in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/019-modules-and-module-organization-in-nest-js)
{.links-list}


# Módulos y organización de módulos en Nest.js

Nest.js es un marco de Node.js para crear aplicaciones escalables del lado del servidor. Utiliza JavaScript moderno, está construido con TypeScript (opcional) y combina elementos de programación orientada a objetos, programación funcional y programación reactiva.

Nest.js está fuertemente inspirado en Angular. De hecho, el autor de Nest.js es la misma persona que creó Angular. Nest.js comparte muchos de los mismos conceptos e ideas que Angular, por lo que si está familiarizado con Angular, Nest.js le resultará muy familiar.

Uno de los conceptos clave en Nest.js son los módulos. Los módulos se utilizan para organizar su código y estructurar su aplicación. Nest.js viene con un sistema de módulos incorporado, que se basa en el sistema de módulos CommonJS.

Los módulos son como bibliotecas. Son una forma de empaquetar el código para que pueda reutilizarse en otras partes de su aplicación. Los módulos de Nest.js son muy similares a los módulos de Angular.

Cada módulo de Nest.js es una colección de componentes, directivas, conductos y servicios relacionados. Los módulos pueden importar otros módulos, lo que le brinda una forma de compartir código entre módulos.

Los módulos también pueden exportar componentes, directivas, conductos y servicios para que puedan usarse en otros módulos.

Los módulos de Nest.js son diferentes de los módulos de Node.js. Los módulos de Node.js se utilizan para crear aplicaciones que se ejecutan en Node.js. Los módulos de Nest.js se usan para crear aplicaciones que se ejecutan en Node.js y usan Nest.js.

Los módulos de Node.js generalmente se empaquetan como bibliotecas y se publican en npm. Los módulos de Nest.js generalmente se empaquetan como bibliotecas y también se publican en npm.

## Creando un módulo

Crear un módulo Nest.js es simple. Todo lo que necesita es un directorio con un archivo llamado `module.ts`. El archivo `module.ts` es el punto de entrada para el módulo.

```typescript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

El decorador `@Module` se usa para definir un módulo Nest.js. El decorador `@Module` toma un objeto con algunas propiedades. La propiedad más importante es la propiedad `imports`.

La propiedad `importaciones` es una matriz de otros módulos de los que depende este módulo. Así es como compartes código entre módulos.

```typescript
import { Module } from '@nestjs/common';

@Module({
  imports: [OtherModule],
})
export class MyModule {}
```

La propiedad `importaciones` no es necesaria. Si no necesita compartir código entre módulos, no necesita usar la propiedad `importaciones`.

## Organización del módulo

Las aplicaciones de Nest.js normalmente se organizan en un conjunto de módulos. El módulo principal es el módulo raíz y los otros módulos son módulos secundarios.

El módulo raíz es el módulo que se inicia cuando se inicia la aplicación. Los otros módulos son cargados por el módulo raíz.

Los módulos secundarios pueden ser cargados por otros módulos secundarios. Esto le permite crear una estructura anidada de módulos.

La forma recomendada de organizar los módulos es tener un módulo de función para cada función en su aplicación. Un módulo de características es un módulo que encapsula una característica de su aplicación.

Por ejemplo, si tiene una función de blog, tendría un módulo de función de blog. El módulo de función de blog contendría todo el código para la función de blog.

Los módulos de características normalmente se organizan en una estructura de directorio. Por ejemplo, el módulo de características del blog podría estar organizado en la siguiente estructura de directorios.

```
- blog
  - blog.module.ts
  - blog.service.ts
  - blog.controller.ts
  - blog.component.ts
  - blog.pipe.ts
  - blog.directive.ts
```

El archivo `blog.module.ts` es el archivo del módulo para el módulo de características del blog. Los otros archivos en el directorio son los componentes del módulo.

La forma recomendada de estructurar su aplicación es tener un módulo raíz y un conjunto de módulos de características. Esto le brinda una clara separación de preocupaciones y una estructura clara para su aplicación.

## Resumen

Los módulos son un concepto clave en Nest.js. Los módulos se utilizan para organizar su código y estructurar su aplicación. Nest.js viene con un sistema de módulos incorporado, que se basa en el sistema de módulos CommonJS.

Cada módulo de Nest.js es una colección de componentes, directivas, conductos y servicios relacionados. Los módulos pueden importar otros módulos, lo que le brinda una forma de compartir código entre módulos.

Los módulos también pueden exportar componentes, directivas, conductos y servicios para que puedan usarse en otros módulos.

Los módulos de Nest.js son diferentes de los módulos de Node.js. Los módulos de Node.js se utilizan para crear aplicaciones que se ejecutan en Node.js. Los módulos de Nest.js se usan para crear aplicaciones que se ejecutan en Node.js y usan Nest.js.

Los módulos de Node.js generalmente se empaquetan como bibliotecas y se publican en npm. Los módulos de Nest.js generalmente se empaquetan como bibliotecas y también se publican en npm.

Crear un módulo Nest.js es simple. Todo lo que necesita es un directorio con un archivo llamado `module.ts`. El archivo `module.ts` es el punto de entrada para el módulo.

El decorador `@Module` se usa para definir un módulo Nest.js. El decorador `@Module` toma un objeto con algunas propiedades. La propiedad más importante es la propiedad `imports`.

La propiedad `importaciones` es una matriz de otros módulos de los que depende este módulo. Así es como compartes código entre módulos.

Las aplicaciones de Nest.js normalmente se organizan en un conjunto de módulos. El módulo principal es el módulo raíz y los otros módulos son módulos secundarios.

Los módulos secundarios pueden ser cargados por otros módulos secundarios. Esto le permite crear una estructura anidada de módulos.

La forma recomendada de organizar los módulos es tener un módulo de función para cada función en su aplicación. Un módulo de características es un módulo que encapsula una característica de su aplicación.

Por ejemplo, si tiene una función de blog, tendría un módulo de función de blog. El módulo de función de blog contendría todo el código para la función de blog.