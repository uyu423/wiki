---
title: Bases de datos Node.js y NoSQL: una guía práctica
description: 
published: true
date: 2023-02-12T19:56:01.380Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:55:59.640Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and NoSQL Databases: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-nosql-databases-a-hands-on-guide)
{.links-list}


# Bases de datos Node.js y NoSQL: una guía práctica

Node.js es un potente tiempo de ejecución de JavaScript basado en el motor V8 de Chrome que se puede utilizar para crear aplicaciones de red escalables. Las bases de datos NoSQL son cada vez más populares por su flexibilidad y escalabilidad, lo que las convierte en una opción natural para usar con Node.js.

En este artículo, adoptaremos un enfoque práctico para trabajar con bases de datos Node.js y NoSQL. Cubriremos los conceptos básicos de cada tecnología y luego crearemos una aplicación CRUD simple que almacena datos en una base de datos MongoDB.

## ¿Qué es Node.js?

Node.js es un entorno de tiempo de ejecución multiplataforma de código abierto para desarrollar aplicaciones del lado del servidor. Las aplicaciones de Node.js están escritas en JavaScript y se pueden ejecutar dentro del tiempo de ejecución de Node.js en OS X, Microsoft Windows y Linux.

 Node.js proporciona una arquitectura basada en eventos y una API de E/S sin bloqueo que lo hace liviano y eficiente. Las aplicaciones de Node.js se pueden ejecutar en un solo subproceso, haciendo uso de un solo núcleo de CPU.

## ¿Qué es NoSQL?

NoSQL es un término utilizado para describir una clase de sistemas de gestión de bases de datos que difieren de las bases de datos relacionales tradicionales en algunos aspectos clave.

Las bases de datos NoSQL a menudo son más escalables que las bases de datos relacionales, ya que están diseñadas para manejar grandes cantidades de datos que pueden distribuirse entre muchos servidores básicos. Las bases de datos NoSQL también suelen ser más flexibles que las bases de datos relacionales, ya que no requieren un esquema rígido.

## Node.js y NoSQL

Las bases de datos Node.js y NoSQL son una combinación natural, ya que ambas están diseñadas para manejar grandes cantidades de datos y son escalables horizontalmente. Además, el esquema flexible de las bases de datos NoSQL significa que los datos se pueden almacenar en un formato que es más natural para los objetos de JavaScript.

Una de las bases de datos NoSQL más populares para usar con Node.js es MongoDB. MongoDB es una base de datos orientada a documentos que almacena datos en documentos similares a JSON.

## Configurando MongoDB

