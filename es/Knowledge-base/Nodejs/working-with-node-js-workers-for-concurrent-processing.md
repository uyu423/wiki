---
title: Trabajar con trabajadores de Node.js para el procesamiento concurrente
description: 
published: true
date: 2023-02-05T06:17:28.584Z
tags: 
editor: markdown
dateCreated: 2023-02-05T06:17:23.247Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with Node.js Workers for Concurrent Processing***English** document is available*](/en/Knowledge-base/Nodejs/working-with-node-js-workers-for-concurrent-processing)
{.links-list}


# Trabajar con trabajadores de Node.js para el procesamiento concurrente

En este artículo, analizaremos cómo trabajar con los trabajadores de Node.js para el procesamiento simultáneo.

El procesamiento concurrente es una forma de paralelismo en el que múltiples unidades de procesamiento trabajan en diferentes partes de una tarea al mismo tiempo. En la programación de computadoras, esto a menudo se logra dividiendo una tarea en subtareas más pequeñas que se pueden ejecutar en paralelo.

Node.js es un tiempo de ejecución de JavaScript basado en el motor de JavaScript V8 que permite el procesamiento simultáneo. Los trabajadores de Node.js son procesos separados que pueden ejecutarse independientemente del proceso principal de Node.js. Estos trabajadores se pueden utilizar para realizar tareas que requieren un uso intensivo de la CPU, como el procesamiento de imágenes o el cifrado de datos.

Hay dos formas de crear un trabajador en Node.js:

- Usa el método `child_process.fork()` para crear un nuevo proceso.
- Utilice el módulo `cluster` para crear un trabajador.

El método `child_process.fork()` es la forma recomendada de crear trabajadores. Este método le permite pasar datos entre los procesos padre e hijo, y también proporciona un método `send()` para enviar mensajes entre procesos.

El módulo `cluster` es un módulo integrado que le permite crear trabajadores. El módulo de clúster es útil si necesita crear una gran cantidad de trabajadores.

## Creando un trabajador

Empecemos por crear un trabajador usando el método `child_process.fork()`.

```javascript
const {fork} = require('child_process');

const worker = fork('worker.js');
```

El código anterior crea un nuevo proceso llamando al método `fork()`. El método `fork()` toma una ruta al archivo JavaScript que se ejecutará en el nuevo proceso. En este caso, estamos pasando la ruta al archivo `worker.js`.

El archivo `worker.js` contiene el siguiente código:

```javascript
console.log('Worker started');

process.on('message', (message) => {
  console.log(`Message from parent: ${message}`);
});

process.send('Hello from the child!');
```

El código anterior configura un oyente para el evento `message`. Este evento se emite cuando el proceso principal envía un mensaje al proceso secundario. El oyente registra el mensaje en la consola.

El proceso hijo también envía un mensaje al proceso padre usando el método `send()`.

## Enviando mensajes

Ahora que hemos visto cómo crear un trabajador y enviar mensajes entre los procesos principal y secundario, echemos un vistazo a cómo enviar mensajes del proceso principal al secundario.

```javascript
worker.send('Hello from the parent!');
```

El código anterior envía un mensaje del proceso principal al secundario. El mensaje será recibido por el detector de eventos `message` que creamos en el archivo `worker.js`.

## Manejo de errores

Es importante manejar los errores cuando se trabaja con trabajadores. De lo contrario, los errores pasarán desapercibidos y podrían provocar un comportamiento inesperado.

Para manejar errores en el proceso secundario, puede usar el evento `error`:

```javascript
worker.on('error', (err) => {
  console.error(err);
});
```

El código anterior configura un detector de eventos de "error" en el proceso secundario. Este evento se emite cuando hay un error en el proceso hijo. El oyente registra el error en la consola.

## Despedir a un trabajador

Puedes despedir a un trabajador usando el método `kill()`:

```javascript
worker.kill();
```

El código anterior finaliza el proceso de trabajo.

## Resumen

En este artículo, hemos visto cómo trabajar con los trabajadores de Node.js para el procesamiento simultáneo. También hemos visto cómo crear un trabajador, enviar mensajes entre los procesos principal y secundario y manejar errores.