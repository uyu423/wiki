---
title: 018: Creación de componentes reutilizables en Nest.js
description: 
published: true
date: 2023-02-07T21:17:22.330Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:17:16.600Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [018: Creating reusable components in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/018-creating-reusable-components-in-nest-js)
{.links-list}


# Creación de componentes reutilizables en Nest.js

Nest.js es un marco para crear aplicaciones Node.js. Utiliza TypeScript y está construido sobre Express.js.

Uno de los beneficios de usar Nest.js es que facilita la creación de componentes reutilizables. En esta publicación, veremos cómo crear un componente reutilizable en Nest.js.

## Definición de un componente

El primer paso para crear un componente reutilizable es definirlo. Podemos hacer esto usando el decorador @Component.

Por ejemplo, supongamos que queremos crear un componente que registre información sobre un usuario. Lo definiríamos así:

```typescript
@Component()
export class UserLoggerComponent {
  // ...
}
```

## Usando un componente

Una vez que hemos definido un componente, podemos usarlo en nuestra aplicación Nest.js inyectándolo en un controlador o servicio.

Por ejemplo, digamos que tenemos un controlador que maneja las solicitudes para crear usuarios. Podemos inyectar nuestro UserLoggerComponent en este controlador y usarlo para registrar información sobre el nuevo usuario:

```typescript
@Controller('users')
export class UserController {
  constructor(private readonly userLogger: UserLoggerComponent) {}

  @Post()
  async createUser(@Body() userDto: UserDto) {
    // ...

    this.userLogger.log(userDto);

    // ...
  }
}
```

## Conclusión

En esta publicación, hemos visto cómo crear componentes reutilizables en Nest.js. Hemos definido un componente usando el decorador @Component y lo hemos inyectado en un controlador para usarlo.