---
title: 049: Errores comunes que se deben evitar al usar Nest.js
description: 
published: true
date: 2023-02-02T04:17:39.230Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:17:37.612Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [049: Common pitfalls to avoid when using Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/049-common-pitfalls-to-avoid-when-using-nest-js)
{.links-list}


# 049: errores comunes que se deben evitar al usar Nest.js

Nest.js es un marco poderoso para crear aplicaciones de Node.js. Sin embargo, al igual que con cualquier marco, existen ciertas trampas comunes que pueden hacer tropezar a los desarrolladores que son nuevos en Nest. En esta publicación, veremos algunos de los errores más comunes que se cometen al usar Nest.js y cómo evitarlos.

## 1. No inicializar Nest.js correctamente

Uno de los errores más comunes que se cometen al usar Nest.js es no inicializar el marco correctamente. Nest.js debe inicializarse con el indicador `--init` al crear un nuevo proyecto:

```
nest new my-project --init
```

Si olvida incluir el indicador `--init`, su proyecto no se configurará correctamente y se encontrará con errores.

## 2. No usar el decorador @Module

Otro error que se comete a menudo es olvidarse de usar el decorador `@Module` al crear módulos. Se requiere el decorador `@Module` para todos los módulos Nest.js:

```javascript
import { Module } from '@nestjs/common';

@Module({})
export class MyModule {}
```

Si olvida usar el decorador `@Module`, Nest.js no podrá identificar correctamente su módulo y se encontrará con errores.

## 3. No usar el decorador @Controller

De manera similar, se requiere el decorador `@Controller` para todos los controladores Nest.js:

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

Si olvida usar el decorador `@Controller`, Nest.js no podrá identificar correctamente su controlador y se encontrará con errores.

## 4. No usar el decorador @Injectable

Otro decorador que suele olvidarse es el decorador `@Injectable`. Se requiere el decorador `@Injectable` para todos los servicios de Nest.js:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

Si olvida usar el decorador `@Injectable`, Nest.js no podrá identificar correctamente su servicio y se encontrará con errores.

## 5. No usar el decorador @NestModule

Otro error que se comete a menudo es olvidarse de usar el decorador `@NestModule` al crear módulos. Se requiere el decorador `@NestModule` para todos los módulos Nest.js:

```javascript
import { NestModule } from '@nestjs/common';

@NestModule({})
export class MyModule {}
```

Si olvida usar el decorador `@NestModule`, Nest.js no podrá identificar correctamente su módulo y se encontrará con errores.

## 6. No usar el decorador @NestController

De manera similar, se requiere el decorador `@NestController` para todos los controladores Nest.js:

```javascript
import { NestController } from '@nestjs/common';

@NestController('/my-controller')
export class MyController {}
```

Si olvida usar el decorador `@NestController`, Nest.js no podrá identificar correctamente su controlador y se encontrará con errores.

## 7. No usar el decorador @NestInjectable

Otro decorador que a menudo se olvida es el decorador `@NestInjectable`. Se requiere el decorador `@NestInjectable` para todos los servicios de Nest.js:

```javascript
import { NestInjectable } from '@nestjs/common';

@NestInjectable()
export class MyService {}
```

Si olvida usar el decorador `@NestInjectable`, Nest.js no podrá identificar correctamente su servicio y se encontrará con errores.

## 8. No usar el decorador @Component

Otro error que se comete a menudo es olvidarse de usar el decorador `@Component` al crear módulos. Se requiere el decorador `@Component` para todos los módulos Nest.js:

```javascript
import { Component } from '@nestjs/common';

@Component({})
export class MyModule {}
```

Si olvida usar el decorador `@Component`, Nest.js no podrá identificar correctamente su módulo y se encontrará con errores.

## 9. No usar el decorador @Controller

De manera similar, se requiere el decorador `@Controller` para todos los controladores Nest.js:

```javascript
import { Controller } from '@nestjs/common';

@Controller('/my-controller')
export class MyController {}
```

Si olvida usar el decorador `@Controller`, Nest.js no podrá identificar correctamente su controlador y se encontrará con errores.

## 10. No usar el decorador @Injectable

Otro decorador que suele olvidarse es el decorador `@Injectable`. Se requiere el decorador `@Injectable` para todos los servicios de Nest.js:

```javascript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {}
```

Si olvida usar el decorador `@Injectable`, Nest.js no podrá identificar correctamente su servicio y se encontrará con errores.