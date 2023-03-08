---
title: 068: Integración de TensorFlow.js con bases de datos en Node.js
description: 
published: true
date: 2023-02-02T22:43:43.548Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:43:38.872Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [068: Integrating TensorFlow.js with Databases in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/068-integrating-tensorflow-js-with-databases-in-node-js)
{.links-list}


# 068: Integrando TensorFlow.js con Bases de Datos en Node.js

TensorFlow.js es una poderosa herramienta para el aprendizaje automático en JavaScript. En esta publicación, le mostraremos cómo usar TensorFlow.js con bases de datos en Node.js.

## Configuración de su entorno

Antes de comenzar, debemos configurar nuestro entorno. Tendremos que instalar Node.js y la API TensorFlow.js Node.js.

Puede instalar Node.js desde el [sitio web de Node.js](https://nodejs.org/en/).

Una vez que haya instalado Node.js, puede instalar TensorFlow.js Node.js API con el siguiente comando:

```
npm install @tensorflow/tfjs-node
```

## Conexión a una base de datos

Ahora que tenemos nuestro entorno configurado, podemos comenzar a trabajar con bases de datos.

Usaremos el módulo [sqlite3](https://www.npmjs.com/package/sqlite3) Node.js para conectarnos a una base de datos SQLite. SQLite es una base de datos liviana que no requiere un servidor separado.

Primero, necesitamos instalar el módulo sqlite3:

```
npm install sqlite3
```

A continuación, crearemos un archivo llamado `database.js` con los siguientes contenidos:

```javascript
const sqlite3 = require('sqlite3').verbose();

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  db.each('SELECT * FROM items', (err, row) => {
    console.log(row.name + ': ' + row.value);
  });
});

db.close();
```

En este archivo, nos estamos conectando a una base de datos SQLite llamada `database.sqlite3`. Luego estamos creando una tabla llamada `elementos` e insertando algunos datos en ella.

Finalmente, estamos consultando los datos de la base de datos e imprimiéndolos en la consola.

Para ejecutar este archivo, puede usar el siguiente comando:

```
node database.js
```

## Uso de TensorFlow.js con bases de datos

Ahora que hemos visto cómo conectarse a una base de datos, echemos un vistazo a cómo usar TensorFlow.js con bases de datos.

Usaremos el mismo archivo `database.js` de la sección anterior. Solo agregaremos algunas líneas de código para cargar los datos de la base de datos en TensorFlow.js `tf.data.Dataset`.

```javascript
const sqlite3 = require('sqlite3').verbose();
const tf = require('@tensorflow/tfjs-node');

const db = new sqlite3.Database('./database.sqlite3');

db.serialize(() => {
  // create a table
  db.run('CREATE TABLE IF NOT EXISTS items (name, value)');

  // insert some data
  const stmt = db.prepare('INSERT INTO items VALUES (?, ?)');
  for (let i = 0; i < 10; i++) {
    stmt.run(`Item ${i}`, i);
  }
  stmt.finalize();

  // query the data
  const dataset = tf.data.Dataset.fromSqlQuery('SELECT * FROM items', db, (err, row) => {
    return {
      name: row.name,
      value: row.value
    };
  });

  // print the data
  dataset.forEachAsync(item => {
    console.log(item.name + ': ' + item.value);
  });
});

db.close();
```

En este archivo, usamos la función `tf.data.Dataset.fromSqlQuery()` para cargar los datos de la base de datos en `tf.data.Dataset`. Luego estamos imprimiendo los datos en la consola.

Para ejecutar este archivo, puede usar el siguiente comando:

```
node database.js
```

## Resumen

En esta publicación, hemos visto cómo usar TensorFlow.js con bases de datos en Node.js. Hemos visto cómo conectarse a una base de datos y cómo usar TensorFlow.js para cargar datos desde una base de datos.