---
title: 007: Creación de servicios en Nest.js
description: 
published: true
date: 2023-02-14T18:32:19.729Z
tags: 
editor: markdown
dateCreated: 2023-02-14T18:32:18.093Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [007: Creating services in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/007-creating-services-in-nest-js)
{.links-list}


# Introducción

En esta publicación, veremos cómo crear servicios en Nest.js. Los servicios son una excelente manera de abstraer la lógica compleja en sus aplicaciones, y Nest.js proporciona una forma muy sencilla de crearlos.

Estaremos cubriendo los siguientes temas:

- ¿Qué es un servicio?
- ¿Cuáles son los beneficios de utilizar los servicios?
- ¿Cómo crear un servicio en Nest.js?
- ¿Cómo inyectar un servicio en un componente Nest.js?
- ¿Cómo usar un servicio en un componente Nest.js?

# ¿Qué es un servicio?

En ingeniería de software, un servicio es una unidad autónoma de funcionalidad a la que pueden acceder otros componentes de una aplicación. Los servicios generalmente se usan para encapsular la lógica comercial y se pueden reutilizar en diferentes partes de una aplicación.

# ¿Cuáles son los beneficios de usar los servicios?

El uso de servicios en sus aplicaciones ofrece muchos beneficios, incluidos los siguientes:

- Los servicios pueden ayudar a mantener su código SECO (No se repita).
- Los servicios pueden hacer que su código sea más modular y más fácil de mantener.
- Los servicios pueden mejorar la capacidad de prueba de su código.
- Los servicios pueden hacer que su código sea más escalable.

# ¿Cómo crear un servicio en Nest.js?

Crear un servicio en Nest.js es muy sencillo. Primero, cree un nuevo archivo en el directorio `src/` y asígnele el nombre `my-service.service.ts`. Luego, agregue el siguiente código al archivo:

```typescript
import { Injectable } from '@nestjs/common';

@Injectable()
export class MyService {
  doSomething(): string {
    return 'Hello, world!';
  }
}
```

Como puede ver, hemos importado el módulo `@nestjs/common`, que proporciona el decorador `@Injectable()`. Luego hemos usado este decorador para marcar nuestra clase `MyService` como inyectable.

# ¿Cómo inyectar un servicio en un componente Nest.js?

Para usar un servicio en un componente Nest.js, debemos inyectarlo en el componente. Inyectar un servicio en un componente es muy simple. Primero, necesitamos importar el decorador `@Inject()` desde el módulo `@nestjs/common`. Luego, podemos usar este decorador para inyectar el servicio en el componente:

```typescript
import { Injectable, Inject } from '@nestjs/common';
import { MyService } from './my-service.service';

@Injectable()
export class MyComponent {
  constructor(
    @Inject(MyService)
    private readonly myService: MyService,
  ) {}
}
```

# ¿Cómo usar un servicio en un componente Nest.js?

Una vez que se ha inyectado un servicio en un componente, se puede utilizar como cualquier otro servicio. En el siguiente ejemplo, utilizaremos el método `doSomething()` de nuestro servicio `MyService`:

```typescript
import { Injectable, Inject } from '@nestjs/common';
import { MyService } from './my-service.service';

@Injectable()
export class MyComponent {
  constructor(
    @Inject(MyService)
    private readonly myService: MyService,
  ) {}

  doSomething(): string {
    return this.myService.doSomething();
  }
}
```

# Conclusión

En esta publicación, hemos visto cómo crear servicios en Nest.js. Los servicios son una excelente manera de abstraer la lógica compleja en sus aplicaciones, y Nest.js proporciona una forma muy sencilla de crearlos.

También hemos analizado cómo inyectar un servicio en un componente de Nest.js y cómo usar un servicio en un componente de Nest.js.

Si desea obtener más información sobre los servicios en Nest.js, le recomendaría consultar los siguientes recursos:

- [Documentación de Nest.js - Servicios](https://docs.nestjs.com/fundamentals/services)
- [Tutorial de Nest.js - Servicios](https://nestjs.com/tutorials/services)
- [Ejemplos de Nest.js - Servicios](https://github.com/nestjs/nest/tree/master/sample/10-services)