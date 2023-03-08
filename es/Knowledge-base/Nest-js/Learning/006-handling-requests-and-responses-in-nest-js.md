---
title: 006: Manejo de solicitudes y respuestas en Nest.js
description: 
published: true
date: 2023-02-14T17:32:29.683Z
tags: 
editor: markdown
dateCreated: 2023-02-14T17:32:27.903Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [006: Handling requests and responses in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/006-handling-requests-and-responses-in-nest-js)
{.links-list}


## Introducción

En Nest.js, el manejo de solicitudes y respuestas es un proceso de dos pasos. Primero, debe crear un controlador de solicitudes que reciba la solicitud entrante y la procese. En segundo lugar, debe crear un controlador de respuesta que envíe los datos procesados al cliente.

Crear un controlador de solicitudes es simple. Todo lo que necesita hacer es crear una función que tome una solicitud y un objeto de respuesta, y luego escriba su código dentro de esa función.

```javascript
function requestHandler(req, res) {
  // your code here
}
```

El objeto de solicitud contiene información sobre la solicitud entrante, como la URL, los encabezados y el cuerpo. El objeto de respuesta se utiliza para enviar datos al cliente.

Crear un controlador de respuesta es igual de simple. Todo lo que necesita hacer es crear una función que tome un objeto de datos y un objeto de respuesta, y luego escriba su código dentro de esa función.

```javascript
function responseHandler(data, res) {
  // your code here
}
```

El objeto de datos contiene los datos que desea devolver al cliente. El objeto de respuesta se utiliza para devolver los datos al cliente.

## Enviando una respuesta

Una vez que haya creado sus controladores de solicitud y respuesta, debe decirle a Nest.js cómo enviar la respuesta al cliente. Esto se hace usando la función ```res.send()```.

La función ```res.send()``` toma dos argumentos: los datos a enviar y el código de estado HTTP. El código de estado HTTP es opcional, pero generalmente es una buena idea incluirlo.

Aquí hay un ejemplo de cómo usar la función ```res.send()```:

```javascript
function responseHandler(data, res) {
  res.send(data, 200);
}
```

## Enviar una respuesta JSON

Si desea enviar una respuesta JSON, puede usar la función ```res.json()```. La función ```res.json()``` toma dos argumentos: los datos que se enviarán y el código de estado HTTP.

Aquí hay un ejemplo de cómo usar la función ```res.json()```:

```javascript
function responseHandler(data, res) {
  res.json(data, 200);
}
```

## Enviar una respuesta HTML

Si desea enviar una respuesta HTML, puede utilizar la función ```res.render()```. La función ```res.render()``` toma dos argumentos: la ruta al archivo HTML y un objeto que contiene los datos que se pasarán al archivo HTML.

Aquí hay un ejemplo de cómo usar la función ```res.render()```:

```javascript
function responseHandler(data, res) {
  res.render('index.html', data);
}
```

## Enviar un archivo

Si desea enviar un archivo, puede utilizar la función ```res.sendFile()```. La función ```res.sendFile()``` toma dos argumentos: la ruta al archivo y un objeto que contiene las opciones para enviar el archivo.

Aquí hay un ejemplo de cómo usar la función ```res.sendFile()```:

```javascript
function responseHandler(data, res) {
  res.sendFile('/path/to/file.txt', {
    root: __dirname
  });
}
```

## Enviando una redirección

Si desea enviar una redirección, puede utilizar la función ```res.redirect()```. La función ```res.redirect()``` toma un argumento: la URL a la que se redirigirá.

Aquí hay un ejemplo de cómo usar la función ```res.redirect()```:

```javascript
function responseHandler(data, res) {
  res.redirect('/path/to/new/page');
}
```

## Conclusión

En Nest.js, el manejo de solicitudes y respuestas es un proceso de dos pasos. Primero, debe crear un controlador de solicitudes que reciba la solicitud entrante y la procese. En segundo lugar, debe crear un controlador de respuesta que envíe los datos procesados al cliente.

Crear un controlador de solicitudes es simple. Todo lo que necesita hacer es crear una función que tome una solicitud y un objeto de respuesta, y luego escriba su código dentro de esa función.

Crear un controlador de respuesta es igual de simple. Todo lo que necesita hacer es crear una función que tome un objeto de datos y un objeto de respuesta, y luego escriba su código dentro de esa función.

Una vez que haya creado sus controladores de solicitud y respuesta, debe decirle a Nest.js cómo enviar la respuesta al cliente. Esto se hace usando la función ```res.send()```.

Si desea enviar una respuesta JSON, puede usar la función ```res.json()```. Si desea enviar una respuesta HTML, puede utilizar la función ```res.render()```. Si desea enviar un archivo, puede utilizar la función ```res.sendFile()```. Si desea enviar una redirección, puede utilizar la función ```res.redirect()```.