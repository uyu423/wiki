---
title: 018: Análisis de video con TensorFlow.js y Node.js
description: 
published: true
date: 2023-02-02T11:04:51.596Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:04:49.931Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [018: Video Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/018-video-analysis-with-tensorflow-js-and-node-js)
{.links-list}


## Introducción

En esta publicación, veremos cómo usar TensorFlow.js y Node.js para realizar análisis de video. Usaremos un modelo previamente entrenado para identificar objetos en el video y luego rastrearlos a medida que se mueven.

Usaremos las siguientes herramientas y bibliotecas:

-TensorFlow.js
- Nodo.js
- ffmpeg (opcional)

## ¿Qué es TensorFlow.js?

TensorFlow.js es una biblioteca de JavaScript para entrenar e implementar modelos de aprendizaje automático. Se utiliza tanto para el aprendizaje profundo como para el aprendizaje automático tradicional.

## ¿Qué es Node.js?

Node.js es un tiempo de ejecución de JavaScript que se usa para desarrollar aplicaciones del lado del servidor.

## Configuración del entorno

Antes de comenzar, debemos configurar nuestro entorno. Necesitaremos instalar Node.js y TensorFlow.js.

Si aún no tiene instalado Node.js, puede descargarlo del [sitio web de Node.js] (https://nodejs.org/en/).

Una vez instalado Node.js, podemos instalar TensorFlow.js usando el siguiente comando:

```
npm install @tensorflow/tfjs
```

## Convertir el video a un formato adecuado

Para usar el modelo preentrenado, necesitamos convertir el video a un formato que el modelo pueda entender. El modelo espera que el video esté en formato MPEG-4 con una resolución y velocidad de fotogramas específicas.

Si tiene ffmpeg instalado, puede usar el siguiente comando para convertir el video:

```
ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4
```

Si no tiene ffmpeg instalado, puede descargarlo del [sitio web de ffmpeg] (https://ffmpeg.org/).

## Analizando el video

Ahora que tenemos nuestro entorno configurado y el video convertido, podemos comenzar a analizarlo.

Usaremos un modelo previamente entrenado llamado [YOLOv2](https://pjreddie.com/darknet/yolo/). Este modelo se entrenó en el conjunto de datos [Pascal VOC](http://host.robots.ox.ac.uk/pascal/VOC/) y puede identificar 20 clases diferentes de objetos.

Para usar el modelo, primero debemos cargarlo en TensorFlow.js. Esto lo podemos hacer con el siguiente código:

```javascript
const tf = require('@tensorflow/tfjs');

const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v2_1.0_224/model.json');
```

Una vez que se carga el modelo, podemos comenzar a analizar el video. Tendremos que pasar cada cuadro del video al modelo y recuperar las predicciones.

Para hacer esto, primero necesitaremos obtener una lista de todos los cuadros en el video. Esto lo podemos hacer con el siguiente código:

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

Una vez que tengamos la lista de cuadros, podemos comenzar a analizar el video. Para cada cuadro, necesitaremos pasarlo al modelo y recuperar las predicciones.

Para hacer esto, primero necesitaremos obtener una lista de todos los cuadros en el video. Esto lo podemos hacer con el siguiente código:

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

Una vez que tengamos la lista de cuadros, podemos comenzar a analizar el video. Para cada cuadro, necesitaremos pasarlo al modelo y recuperar las predicciones.

Para hacer esto, primero necesitaremos obtener una lista de todos los cuadros en el video. Esto lo podemos hacer con el siguiente código:

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

Una vez que tengamos la lista de cuadros, podemos comenzar a analizar el video. Para cada cuadro, necesitaremos pasarlo al modelo y recuperar las predicciones.

Para ello, utilizaremos el siguiente código:

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

Este código cargará el video en TensorFlow.js, analizará cada cuadro y luego enviará los resultados a la consola.

## Seguimiento de los objetos

Ahora que tenemos las predicciones para cada cuadro, podemos comenzar a rastrear los objetos. Para hacer esto, usaremos el [filtro Kalman](https://en.wikipedia.org/wiki/Kalman_filter).

El filtro de Kalman es un modelo matemático que puede predecir el estado futuro de un sistema, basado en observaciones pasadas.

Usaremos el filtro de Kalman para predecir la posición futura de cada objeto, en función de sus posiciones pasadas. Esto nos permitirá rastrear los objetos a medida que se mueven en el video.

Para usar el filtro Kalman, primero necesitaremos instalar la biblioteca [kalman-filter](https://www.npmjs.com/package/kalman-filter). Esto lo podemos hacer con el siguiente comando:

```
npm install kalman-filter
```

Una vez que la biblioteca está instalada, podemos usar el siguiente código para rastrear los objetos:

```javascript
const kf = new KalmanFilter();

const trackedObjects = [];

for (const prediction of predictions) {
  const trackedObject = trackedObjects.find(obj => obj.id === prediction.id);

  if (trackedObject) {
    trackedObject.update(prediction);
  } else {
    trackedObjects.push(new TrackedObject(prediction));
  }
}
```

Este código rastreará los objetos en el video y enviará sus posiciones a la consola.

## Visualizando los resultados

Ahora que tenemos las predicciones y los objetos rastreados, podemos comenzar a visualizar los resultados.

Usaremos la biblioteca [PIXI.js](https://www.pixijs.com/) para dibujar un cuadro alrededor de cada objeto.

Primero, necesitamos instalar la biblioteca [pixi.js](https://www.npmjs.com/package/pixi.js). Esto lo podemos hacer con el siguiente comando:

```
npm install pixi.js
```

Una vez que la biblioteca está instalada, podemos usar el siguiente código para dibujar las cajas:

```javascript
const app = new PIXI.Application();

document.body.appendChild(app.view);

const graphics = new PIXI.Graphics();

app.stage.addChild(graphics);

for (const trackedObject of trackedObjects) {
  const { x, y, width, height } = trackedObject;

  graphics.lineStyle(1, 0xffffff);
  graphics.drawRect(x, y, width, height);
}
```

Este código dibujará un cuadro alrededor de cada objeto en el video.

## Conclusión

En esta publicación, hemos visto cómo usar TensorFlow.js y Node.js para realizar análisis de video. Usamos un modelo previamente entrenado para identificar objetos en el video y luego rastrearlos a medida que se mueven.

También hemos visto cómo usar el filtro de Kalman para predecir la posición futura de cada objeto, en función de sus posiciones pasadas. Esto nos permite rastrear los objetos a medida que se mueven en el video.

Finalmente, hemos visto cómo usar la biblioteca PIXI.js para dibujar un cuadro alrededor de cada objeto.