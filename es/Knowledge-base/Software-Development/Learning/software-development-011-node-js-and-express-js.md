---
title: Desarrollo de software 011: Node.js y Express.js
description: 
published: true
date: 2023-02-16T11:55:36.491Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:55:34.913Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 011: Node.js and Express.js***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-011-node-js-and-express-js)
{.links-list}


# Desarrollo de Software 011: Node.js y Express.js

En esta publicación, veremos Node.js y Express.js, dos herramientas populares utilizadas para el desarrollo de software.

Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera de un navegador. Esto lo hace ideal para desarrollar aplicaciones del lado del servidor.

Express.js es un marco de aplicación web para Node.js. Proporciona un conjunto de herramientas para construir aplicaciones web.

## Nodo.js

Node.js es un entorno de tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera de un navegador. Esto lo hace ideal para desarrollar aplicaciones del lado del servidor.

Node.js se basa en el motor JavaScript V8, que se utiliza en Google Chrome. Node.js también tiene un gran ecosistema de bibliotecas de código abierto que se pueden usar para diversas tareas.

### Instalación de Node.js

Instalar Node.js es un proceso simple. Puede descargar el instalador de Node.js desde el [sitio web de Node.js] (https://nodejs.org/en/).

Una vez descargado el instalador, ejecútelo y siga las instrucciones. Node.js se instalará en su computadora.

### Ejecutando Node.js

Una vez que se haya instalado Node.js, puede ejecutar código JavaScript utilizando el tiempo de ejecución de Node.js.

Para ejecutar un archivo JavaScript, use el siguiente comando:

```
node {filename}
```

Por ejemplo, para ejecutar un archivo llamado `hello.js`, usaría el siguiente comando:

```
node hello.js
```

Node.js ejecutará el código en el archivo `hello.js` e imprimirá los resultados en la consola.

## Express.js

Express.js es un marco de aplicación web para Node.js. Proporciona un conjunto de herramientas para construir aplicaciones web.

Express.js es una opción popular para crear aplicaciones web. Es fácil de usar y tiene una gran comunidad de usuarios.

### Hola Mundo

Vamos a crear un simple "¡Hola, mundo!" aplicación usando Express.js.

Cree un archivo llamado `hello.js` y agregue el siguiente código:

```javascript
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, World!');
});

app.listen(3000, () => {
  console.log('Hello, World! app is listening on port 3000');
});
```

Este código crea una aplicación Express.js que responde a las solicitudes HTTP `GET` con un "¡Hola, mundo!" mensaje.

El método `app.listen()` inicia la aplicación Express.js en el puerto 3000.

Para ejecutar la aplicación, use el siguiente comando:

```
node hello.js
```

Ahora puede acceder a la aplicación en http://localhost:3000.

## Conclusión

En esta publicación, analizamos Node.js y Express.js. Hemos visto cómo instalar Node.js y ejecutar código JavaScript usando el tiempo de ejecución de Node.js. También hemos visto cómo crear una aplicación web simple usando Express.js.