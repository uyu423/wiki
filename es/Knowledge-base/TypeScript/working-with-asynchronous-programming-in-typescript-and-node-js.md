---
title: Trabajar con programación asíncrona en TypeScript y Node.js
description: 
published: true
date: 2023-02-16T13:19:33.899Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:19:23.155Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with Asynchronous Programming in TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/working-with-asynchronous-programming-in-typescript-and-node-js)
{.links-list}


# Trabajar con programación asíncrona en TypeScript y Node.js

La programación asíncrona es un paradigma de programación popular que permite una ejecución eficiente del código al evitar el bloqueo de llamadas. En este artículo, veremos cómo trabajar con programación asíncrona en TypeScript y Node.js.

## ¿Qué es la programación asíncrona?

La programación asincrónica es un paradigma de programación que permite la ejecución eficiente de código al evitar el bloqueo de llamadas. Las llamadas de bloqueo son llamadas que esperan una respuesta antes de continuar con la ejecución, lo que puede causar problemas de rendimiento.

Con la programación asíncrona, un programa puede continuar ejecutando otro código mientras espera una respuesta de una llamada de bloqueo. Esto permite una ejecución de código más eficiente, ya que el programa no espera una respuesta sin hacer nada.

## Programación asíncrona en TypeScript

TypeScript es un superconjunto escrito de JavaScript que se compila en un código JavaScript simple y limpio. Ofrece clases, módulos e interfaces para ayudarlo a crear componentes sólidos.

TypeScript está diseñado para el desarrollo de aplicaciones grandes y transcompilaciones a JavaScript. La programación asíncrona es un paradigma de programación popular en TypeScript, ya que permite una ejecución eficiente del código al evitar el bloqueo de llamadas.

Hay dos formas de trabajar con programación asíncrona en TypeScript: Promises y async/await.

### Promesas

Las promesas son una forma de trabajar con código asíncrono en TypeScript. Una promesa representa una operación que aún no se ha completado, pero se espera que lo haga en el futuro.

Las promesas se usan para manejar operaciones asincrónicas en TypeScript. Una promesa puede estar en uno de tres estados:

- **Pendiente**: La operación aún no se ha completado.
- **Cumplido**: La operación se completó con éxito.
- **Rechazado**: La operación ha fallado.

Se puede crear una promesa usando el constructor `Promise`:

```typescript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

El constructor `Promise` toma una función de devolución de llamada con dos parámetros: `resolve` y `reject`. Se llama a la función `resolve` cuando la operación asincrónica se completa con éxito. La función `rechazar` se llama cuando falla la operación asincrónica.

Una vez que se crea una promesa, puede usar el método `then()` para registrar una función de devolución de llamada que se llamará cuando se cumpla la promesa:

```typescript
promise.then((result) => {
  // do something with the result
});
```

También puede usar el método `catch()` para registrar una función de devolución de llamada que se llamará cuando se rechace la promesa:

```typescript
promise.catch((error) => {
  // do something with the error
});
```

Aquí hay un ejemplo del uso de una promesa para cargar una imagen desde una URL:

```typescript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

En este ejemplo, creamos una `Promesa` que se resuelve con la URL de la imagen cuando la imagen se ha cargado, o se rechaza con un error si la imagen no se carga.

### Asíncrono/Espera

Async/await es una forma de trabajar con código asíncrono en TypeScript. Le permite escribir código asíncrono que se ve y se siente como código síncrono.

Async/await se basa en promesas y utiliza las palabras clave `async` y `await`.

La palabra clave `async` se usa para crear una función asíncrona. Una función asíncrona es una función que devuelve una promesa:

```typescript
async function loadImage(url: string): Promise<string> {
  // do something async
}
```

La palabra clave `await` se usa para esperar a que se resuelva una promesa. Solo se puede usar dentro de una función `async`:

```typescript
async function loadImage(url: string): Promise<string> {
  const image = await loadImage(url);
  // do something with the image
}
```

En este ejemplo, usamos la palabra clave `async` para crear una función asíncrona. Usamos la palabra clave `await` para esperar a que se resuelva la función `loadImage`.

Async/await es una forma popular de trabajar con código asíncrono en TypeScript, ya que le permite escribir código asíncrono que se ve y se siente como código síncrono.

## Programación asíncrona en Node.js

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome. Utiliza un modelo de E/S sin bloqueo y controlado por eventos que lo hace liviano y eficiente.

Node.js está diseñado para crear aplicaciones de red escalables. La programación asincrónica es un paradigma de programación popular en Node.js, ya que permite una ejecución eficiente del código al evitar el bloqueo de llamadas.

Hay dos formas de trabajar con programación asincrónica en Node.js: devoluciones de llamada y promesas.

### Devoluciones de llamadas

Las devoluciones de llamada son una forma de trabajar con código asíncrono en Node.js. Una devolución de llamada es una función que se llama cuando se completa una operación asincrónica.

Cuando se inicia una operación asíncrona, se proporciona una función de devolución de llamada. La función de devolución de llamada se llama cuando se completa la operación asincrónica.

Las funciones de devolución de llamada se usan comúnmente en Node.js para operaciones asincrónicas como la E/S de archivos.

Aquí hay un ejemplo del uso de una función de devolución de llamada para leer un archivo:

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

