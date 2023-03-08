---
title: 061: Uso de Nest.js con la API del sistema de archivos
description: 
published: true
date: 2023-02-10T10:56:24.848Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:56:18.455Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [061: Using Nest.js with the Filesystem API***English** document is available*](/en/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}


# Uso de Nest.js con la API del sistema de archivos

Nest.js es un marco de Node.js que lo ayuda a crear aplicaciones escalables del lado del servidor. Utiliza TypeScript y se integra bien con el ecosistema Node.js.

En esta publicación, veremos cómo usar Nest.js con la API del sistema de archivos. Usaremos los siguientes módulos:

- [fs](https://nodejs.org/api/fs.html): El módulo del sistema de archivos Node.js.
- [ruta](https://nodejs.org/api/path.html): El módulo de ruta de Node.js.
- [util](https://nodejs.org/api/util.html): El módulo de utilidad de Node.js.

## Leer y escribir archivos

Lo primero que haremos será aprender a leer y escribir archivos. Comenzaremos con un ejemplo simple que lee un archivo e imprime su contenido en la consola.

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    throw err;
  }

  console.log(data);
});
```

En el código anterior, hemos usado el método `fs.readFile()` para leer el contenido de un archivo. El primer argumento es la ruta al archivo y el segundo argumento es la codificación. La función de devolución de llamada toma dos argumentos: un objeto `err` y los `datos` del archivo.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el argumento `data` contendrá el contenido del archivo.

También podemos usar el método `fs.readFileSync()` para leer archivos sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

Ahora veamos cómo escribir archivos. El siguiente ejemplo escribe una cadena en un archivo:

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.writeFile()` para escribir una cadena en un archivo. El primer argumento es la ruta al archivo, el segundo argumento es la cadena a escribir y el tercer argumento es la codificación. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el archivo se escribirá correctamente.

También podemos usar el método `fs.writeFileSync()` para escribir archivos sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Agregar archivos

 A veces necesitamos agregar datos a un archivo existente en lugar de sobrescribirlo. Podemos hacer esto con el método `fs.appendFile()`:

```javascript
const fs = require('fs');

fs.appendFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.appendFile()` para agregar una cadena a un archivo. El primer argumento es la ruta al archivo, el segundo argumento es la cadena para agregar y el tercer argumento es la codificación. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el archivo se escribirá correctamente.

También podemos usar el método `fs.appendFileSync()` para agregar archivos sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Cambio de nombre de archivos

Podemos usar el método `fs.rename()` para cambiar el nombre de los archivos:

```javascript
const fs = require('fs');

fs.rename('old-file.txt', 'new-file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.rename()` para cambiar el nombre de un archivo. El primer argumento es la ruta anterior y el segundo argumento es la ruta nueva. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el archivo se renombrará con éxito.

También podemos usar el método `fs.renameSync()` para renombrar archivos sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Eliminación de archivos

Podemos usar el método `fs.unlink()` para eliminar archivos:

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.unlink()` para eliminar un archivo. El primer argumento es la ruta al archivo. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el archivo se eliminará con éxito.

También podemos usar el método `fs.unlinkSync()` para eliminar archivos sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Archivos de estado

Podemos usar el método `fs.stat()` para obtener información sobre un archivo:

```javascript
const fs = require('fs');

fs.stat('file.txt', (err, stats) => {
  if (err) {
    throw err;
  }

  console.log(stats);
});
```

En el código anterior, hemos usado el método `fs.stat()` para obtener información sobre un archivo. El primer argumento es la ruta al archivo. La función de devolución de llamada toma dos argumentos: un objeto `err` y un objeto `stats`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el objeto `stats` contendrá información sobre el archivo.

También podemos usar el método `fs.statSync()` para obtener información sobre los archivos de forma síncrona. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Ver archivos

Podemos usar el método `fs.watch()` para observar los cambios en un archivo:

```javascript
const fs = require('fs');

fs.watch('file.txt', (eventType, filename) => {
  console.log(eventType, filename);
});
```

En el código anterior, hemos usado el método `fs.watch()` para observar los cambios en un archivo. El primer argumento es la ruta al archivo. La función de devolución de llamada toma dos argumentos: una cadena `eventType` y una cadena `filename`.

El argumento `eventType` será uno de los siguientes:

- `rename`: El archivo ha sido renombrado.
- `cambio`: El archivo ha sido cambiado.

El argumento `filename` será la nueva ruta del archivo si se le cambió el nombre, o `null` si se cambió el archivo.

También podemos usar el método `fs.watchFile()` para observar cambios en un archivo. Sin embargo, este método utiliza sondeos, que pueden ser costosos.

## Lectura de directorios

Podemos usar el método `fs.readdir()` para leer el contenido de un directorio:

```javascript
const fs = require('fs');

fs.readdir('/path/to/directory', (err, files) => {
  if (err) {
    throw err;
  }

  console.log(files);
});
```

En el código anterior, hemos usado el método `fs.readdir()` para leer el contenido de un directorio. El primer argumento es la ruta al directorio. La función de devolución de llamada toma dos argumentos: un objeto `err` y una matriz `files`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, la matriz `archivos` contendrá los nombres de los archivos en el directorio.

También podemos usar el método `fs.readdirSync()` para leer el contenido de un directorio sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Creación de directorios

Podemos usar el método `fs.mkdir()` para crear un directorio:

```javascript
const fs = require('fs');

fs.mkdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.mkdir()` para crear un directorio. El primer argumento es la ruta al directorio. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el directorio se creará correctamente.

También podemos usar el método `fs.mkdirSync()` para crear un directorio sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Eliminación de directorios

Podemos usar el método `fs.rmdir()` para eliminar un directorio:

```javascript
const fs = require('fs');

fs.rmdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

En el código anterior, hemos usado el método `fs.rmdir()` para eliminar un directorio. El primer argumento es la ruta al directorio. La función de devolución de llamada toma un argumento: un objeto `err`.

Si hay un error, se establecerá el objeto `err`. De lo contrario, el directorio se eliminará con éxito.

También podemos usar el método `fs.rmdirSync()` para eliminar un directorio sincrónicamente. Sin embargo, este método bloquea el bucle de eventos, por lo que generalmente no se recomienda.

## Conclusión

En esta publicación, hemos visto cómo usar Nest.js con la API del sistema de archivos. Hemos aprendido cómo leer y escribir archivos, cómo agregar datos a los archivos, cómo cambiar el nombre y eliminar archivos, cómo obtener información sobre los archivos, cómo observar cambios en los archivos, cómo leer el contenido de los directorios, cómo Crear y eliminar directorios.