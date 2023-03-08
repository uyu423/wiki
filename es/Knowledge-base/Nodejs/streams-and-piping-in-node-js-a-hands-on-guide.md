---
title: Secuencias y tuberías en Node.js: una guía práctica
description: 
published: true
date: 2023-02-01T20:36:28.638Z
tags: 
editor: markdown
dateCreated: 2023-02-01T20:36:26.895Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Streams and Piping in Node.js: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/streams-and-piping-in-node-js-a-hands-on-guide)
{.links-list}


# Flujos y tuberías en Node.js: una guía práctica

Si es un desarrollador de Node.js, es probable que haya usado secuencias en su código. Los flujos son una parte fundamental de Node.js y se utilizan para una variedad de tareas, incluido el manejo de solicitudes y respuestas HTTP, lectura y escritura de archivos, y más.

En este artículo, adoptaremos un enfoque práctico para aprender sobre flujos y tuberías en Node.js. Cubriremos los siguientes temas:

- ¿Qué son los arroyos?
- Tipos de flujo
- Creación de flujos
- Chorros de tubería
-Manejo de errores

## ¿Qué son las corrientes?

Una secuencia es una abstracción para trabajar con datos que se pueden leer o escribir. Los flujos son una parte clave de Node.js y se utilizan para una variedad de tareas, incluido el manejo de solicitudes y respuestas HTTP, lectura y escritura de archivos, y más.

Los flujos se pueden considerar como una canalización de datos, donde los datos fluyen a través del flujo desde un origen hasta un destino. Los flujos se pueden usar para leer datos de un origen, escribir datos en un destino o ambos.

## Tipos de transmisión

Hay cuatro tipos de flujos: de lectura, de escritura, dúplex y de transformación.

- Los flujos legibles se utilizan para leer datos de una fuente.
- Los flujos de escritura se utilizan para escribir datos en un destino.
- Los flujos dúplex se utilizan tanto para leer como para escribir datos.
- Los flujos de transformación se utilizan para transformar datos a medida que fluyen a través del flujo.

## Creando flujos

Hay algunas formas diferentes de crear flujos en Node.js.

Una forma es usar el módulo de transmisión incorporado:

```javascript
const stream = require('stream');

const readableStream = new stream.Readable();
const writableStream = new stream.Writable();
const duplexStream = new stream.Duplex();
const transformStream = new stream.Transform();
```

Otra forma es usar el módulo integrado `fs`:

```javascript
const fs = require('fs');

const readableStream = fs.createReadStream('/path/to/file');
const writableStream = fs.createWriteStream('/path/to/file');
```

## Chorros de tubería

La canalización es una forma de conectar flujos entre sí para que los datos fluyan de un flujo a otro.

Por ejemplo, podría canalizar un flujo legible en un flujo escribible:

```javascript
readableStream.pipe(writableStream);
```

Las tuberías se pueden usar para encadenar múltiples flujos juntos. Por ejemplo, podría canalizar un flujo legible en un flujo de transformación, que transforma los datos, y luego canalizar el flujo de transformación en un flujo de escritura:

```javascript
readableStream.pipe(transformStream).pipe(writableStream);
```

## Manejo de errores

Es importante controlar los errores cuando se trabaja con secuencias. Los errores pueden ocurrir por una variedad de razones, como que una secuencia se cierre inesperadamente o que los datos estén dañados.

Hay algunas formas diferentes de manejar los errores cuando se trabaja con secuencias.

Una forma es escuchar el evento `'error'` en una secuencia:

```javascript
stream.on('error', (err) => {
  // handle the error
});
```

Otra forma es usar el método `.pipe()` con una función de devolución de llamada:

```javascript
stream.pipe(destination, (err) => {
  // handle the error
});
```

Finalmente, puedes usar el método `.catch()` con una Promesa:

```javascript
stream.catch((err) => {
  // handle the error
});
```

## Conclusión

En este artículo, adoptamos un enfoque práctico para aprender sobre flujos y tuberías en Node.js. Hemos cubierto los siguientes temas:

- ¿Qué son los arroyos?
- Tipos de flujo
- Creación de flujos
- Chorros de tubería
- Manejo de errores