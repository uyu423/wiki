---
title: 057: Uso de Nest.js con Service Workers
description: 
published: true
date: 2023-02-15T20:32:42.846Z
tags: 
editor: markdown
dateCreated: 2023-02-15T20:32:35.149Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [057: Using Nest.js with Service Workers***English** document is available*](/en/Knowledge-base/Nest-js/Learning/057-using-nest-js-with-service-workers)
{.links-list}


# Uso de Nest.js con Service Workers

Service Workers es una poderosa herramienta que puede mejorar en gran medida el rendimiento de sus aplicaciones web. Sin embargo, vienen con algunas advertencias que pueden hacer tropezar incluso a los desarrolladores experimentados. En esta publicación, veremos cómo usar Nest.js con Service Workers para evitar algunas de estas trampas.

## ¿Qué es un trabajador de servicio?

Un Service Worker es un script que se ejecuta en segundo plano en su navegador web e intercepta solicitudes de red. Esto les permite hacer cosas como almacenar recursos en caché para uso fuera de línea o servir contenido diferente según las condiciones de la red.

## ¿Qué es Nest.js?

Nest.js es un marco para crear aplicaciones del lado del servidor usando JavaScript. Está construido sobre el marco web Express y utiliza TypeScript para proporcionar seguridad de tipos.

## Uso de Nest.js con Service Workers

Usar Nest.js con Service Workers es un proceso de dos pasos. Primero, debe registrar el script de Service Worker con Nest.js. Esto se puede hacer en el archivo `app.module.ts`:

```typescript
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ServiceWorkerModule } from '@nestjs/service-worker';

@Module({
  imports: [
    ServiceWorkerModule.register('/ngsw-worker.js'),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

El segundo paso es crear el archivo `ngsw-worker.js` en la raíz de su proyecto. Este archivo contiene el código del Service Worker y será atendido por Nest.js.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // This is where you can handle network requests
  // and serve different content based on the network conditions
});
```

Ahora que tiene una comprensión básica de cómo usar Nest.js con Service Workers, echemos un vistazo a algunos de los beneficios que pueden proporcionar.

## Beneficios de los trabajadores de servicios

Service Workers puede proporcionar una serie de beneficios a sus aplicaciones web, incluido el soporte sin conexión, la sincronización de datos en segundo plano y las notificaciones automáticas.

### Soporte fuera de línea

Uno de los casos de uso más comunes para Service Workers es proporcionar soporte fuera de línea para aplicaciones web. Esto se puede lograr almacenando en caché los recursos en el controlador de eventos `fetch` de Service Worker.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

### Sincronización de datos de fondo

Otro caso de uso común para Service Workers es realizar la sincronización de datos en segundo plano. Esto puede ser útil para cosas como actualizar una base de datos local con datos de un servidor remoto.

```javascript
// This is the code for the Service Worker

self.addEventListener('sync', event => {
  // This is where you can perform background data synchronization
});
```

### Notificaciones push

Service Workers también se puede utilizar para enviar notificaciones automáticas a los usuarios. Esto puede ser útil para cosas como alertas o actualizaciones.

```javascript
// This is the code for the Service Worker

self.addEventListener('push', event => {
  // This is where you can send push notifications to users
});
```

## Trampas de los trabajadores de servicios

A pesar de sus muchos beneficios, los Service Workers vienen con algunas advertencias que pueden hacer tropezar incluso a los desarrolladores experimentados.

### Seguridad

Una de las mayores preocupaciones de los Service Workers es la seguridad. Dado que los Service Workers tienen acceso a las solicitudes de red, se pueden utilizar para realizar ataques de intermediarios.

Para mitigar este riesgo, es importante registrar solo trabajadores de servicio de fuentes confiables. En el caso de Nest.js, esto significa solo registrar trabajadores de servicio que son atendidos por Nest.js.

### Almacenamiento en caché

Otro peligro potencial con Service Workers es el almacenamiento en caché. Al usar Service Workers para almacenar recursos en caché, es importante establecer los encabezados de almacenamiento en caché correctos. De lo contrario, es posible que los recursos no se almacenen en caché correctamente o que se almacenen en caché durante demasiado tiempo.

```javascript
// This is the code for the Service Worker

self.addEventListener('fetch', event => {
  // Try to fetch the resource from the network first
  event.respondWith(
    fetch(event.request).then(response => {
      // If the network request succeeds, cache the response
      return caches.open(CACHE_NAME).then(cache => {
        cache.put(event.request, response.clone());
        return response;
      });
    }).catch(() => {
      // If the network request fails, try to get the resource from the cache
      return caches.match(event.request);
    })
  );
});
```

## Conclusión

En esta publicación, analizamos cómo usar Nest.js con Service Workers. También hemos visto algunos de los beneficios que los trabajadores de servicio pueden proporcionar, así como algunos de los peligros que debe tener en cuenta.

Si está interesado en obtener más información sobre Service Workers, le recomiendo consultar los siguientes recursos:

- [Trabajadores de servicios: una introducción](https://developers.google.com/web/fundamentals/primers/service-workers)
- [Uso de trabajadores de servicios] (https://developers.google.com/web/fundamentals/getting-started/primers/service-workers)
- [El ciclo de vida del trabajador del servicio](https://developers.google.com/web/fundamentals/getting-started/primers/service-workers# the_serviceworker_lifecycle)