En este ejemplo, usamos la función `fs.readFile` para leer un archivo. La función `fs.readFile` toma una ruta a un archivo y una función de devolución de llamada. La función de devolución de llamada se llama con los parámetros `err` y `data`. Si el parámetro `err` no es `null`, entonces ocurrió un error. De lo contrario, el parámetro `data` contiene los datos del archivo.

### Promesas

Las promesas son una forma de trabajar con código asíncrono en Node.js. Una promesa representa una operación que aún no se ha completado, pero se espera que lo haga en el futuro.

Las promesas se usan para manejar operaciones asincrónicas en Node.js. Una promesa puede estar en uno de tres estados:

- **Pendiente**: La operación aún no se ha completado.
- **Cumplido**: La operación se completó con éxito.
- **Rechazado**: La operación ha fallado.

Se puede crear una promesa usando el constructor `Promise`:

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

El constructor `Promise` toma una función de devolución de llamada con dos parámetros: `resolve` y `reject`. Se llama a la función `resolve` cuando la operación asincrónica se completa con éxito. La función `rechazar` se llama cuando falla la operación asincrónica.

Una vez que se crea una promesa, puede usar el método `then()` para registrar una función de devolución de llamada que se llamará cuando se cumpla la promesa:

```javascript
promise.then((result) => {
  // do something with the result
});
```

También puede usar el método `catch()` para registrar una función de devolución de llamada que se llamará cuando se rechace la promesa:

```javascript
promise.catch((error) => {
  // do something with the error
});
```

Aquí hay un ejemplo del uso de una promesa para cargar una imagen desde una URL:

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

En este ejemplo, creamos una `Promesa` que se resuelve con la URL de la imagen cuando la imagen se ha cargado, o se rechaza con un error si la imagen no se carga.

## Programación asíncrona en Node.js

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 de Chrome. Utiliza un modelo de E/S sin bloqueo y controlado por eventos que lo hace liviano y eficiente.

Node.js está diseñado para crear aplicaciones de red escalables. La programación asincrónica es un paradigma de programación popular en Node.js, ya que permite una ejecución eficiente del código al evitar el bloqueo de llamadas.

Hay dos formas de trabajar con programación asincrónica en Node.js: devoluciones de llamada y promesas.

### Devoluciones de llamada

Las devoluciones de llamada son una forma de trabajar con código asíncrono en Node.js. Una devolución de llamada es una función que se llama cuando se completa una operación asincrónica.

Cuando se inicia una operación asíncrona, se proporciona una función de devolución de llamada. La función de devolución de llamada se llama cuando se completa la operación asincrónica.

Las funciones de devolución de llamada se usan comúnmente en Node.js para operaciones asincrónicas como la E/S de archivos.

Aquí hay un ejemplo del uso de una función de devolución de llamada para leer un archivo:

```javascript
const fs = require('fs');

fs.readFile('/path/to/file', (err, data) => {
  if (err) {
    // do something with the error
  } else {
    // do something with the data
  }
});
```

En este ejemplo, usamos la función `fs.readFile` para leer un archivo. La función `fs.readFile` toma una ruta a un archivo y una función de devolución de llamada. La función de devolución de llamada se llama con los parámetros `err` y `data`. Si el parámetro `err` no es `null`, entonces ocurrió un error. De lo contrario, el parámetro `data` contiene los datos del archivo.

### Promesas

Las promesas son una forma de trabajar con código asíncrono en Node.js. Una promesa representa una operación que aún no se ha completado, pero se espera que lo haga en el futuro.

Las promesas se usan para manejar operaciones asincrónicas en Node.js. Una promesa puede estar en uno de tres estados:

- **Pendiente**: La operación aún no se ha completado.
- **Cumplido**: La operación se completó con éxito.
- **Rechazado**: La operación ha fallado.

Se puede crear una promesa usando el constructor `Promise`:

```javascript
const promise = new Promise((resolve, reject) => {
  // do something async
});
```

El constructor `Promise` toma una función de devolución de llamada con dos parámetros: `resolve` y `reject`. Se llama a la función `resolve` cuando la operación asincrónica se completa con éxito. La función `rechazar` se llama cuando falla la operación asincrónica.

Una vez que se crea una promesa, puede usar el método `then()` para registrar una función de devolución de llamada que se llamará cuando se cumpla la promesa:

```javascript
promise.then((result) => {
  // do something with the result
});
```

También puede usar el método `catch()` para registrar una función de devolución de llamada que se llamará cuando se rechace la promesa:

```javascript
promise.catch((error) => {
  // do something with the error
});
```

Aquí hay un ejemplo del uso de una promesa para cargar una imagen desde una URL:

```javascript
const loadImage = (url: string): Promise<string> => {
  return new Promise((resolve, reject) => {
    const image = new Image();

    image.onload = () => resolve(url);
    image.onerror = () => reject(new Error(`Failed to load image from URL: ${url}`));

    image.src = url;
  });
};
```

En este ejemplo, creamos una `Promesa` que se resuelve con la URL de la imagen cuando la imagen se ha cargado, o se rechaza con un error si la imagen no se carga.

## Recursos externos

- [Funciones asíncronas - TypeScript](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html# async-functions)
- [Funciones de devolución de llamada en Node.js](https://nodejs.org/en/knowledge/javascript-conventions/callbacks/)
- [Usar promesas en Node.js](https://nodejs.org/en/knowledge/javascript-conventions/using-promises-in-nodejs/)