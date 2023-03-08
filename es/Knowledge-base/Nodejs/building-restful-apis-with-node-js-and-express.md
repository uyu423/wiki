---
title: Creación de API RESTful con Node.js y Express
description: 
published: true
date: 2023-02-07T02:19:10.900Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:19:09.193Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building RESTful APIs with Node.js and Express***English** document is available*](/en/Knowledge-base/Nodejs/building-restful-apis-with-node-js-and-express)
{.links-list}


# Creación de API RESTful con Node.js y Express

Node.js es una plataforma poderosa para crear aplicaciones del lado del servidor. En este artículo, le mostraremos cómo crear una API RESTful con Node.js y Express.

## ¿Qué es una API REST?

Una API REST es una interfaz de programación de aplicaciones que utiliza solicitudes HTTP para OBTENER, PONER, PUBLICAR y ELIMINAR datos. Se puede usar una API REST para acceder a los recursos de un servidor, lo que la convierte en una herramienta perfecta para crear un back-end para su aplicación web o móvil.

## ¿Por qué usar Express?

Express es un marco popular para crear aplicaciones web en Node.js. Es liviano y fácil de usar, lo que lo convierte en una excelente opción para crear API RESTful.

## Creación de una API REST con Node.js y Express

Ahora que sabemos qué es una API REST y por qué usaríamos Express para crear una, ¡comencemos!

Crearemos una API REST simple que permita a los usuarios administrar una lista de tareas pendientes. Nuestra API tendrá los siguientes puntos finales:

- `GET /todos`: Obtener una lista de todas las tareas pendientes
- `POST /todos`: Crea una nueva tarea
- `PUT /todos/:id`: Actualizar una tarea pendiente
- `DELETE /todos/:id`: Eliminar una tarea pendiente

### Configuración de un proyecto Node.js

