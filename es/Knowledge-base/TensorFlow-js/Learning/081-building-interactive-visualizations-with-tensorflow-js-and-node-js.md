---
title: 081: Creación de visualizaciones interactivas con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-03T01:44:02.579Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:44:00.873Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [081: Building Interactive Visualizations with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/081-building-interactive-visualizations-with-tensorflow-js-and-node-js)
{.links-list}


# 081: Creación de visualizaciones interactivas con TensorFlow.js y Node.js

En esta publicación, veremos cómo crear visualizaciones interactivas con TensorFlow.js y Node.js.

TensorFlow.js es una potente biblioteca de JavaScript para el cálculo numérico que permite el aprendizaje automático en el navegador. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

Juntas, estas dos tecnologías se pueden usar para crear visualizaciones interactivas que se pueden usar para explorar y analizar datos.

## Empezando

Para comenzar, deberá instalar Node.js y TensorFlow.js.

Node.js se puede descargar e instalar desde el sitio web oficial: https://nodejs.org/en/

TensorFlow.js se puede instalar usando el administrador de paquetes de Node.js:

```
npm install @tensorflow/tfjs
```

## Hola Mundo

Una vez que haya instalado Node.js y TensorFlow.js, puede crear un programa simple "Hello World" usando el siguiente código:

```javascript
// Load the TensorFlow.js library
const tf = require('@tensorflow/tfjs');

// Define a TensorFlow.js graph
tf.tensor([1, 2, 3, 4]).print();
```

Guarde el código anterior en un archivo llamado "hello.js" y ejecútelo usando el tiempo de ejecución de Node.js:

```
node hello.js
```

Debería ver el siguiente resultado:

```
Tensor
    [[1, 2, 3, 4]]
```

 ¡Felicidades! Acabas de ejecutar tu primer programa TensorFlow.js.

## Creación de una visualización interactiva

Ahora que hemos visto cómo comenzar con TensorFlow.js y Node.js, veamos cómo usar estas tecnologías para crear una visualización interactiva.

Usaremos las siguientes bibliotecas para construir nuestra visualización:

- TensorFlow.js: para computación numérica y aprendizaje automático
- Node.js: para ejecutar código JavaScript fuera del navegador
- Express: para crear un servidor web
- Socket.IO: para la comunicación en tiempo real entre el servidor web y el navegador

Nuestra visualización será un gráfico de líneas simple que se actualiza en tiempo real.

### Definición de los datos

Primero, definamos los datos que estaremos visualizando. Usaremos un gráfico de TensorFlow.js para generar puntos de datos aleatorios.

```javascript
// Define a TensorFlow.js graph that generates random data
const data = tf.tensor(new Array(100).fill(0).map(() => Math.random()));
```

El código anterior define un gráfico de TensorFlow.js que genera 100 puntos de datos aleatorios.

### Creación del servidor web

A continuación, creemos un servidor web usando Node.js y Express.

```javascript
// Load the Express.js library
const express = require('express');

// Create an Express.js app
const app = express();

// Define the port that the app will listen on
const port = 3000;

// Start the Express.js app
app.listen(port, () => console.log(`Example app listening on port ${port}!`));
```

El código anterior crea una aplicación Express.js que escucha en el puerto 3000.

### Sirviendo la página HTML

Ahora que tenemos nuestro servidor web en funcionamiento, sirvamos una página HTML que se usará para mostrar nuestra visualización.

```javascript
// Serve the HTML page
app.get('/', (req, res) => res.sendFile(__dirname + '/index.html'));
```

El código anterior define una ruta que sirve a la página HTML cuando se accede a la URL raíz.

La página HTML debe tener los siguientes contenidos:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>081: Building Interactive Visualizations with TensorFlow.js and Node.js</title>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.13.0/dist/tf.min.js"></script>
    <script src="https://cdn.socket.io/socket.io-1.4.5.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/2.7.3/Chart.min.js"></script>
  </head>
  <body>
    <canvas id="chart"></canvas>
    <script>
      // Your code here
    </script>
  </body>
</html>
```

La página HTML incluye las siguientes bibliotecas:

- TensorFlow.js: para computación numérica y aprendizaje automático
- Socket.IO: para la comunicación en tiempo real entre el servidor web y el navegador
- Chart.js: para la creación de tablas y gráficos

La página HTML también incluye un elemento ```<canvas>``` que se usará para mostrar el gráfico de líneas.

### Envío de datos al navegador

Ahora que tenemos nuestro servidor web en funcionamiento y estamos sirviendo la página HTML, enviemos los datos al navegador.

Usaremos Socket.IO para establecer una conexión en tiempo real entre el servidor web y el navegador.

```javascript
// Load the Socket.IO library
const io = require('socket.io')(server);

// Send the data to the browser
io.on('connection', socket => {
  setInterval(() => {
    socket.emit('data', data.toArray());
  }, 1000);
});
```

El código anterior usa Socket.IO para enviar los datos al navegador cada segundo.

### Recibir los datos en el navegador

Ahora que estamos recibiendo los datos en el navegador, visualicémoslos usando Chart.js.

```javascript
// Connect to the socket.io server
const socket = io('http://localhost:3000');

// Receive the data from the server
socket.on('data', data => {
  // Visualize the data using Chart.js
  const chart = new Chart(document.getElementById('chart'), {
    type: 'line',
    data: {
      labels: data.map((_, i) => i),
      datasets: [{
        label: 'Random Data',
        data: data,
        borderColor: '#ff0000',
        fill: false
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false
    }
  });
});
```

El código anterior usa Chart.js para visualizar los datos como un gráfico de líneas. El gráfico se actualiza en tiempo real a medida que se reciben nuevos puntos de datos.

## Conclusión

En esta publicación, hemos visto cómo crear visualizaciones interactivas con TensorFlow.js y Node.js.

TensorFlow.js es una potente biblioteca de JavaScript para el cálculo numérico que permite el aprendizaje automático en el navegador. Node.js es un tiempo de ejecución de JavaScript que le permite ejecutar código JavaScript fuera del navegador.

Juntas, estas dos tecnologías se pueden usar para crear visualizaciones interactivas que se pueden usar para explorar y analizar datos.