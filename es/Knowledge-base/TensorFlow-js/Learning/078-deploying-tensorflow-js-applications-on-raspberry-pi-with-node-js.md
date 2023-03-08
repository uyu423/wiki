---
title: 078: Implementación de aplicaciones TensorFlow.js en Raspberry Pi con Node.js
description: 
published: true
date: 2023-02-03T01:04:40.492Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:04:38.864Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [078: Deploying TensorFlow.js Applications on Raspberry Pi with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/078-deploying-tensorflow-js-applications-on-raspberry-pi-with-node-js)
{.links-list}


## Introducción

Raspberry Pi es una computadora del tamaño de una tarjeta de crédito que se puede usar para varios proyectos electrónicos. Tiene una amplia gama de aplicaciones y se puede utilizar en diversos campos, como la educación, la industria y la investigación.

Una de las aplicaciones más populares de Raspberry Pi es su uso como dispositivo de borde para el aprendizaje automático. TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático.

En esta publicación, lo guiaremos a través del proceso de configuración de una Raspberry Pi para TensorFlow.js. También le mostraremos cómo implementar una aplicación TensorFlow.js en Raspberry Pi.

## Configuración de Raspberry Pi

Lo primero que debe hacer es configurar su Raspberry Pi. Puede seguir las instrucciones en este enlace: https://www.raspberrypi.org/documentation/setup/

Una vez que su Raspberry Pi esté configurada, debe instalar Node.js en ella. Node.js es un tiempo de ejecución de JavaScript que se requiere para ejecutar aplicaciones TensorFlow.js.

Puede instalar Node.js en Raspberry Pi siguiendo las instrucciones de este enlace: https://nodejs.org/en/download/package-manager/# installing-node-js-via-package-manager

## Implementación de aplicaciones TensorFlow.js

Una vez que haya instalado Node.js, ahora puede implementar aplicaciones TensorFlow.js en su Raspberry Pi.

Hay dos formas de implementar aplicaciones TensorFlow.js:

1. Use un servidor web para servir la aplicación.
2. Utilice una herramienta de línea de comandos para implementar la aplicación.

### Uso de un servidor web

El primer método es usar un servidor web para servir la aplicación. Usaremos el servidor web Node.js, Express.js.

Express.js es un marco de aplicación web para Node.js. Se utiliza para crear aplicaciones web y API.

Puede instalar Express.js ejecutando el siguiente comando:

```
npm install express --save
```

Una vez que Express.js está instalado, puede crear un archivo llamado `app.js` y agregarle el siguiente código:

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello world!');
});

app.listen(3000, () => console.log('Example app listening on port 3000!'));
```

Este código crea un servidor web que responde a las solicitudes HTTP con la cadena `¡Hola mundo!`.

Puede iniciar el servidor web ejecutando el siguiente comando:

```
node app.js
```

Ahora puede acceder al servidor web en http://localhost:3000.

### Uso de una herramienta de línea de comandos

El segundo método consiste en utilizar una herramienta de línea de comandos para implementar la aplicación. Usaremos la CLI de TensorFlow.js.

La CLI de TensorFlow.js es una herramienta de línea de comandos que se puede usar para entrenar, implementar y trabajar con modelos de TensorFlow.js.

Puede instalar la CLI de TensorFlow.js ejecutando el siguiente comando:

```
npm install -g @tensorflow/tfjs-node
```

Una vez que la CLI de TensorFlow.js está instalada, puede usarla para implementar una aplicación de TensorFlow.js.

Supongamos que tiene una aplicación TensorFlow.js en el directorio `app`. Puede implementar la aplicación ejecutando el siguiente comando:

```
tfjs deploy --dir app
```

Esto iniciará un servidor web que sirve a la aplicación TensorFlow.js. Puede acceder a la aplicación en http://localhost:3000.

## Conclusión

En esta publicación, le mostramos cómo implementar aplicaciones TensorFlow.js en Raspberry Pi. También le mostramos cómo usar un servidor web para servir la aplicación.