MongoDB se puede descargar desde el sitio web de MongoDB (https://www.mongodb.com/). Una vez que MongoDB está instalado, el paquete mongodb-server debe instalarse desde npm.

```
$ npm install mongodb-server
```

## Crear una base de datos MongoDB

MongoDB almacena datos en colecciones, que son similares a las tablas en una base de datos relacional. Una base de datos puede contener varias colecciones.

Para crear una nueva base de datos, use el cliente MongoDB para conectarse al servidor mongodb y luego use el método createDatabase().

```javascript
var MongoClient = require('mongodb').MongoClient;

MongoClient.connect('mongodb://localhost:27017/mydatabase', function(err, db) {
   if(err) throw err;

   db.createDatabase('mydatabase', function(err, result) {
      if(err) throw err;
      console.log('Database created!');
   });
});
```

## Inserción de datos en una base de datos MongoDB

Los datos se insertan en una base de datos MongoDB usando el método insert(). El método insert() toma un objeto como parámetro y lo inserta en la colección.

El siguiente ejemplo inserta un documento en la colección de "usuarios".

```javascript
db.collection('users').insert({
   name: 'John Doe',
   age: 40
}, function(err, result) {
   if(err) throw err;
   console.log('Document inserted!');
});
```

## Consultando una base de datos MongoDB

Los datos se consultan desde una base de datos MongoDB usando el método find(). El método find() toma un objeto de consulta como parámetro y devuelve todos los documentos que coinciden con la consulta.

El siguiente ejemplo consulta la colección de "usuarios" para todos los documentos con una edad de 40 años.

```javascript
db.collection('users').find({
   age: 40
}).toArray(function(err, docs) {
   if(err) throw err;
   console.log(docs);
});
```

## Actualización de datos en una base de datos MongoDB

Los datos se actualizan en una base de datos MongoDB mediante el método update(). El método update() toma un objeto de consulta y un objeto de actualización como parámetros. El objeto de actualización contiene los campos que deben actualizarse y los nuevos valores.

El siguiente ejemplo actualiza el nombre del usuario con un _id de 1 a "Jane Doe".

```javascript
db.collection('users').update({
   _id: 1
}, {
   $set: {
      name: 'Jane Doe'
   }
}, function(err, result) {
   if(err) throw err;
   console.log('Document updated!');
});
```

## Eliminación de datos de una base de datos MongoDB

Los datos se eliminan de una base de datos MongoDB mediante el método remove(). El método remove() toma un objeto de consulta como parámetro y elimina todos los documentos que coinciden con la consulta.

El siguiente ejemplo elimina el usuario con un _id de 1.

```javascript
db.collection('users').remove({
   _id: 1
}, function(err, result) {
   if(err) throw err;
   console.log('Document deleted!');
});
```

## Construyendo una aplicación CRUD con Node.js y MongoDB

Ahora que cubrimos los conceptos básicos de Node.js y MongoDB, pongamos en práctica lo que aprendimos creando una aplicación CRUD simple.

La aplicación permitirá a los usuarios crear, leer, actualizar y eliminar documentos en una base de datos MongoDB.

### Configuración del proyecto

Cree un nuevo directorio para el proyecto e inicialícelo con npm.

```
$ mkdir nodejs-mongodb-crud
$ cd nodejs-mongodb-crud
$ npm init
```

Instale las siguientes dependencias desde npm.

```
$ npm install express body-parser mongodb
```

### Creando el servidor

Cree un nuevo archivo llamado server.js y agregue el siguiente código.

```javascript
var express = require('express');
var bodyParser = require('body-parser');
var MongoClient = require('mongodb').MongoClient;

var app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

var db;

MongoClient.connect('mongodb://localhost:27017/crud', function(err, database) {
   if(err) throw err;
   db = database;
   app.listen(3000, function() {
      console.log('Listening on port 3000');
   });
});
```

El código anterior crea un servidor Express y configura el middleware del analizador corporal para analizar datos codificados en URL y JSON. También se conecta a la base de datos MongoDB y guarda el objeto de la base de datos en la variable db. Finalmente, inicia el servidor en el puerto 3000.

### Creando las Rutas

Cree un nuevo archivo llamado route.js y agregue el siguiente código.

```javascript
module.exports = function(app, db) {
   app.post('/users', function(req, res) {
      db.collection('users').insert(req.body, function(err, result) {
         if (err) { 
            res.send({ 'error': 'An error has occurred' }); 
         } else {
            res.send(result.ops[0]);
         }
      });
   });
};
```

El código anterior define una ruta POST/usuarios que inserta un documento en la colección "usuarios". El documento se toma del cuerpo de la solicitud. Si la inserción se realiza correctamente, se devuelve el nuevo documento en la respuesta.

Agregue el siguiente código al final del archivo server.js para cargar las rutas.

```javascript
require('./routes')(app, db);
```

### Prueba de la aplicación

Inicie el servidor MongoDB y el servidor Node.js.

```
$ mongod
$ node server.js
```

Pruebe la aplicación enviando una solicitud POST a la ruta /users. Puedes usar curl o Postman para esto.

```
$ curl -X POST -H "Content-Type: application/json" -d '{"name": "John Doe", "age": 40}' http://localhost:3000/users
```

Deberías ver la siguiente respuesta.

```json
{"name": "John Doe", "age": 40, "_id": "58c0eb9e4a6e4a1c9c5e4a82"}
```

También puede consultar la base de datos para ver si se ha insertado el documento.

```
$ mongo
> use crud
> db.users.find()
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
```

### Actualización de las rutas

Actualice el archivo route.js con el siguiente código.

```javascript
app.get('/users', function(req, res) {
   db.collection('users').find().toArray(function(err, docs) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(docs);
      }
   });
});

app.get('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').findOne({ '_id': new ObjectID(id) }, function(err, doc) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(doc);
      }
   });
});

app.put('/users/:id', function(req, res) {
   var id = req.params.id;
   var user = req.body;
   db.collection('users').update({ '_id': new ObjectID(id) }, user, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(user);
      }
   });
});

app.delete('/users/:id', function(req, res) {
   var id = req.params.id;
   db.collection('users').remove({ '_id': new ObjectID(id) }, function(err, result) {
      if (err) { 
         res.send({ 'error': 'An error has occurred' }); 
      } else {
         res.send(req.body);
      }
   });
});
```

El código anterior define las siguientes rutas:

* GET /usuarios: devuelve todos los documentos de la colección "usuarios"
* GET /users/:id - Devuelve el documento con el id especificado
* PUT /users/:id - Actualiza el documento con el id especificado
* DELETE /users/:id - Elimina el documento con el id especificado

### Probando las rutas

Pruebe las rutas enviando las siguientes solicitudes al servidor.

```
$ curl http://localhost:3000/users
$ curl http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X PUT -H "Content-Type: application/json" -d '{"name": "Jane Doe", "age": 30}' http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
$ curl -X DELETE http://localhost:3000/users/58c0eb9e4a6e4a1c9c5e4a82
```

Deberías ver las siguientes respuestas.

```json
[{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}]
{"_id":"58c0eb9e4a6e4a1c9c5e4a82","name":"John Doe","age":40}
{"name": "Jane Doe", "age": 30}
{"name": "Jane Doe", "age": 30}
```

## Conclusión

En este artículo, adoptamos un enfoque práctico para trabajar con bases de datos Node.js y NoSQL. Hemos cubierto los conceptos básicos de cada tecnología y luego creamos una aplicación CRUD simple que almacena datos en una base de datos MongoDB.

Si está interesado en obtener más información sobre las bases de datos Node.js, MongoDB o NoSQL, consulte los siguientes recursos.

* [Node.js](https://nodejs.org/)
* [MongoDB](https://www.mongodb.com/)
* [NoSQL](https://en.wikipedia.org/wiki/NoSQL)