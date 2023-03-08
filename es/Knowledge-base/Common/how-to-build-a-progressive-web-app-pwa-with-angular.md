---
title: Cómo construir una aplicación web progresiva (PWA) con Angular
description: 
published: true
date: 2023-02-06T07:55:34.119Z
tags: 
editor: markdown
dateCreated: 2023-02-06T07:55:32.541Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Build a Progressive Web App (PWA) with Angular***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-progressive-web-app-pwa-with-angular)
{.links-list}


# Cómo construir una aplicación web progresiva (PWA) con Angular

## ¿Qué es una PWA?

Una aplicación web progresiva (PWA) es una aplicación web que utiliza tecnologías web modernas para ofrecer a los usuarios una experiencia similar a la de una aplicación. Los PWA responden y son rápidos, y se pueden instalar en la pantalla de inicio del usuario.

## ¿Por qué construir una PWA?

Los PWA ofrecen muchos beneficios sobre las aplicaciones web tradicionales, incluido un rendimiento mejorado, capacidad fuera de línea y características similares a las de una aplicación.

## Cómo construir una PWA con Angular

Angular es un marco popular para construir PWA. En este artículo, le mostraremos cómo crear una PWA con Angular.

### 1. Crea un nuevo proyecto Angular

Primero, deberá crear un nuevo proyecto Angular. Puede hacer esto usando la CLI de Angular.

Ejecute el siguiente comando para crear un nuevo proyecto Angular:

```
ng new my-pwa
```

Esto creará una nueva carpeta llamada `my-pwa` con su proyecto Angular.

### 2. Agregar características de PWA

A continuación, deberá agregar funciones de PWA a su proyecto Angular. Puede hacer esto usando el paquete @angular/pwa.

Primero, instale el paquete @angular/pwa:

```
npm install @angular/pwa --save
```

A continuación, agregue el manifiesto de PWA a su archivo `index.html`:

```html
<link rel="manifest" href="/manifest.json">
```

Finalmente, genere un archivo de trabajador de servicio:

```
ng generate service-worker
```

Esto creará un archivo llamado `ngsw-worker.js` en su carpeta `src/`.

### 3. Prueba tu PWA

Ahora que ha agregado funciones de PWA a su proyecto Angular, puede probar su PWA.

Para probar su PWA, deberá ejecutar un servidor local. La CLI de Angular incluye un servidor de desarrollo, por lo que puede usarlo.

Ejecute el siguiente comando para iniciar el servidor de desarrollo:

```
ng serve
```

Ahora, abra su navegador y vaya a http://localhost:4200/. Debería ver su aplicación Angular ejecutándose.

Para probar las funciones de PWA, deberá instalar la extensión [Lighthouse](https://developers.google.com/web/tools/lighthouse/) para Chrome.

Una vez que haya instalado Lighthouse, abra la extensión y haga clic en el botón "Generar informe".

Lighthouse analizará su aplicación y proporcionará un informe. El informe le dirá si su aplicación pasa la lista de verificación de PWA.

Si su aplicación no pasa la lista de verificación, intente agregar más funciones de PWA. Por ejemplo, puede agregar [notificaciones automáticas] (https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/) o [sincronización de fondo] (https://developers.google. com/web/fundamentals/getting-started/primers/background-sync).

## Conclusión

En este artículo, le mostramos cómo crear una aplicación web progresiva con Angular. Los PWA ofrecen muchos beneficios sobre las aplicaciones web tradicionales, incluido un rendimiento mejorado, capacidad fuera de línea y características similares a las de una aplicación. Con Angular, es fácil agregar funciones de PWA a su aplicación web.