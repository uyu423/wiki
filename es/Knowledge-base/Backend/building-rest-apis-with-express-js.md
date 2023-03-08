---
title: Creación de API REST con Express.js
description: 
published: true
date: 2023-02-06T13:55:51.790Z
tags: 
editor: markdown
dateCreated: 2023-02-06T13:55:50.127Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building REST APIs with Express.js***English** document is available*](/en/Knowledge-base/Backend/building-rest-apis-with-express-js)
{.links-list}


# Creación de API REST con Express.js

Si está buscando crear una API REST con Node.js, probablemente querrá usar el popular marco Express.js. En este artículo, le mostraremos cómo crear una API REST básica con Express.js.

## ¿Qué es una API REST?

Antes de comenzar, primero repasemos brevemente qué es una API REST. REST (Representational State Transfer) es un estilo arquitectónico para crear servicios web. Una API REST define un conjunto de operaciones que se pueden realizar en los recursos, que normalmente se identifican mediante direcciones URL.

Por ejemplo, si tiene un blog, podría tener un recurso `/posts` que represente todas las publicaciones del blog, y cada publicación tendría su propia URL. Para crear una nueva publicación, haría `POST` en el recurso `/posts`. Para ver una publicación específica, tendrías que "OBTENER" la URL de la publicación. Para actualizar una publicación, debe "PONER" en la URL de la publicación, y para eliminar una publicación, debe "ELIMINAR" la URL de la publicación.

Estas son solo algunas de las operaciones más comunes, pero hay muchas más que se pueden realizar en los recursos.

## Configuración de Express.js

Ahora que sabemos qué es una API REST, comencemos a configurar Express.js. Lo primero que deberá hacer es instalar el marco Express.js. Puede hacer esto usando el Administrador de paquetes de nodos (NPM).

```
npm install express
```

Una vez que se instala Express.js, puede crear un nuevo archivo `app.js` y solicitar el módulo Express.js.

```javascript
const express = require('express');
const app = express();
```

A continuación, tendremos que configurar algunas rutas. Las rutas están definidas por el método HTTP y el patrón de URL. Para nuestro ejemplo, crearemos una ruta para `GET`ing todas las publicaciones y una ruta para `POST`ing una nueva publicación.

```javascript
app.get('/posts', (req, res) => {
  // Get all posts
});

app.post('/posts', (req, res) => {
  // Create a new post
});
```

También podemos definir rutas para `PUT`ting y `DELETE`ing publicaciones por su id.

```javascript
app.put('/posts/:id', (req, res) => {
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  // Delete a post
});
```

En las rutas `PUT` y `DELETE`, usamos un parámetro de URL, `:id`, que representa la identificación de la publicación que queremos actualizar o eliminar. Podemos acceder a esta identificación en la función del controlador de ruta usando el objeto `req.params`.

```javascript
app.put('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Update a post
});

app.delete('/posts/:id', (req, res) => {
  const id = req.params.id;
  // Delete a post
});
```

Ahora que tenemos nuestras rutas definidas, necesitamos iniciar el servidor Express.js. Podemos hacer esto llamando al método `app.listen` y pasando el número de puerto. También agregaremos una declaración `console.log` para saber cuándo se está ejecutando el servidor.

```javascript
app.listen(3000, () => {
  console.log('Server is running on port 3000');
});
```

## Probando la API

Ahora que nuestro servidor está en funcionamiento, probemos nuestra API. Podemos usar una herramienta como Postman para realizar solicitudes HTTP a nuestra API.

Primero, vamos a `OBTENER` todas las publicaciones. Deberíamos ver una matriz vacía como respuesta, ya que aún no hemos agregado ninguna publicación.

![obtener todas las publicaciones](https://i.imgur.com/VmYbU7D.png)

A continuación, vamos a `PUBLICAR` una nueva publicación. Tendremos que establecer el encabezado `Content-Type` en `application/json` y pasar un cuerpo JSON con el `título` y el `cuerpo` de la publicación.

![publicar una nueva publicación](https://i.imgur.com/WBY4KdI.png)

Si 'RECIBIMOS' todas las publicaciones de nuevo, deberíamos ver nuestra nueva publicación en la respuesta.

![obtener todas las publicaciones con una nueva publicación](https://i.imgur.com/YB7qAFs.png)

Finalmente, vamos a `PONER` una actualización a nuestra publicación y `DELETE`. Tendremos que configurar el encabezado `Content-Type` en `application/json` nuevamente y pasar el `id` de la publicación en la URL. Para la actualización, simplemente cambiaremos el `título` de la publicación.

![poner actualización en la publicación](https://i.imgur.com/YB7qAFs.png)

Si 'RECIBIMOS' la publicación nuevamente, deberíamos ver el 'título' actualizado.

![obtener publicación con título actualizado](https://i.imgur.com/VmYbU7D.png)

Ahora, vamos a `ELIMINAR` la publicación.

![borrar publicación](https://i.imgur.com/VmYbU7D.png)

Si 'RECIBIMOS' todas las publicaciones de nuevo, deberíamos ver que la publicación ha sido eliminada.

![Obtener todas las publicaciones con la publicación eliminada](https://i.imgur.com/VmYbU7D.png)

¡Y eso es! Ahora ha creado con éxito una API REST básica con Express.js.

## Recursos externos

- [Tutorial API REST](https://www.restapitutorial.com/)
- [Express.js](https://expressjs.com/)
- [Node.js](https://nodejs.org/)