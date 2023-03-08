---
title: Integración de TypeScript con la API de Google Maps para servicios basados en la ubicación
description: 
published: true
date: 2023-02-06T18:55:23.336Z
tags: 
editor: markdown
dateCreated: 2023-02-06T18:55:17.688Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Integrating TypeScript with Google Maps API for Location-Based Services***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-google-maps-api-for-location-based-services)
{.links-list}


# Integración de TypeScript con la API de Google Maps para servicios basados en la ubicación

TypeScript es un superconjunto de JavaScript que permite la verificación de tipos y otros beneficios. Google Maps API es una API popular para servicios de ubicación que permite mapas interactivos y geocodificación. En este artículo, le mostraremos cómo integrar TypeScript con la API de Google Maps para crear servicios basados en la ubicación.

## ¿Qué es TypeScript?

TypeScript es un superconjunto de JavaScript que permite la verificación de tipos y otros beneficios. TypeScript es fácil de usar con el código JavaScript existente y se puede adoptar de forma incremental.

## ¿Qué es la API de Google Maps?

Google Maps API es una API popular para servicios de ubicación que permite mapas interactivos y geocodificación. La API se puede utilizar para crear servicios basados en la ubicación, como mapas, búsqueda y navegación.

## Cómo integrar TypeScript con la API de Google Maps

Para usar la API de Google Maps con TypeScript, deberá crear un archivo de declaración de TypeScript. Un archivo de declaración de TypeScript es un archivo que contiene información de tipo de TypeScript para bibliotecas de JavaScript. El archivo de declaración de la API de Google Maps está disponible en GitHub.

Una vez que haya descargado el archivo de declaración, puede incluirlo en su proyecto de TypeScript con la siguiente línea de código:

```typescript
/// <reference path="google-maps-api.d.ts" />
```

Ahora puede usar la API de Google Maps en su código TypeScript. Por ejemplo, el siguiente código crea un mapa y agrega un marcador al mapa:

```typescript
var map: google.maps.Map;
var marker: google.maps.Marker;

map = new google.maps.Map(document.getElementById('map'), {
  zoom: 8,
  center: {lat: -34.397, lng: 150.644}
});

marker = new google.maps.Marker({
  position: {lat: -34.397, lng: 150.644},
  map: map
});
```

## Recursos

- [Mecanografiado](https://www.typescriptlang.org/)
- [API de Google Maps](https://developers.google.com/maps/documentation/javascript/)
- [Archivos de declaración de TypeScript] (https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)
- [google-maps-api.d.ts](https://github.com/DefinitelyTyped/DefinitelyTyped/blob/master/types/google-maps/index.d.ts)