Comencemos configurando un nuevo proyecto de Node.js. Usaremos el [generador Express](https://expressjs.com/en/starter/generator.html) para crear nuestro proyecto.

Primero, instale el generador Express globalmente:

```
npm install -g express-generator
```

A continuación, cree un nuevo proyecto utilizando el generador Express:

```
express todo-api
```

Esto creará un nuevo directorio llamado `todo-api` con los archivos y directorios básicos que necesita para comenzar.

A continuación, cambie a su nuevo directorio de proyectos e instale las dependencias:

```
cd todo-api
npm install
```

Ahora que las dependencias están instaladas, puede iniciar el servidor de desarrollo:

```
npm start
```

Debería ver el siguiente resultado:

```
> todo-api@0.0.0 start /Users/<user>/<path>/todo-api
> node ./bin/www

```

Ahora puede acceder a la aplicación en http://localhost:3000.

### Definición del modelo de tareas pendientes

Nuestra API almacenará las tareas pendientes en una base de datos. Usaremos [MongoDB](https://www.mongodb.com/) para nuestra base de datos y [Mongoose](https://mongoosejs.com/) para nuestra biblioteca de base de datos.

Primero, instale Mongoose:

```
npm install mongoose --save
```

A continuación, cree un nuevo archivo en `./models/Todo.js` y agregue el siguiente código:

```javascript
const mongoose = require('mongoose');

const todoSchema = new mongoose.Schema({
  name: String,
  completed: Boolean
});

const Todo = mongoose.model('Todo', todoSchema);

module.exports = Todo;
```

Este código define un modelo `Todo` con dos campos: `nombre` y `completado`.

### Conexión a la base de datos

Ahora que hemos definido nuestro modelo, necesitamos conectarnos a la base de datos. Haremos esto en el archivo `./bin/www`.

Abra `./bin/www` y agregue el siguiente código:

```javascript
#!/usr/bin/env node

/**
 * Module dependencies.
 */

const app = require('../app');
const debug = require('debug')('todo-api:server');
const http = require('http');

/**
 * Get port from environment and store in Express.
 */

const port = normalizePort(process.env.PORT || '3000');
app.set('port', port);

/**
 * Create HTTP server.
 */

const server = http.createServer(app);

/**
 * Connect to MongoDB
 */

const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/todo-api');

/**
 * Listen on provided port, on all network interfaces.
 */

server.listen(port);
server.on('error', onError);
server.on('listening', onListening);

/**
 * Normalize a port into a number, string, or false.
 */

function normalizePort(val) {
  const port = parseInt(val, 10);

  if (isNaN(port)) {
    // named pipe
    return val;
  }

  if (port >= 0) {
    // port number
    return port;
  }

  return false;
}

/**
 * Event listener for HTTP server "error" event.
 */

function onError(error) {
  if (error.syscall !== 'listen') {
    throw error;
  }

  const bind = typeof port === 'string'
    ? 'Pipe ' + port
    : 'Port ' + port;

  // handle specific listen errors with friendly messages
  switch (error.code) {
    case 'EACCES':
      console.error(bind + ' requires elevated privileges');
      process.exit(1);
      break;
    case 'EADDRINUSE':
      console.error(bind + ' is already in use');
      process.exit(1);
      break;
    default:
      throw error;
  }
}

/**
 * Event listener for HTTP server "listening" event.
 */

function onListening() {
  const addr = server.address();
  const bind = typeof addr === 'string'
    ? 'pipe ' + addr
    : 'port ' + addr.port;
  debug('Listening on ' + bind);
}
```

Este código hace lo siguiente:

- Se conecta a la base de datos MongoDB usando Mongoose
- Inicia el servidor Express en el puerto especificado

### Definición de las rutas API

Ahora que tenemos nuestro modelo y base de datos configurados, podemos comenzar a definir nuestras rutas API.

Comenzaremos definiendo la ruta `GET /todos`. Esta ruta devolverá una lista de todas las tareas pendientes en la base de datos.

Abra `./routes/index.js` y agregue el siguiente código:

```javascript
const express = require('express');
const router = express.Router();

const Todo = require('../models/Todo');

/* GET home page. */
router.get('/', function(req, res, next) {
  res.render('index', { title: 'Express' });
});

/* GET all todos. */
router.get('/todos', function(req, res, next) {
  Todo.find({}, function(err, todos) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todos);
    }
  });
});

module.exports = router;
```

Este código define una ruta `GET /todos` que utiliza el método `Todo.find()` para obtener todas las tareas pendientes de la base de datos.

Si la consulta tiene éxito, la matriz `todos` se devuelve en la respuesta JSON. Si hay un error, se devuelve un `Error interno del servidor 500` con el mensaje de error.

A continuación, definamos la ruta `POST /todos`. Esta ruta se utilizará para crear nuevas tareas pendientes.

Agrega el siguiente código a `./routes/index.js`:

```javascript
/* POST new todo. */
router.post('/todos', function(req, res, next) {
  const todo = new Todo(req.body);
  todo.save(function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

Este código define una ruta `POST /todos` que crea un nuevo `Todo` a partir del objeto `req.body`. El método `save()` se utiliza para guardar la tarea pendiente en la base de datos.

Si se guarda correctamente, se devuelve la nueva tarea pendiente en la respuesta JSON. Si hay un error, se devuelve un `Error interno del servidor 500` con el mensaje de error.

A continuación, definamos la ruta `PUT /todos/:id`. Esta ruta se utilizará para actualizar las tareas pendientes existentes.

Agrega el siguiente código a `./routes/index.js`:

```javascript
/* PUT update todo. */
router.put('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  const todo = req.body;
  Todo.findByIdAndUpdate(id, todo, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

Este código define una ruta `PUT /todos/:id` que utiliza el método `findByIdAndUpdate()` para actualizar una tarea pendiente con el `id` especificado en la URL. El objeto `todo` se actualiza con los datos de `req.body`.

Si la actualización se realiza correctamente, la tarea pendiente actualizada se devuelve en la respuesta JSON. Si hay un error, se devuelve un `Error interno del servidor 500` con el mensaje de error.

Finalmente, definamos la ruta `DELETE /todos/:id`. Esta ruta se utilizará para eliminar las tareas pendientes existentes.

Agrega el siguiente código a `./routes/index.js`:

```javascript
/* DELETE todo. */
router.delete('/todos/:id', function(req, res, next) {
  const id = req.params.id;
  Todo.findByIdAndRemove(id, function(err, todo) {
    if (err) {
      res.status(500).json({ error: err.message });
    } else {
      res.json(todo);
    }
  });
});
```

Este código define una ruta `DELETE /todos/:id` que utiliza el método `findByIdAndRemove()` para eliminar una tarea pendiente con el `id` especificado en la URL.

Si la eliminación se realiza correctamente, la tarea eliminada se devuelve en la respuesta JSON. Si hay un error, se devuelve un `Error interno del servidor 500` con el mensaje de error.

### Prueba de la API

Ahora que hemos definido nuestras rutas API, ¡vamos a probarlas! Usaremos [Postman](https://www.getpostman.com/) para probar nuestra API.

Primero, inicie el servidor de desarrollo:

```
npm start
```

A continuación, abra Postman y cree una nueva solicitud.

Para la ruta `GET /todos`, usaremos la siguiente configuración:

- Método: OBTENER
- URL: http://localhost:3000/todos

![Obtener Tareas](https://i.imgur.com/wLwvWxH.png)

Para la ruta `POST /todos`, usaremos la siguiente configuración:

- Método: POST
- URL: http://localhost:3000/todos
- Cuerpo:
  - Tipo: JSON (aplicación/json)
  - Crudo:
    ```json
    {
      "name": "Prueba pendiente",
      "completado": falso
    }
    ```

![Crear tarea pendiente](https://i.imgur.com/VkzMxK0.png)

Para la ruta `PUT /todos/:id`, usaremos la siguiente configuración:

- Método: PONER
- URL: http://localhost:3000/todos/{id}
- Cuerpo:
  - Tipo: JSON (aplicación/json)
  - Crudo:
    ```json
    {
      "name": "Actualizado Tareas pendientes",
      "completado": verdadero
    }
    ```

![Actualizar tareas pendientes](https://i.imgur.com/pBKgVnS.png)

Para la ruta `DELETE /todos/:id`, usaremos la siguiente configuración:

- Método: ELIMINAR
- URL: http://localhost:3000/todos/{id}

![Eliminar tareas pendientes](https://i.imgur.com/wEwJWdl.png)

## Terminando

En este artículo, le mostramos cómo crear una API RESTful con Node.js y Express. Hemos definido un modelo `Todo` y hemos creado rutas para las solicitudes `GET`, `POST`, `PUT` y `DELETE`. También probamos nuestra API con Postman.

Ahora que ha visto cómo crear una API REST con Node.js y Express, puede usar este conocimiento para crear sus propias API.

## Recursos

- [¿Qué es una API REST?](https://www.mulesoft.com/resources/api/what-rest-api)
- [Exprés](https://expressjs.com/)
- [Node.js](https://nodejs.org/en/)
- [MongoDB](https://www.mongodb.com/)
- [Mangosta](https://mongoosejs.com/)
- [Cartero](https://www.getpostman.com/)