---
title: 080: Integrando TensorFlow.js con AR/VR en Node.js
description: 
published: true
date: 2023-02-03T01:36:51.251Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:36:49.569Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [080: Integrating TensorFlow.js with AR/VR in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}


# 080: Integrando TensorFlow.js con AR/VR en Node.js

TensorFlow.js es una poderosa herramienta que nos permite crear modelos de aprendizaje automático y ejecutarlos en el navegador. Esto lo hace ideal para crear aplicaciones que puedan aprovechar la potencia de procesamiento del dispositivo del usuario, sin necesidad de un servidor potente.

En esta publicación, exploraremos cómo usar TensorFlow.js para crear una aplicación simple de realidad aumentada (AR). Usaremos la biblioteca Three.js para representar objetos 3D en el navegador y la biblioteca AR.js para rastrear la cabeza del usuario y mostrar los objetos 3D en la posición correcta.

## Configuración del proyecto

Comenzaremos configurando un nuevo proyecto de Node.js. Cree un nuevo directorio para el proyecto y ejecute `npm init` para crear un archivo `package.json`.

Necesitaremos algunas bibliotecas para este proyecto. Instale las siguientes bibliotecas con el comando `npm`:

* `tensorflow`
* `@tensorflow/tfjs-nodo`
* `tres`
* `ar.js`

## Creando el modelo

Ahora podemos crear el modelo de aprendizaje automático que usaremos para generar los objetos 3D. Usaremos un modelo de regresión lineal simple para este ejemplo.

Cree un nuevo archivo llamado `model.js` e importe la biblioteca `@tensorflow/tfjs-node`.

```javascript
const tf = require('@tensorflow/tfjs-node');
```

A continuación, definiremos algunas constantes que usaremos para entrenar el modelo. La constante `LEARNING_RATE` define qué tan rápido debe aprender el modelo. La constante `BATCH_SIZE` define cuántos puntos de datos usar al entrenar el modelo. La constante `EPOCHS` define cuántas veces el modelo debe pasar por los datos de entrenamiento.

```javascript
const LEARNING_RATE = 0.01;
const BATCH_SIZE = 10;
const EPOCHS = 10;
```

Ahora podemos definir el modelo. Usaremos un modelo 'secuencial' y agregaremos una capa 'densa'. La capa "densa" es una capa completamente conectada que multiplica los datos de entrada por un conjunto de pesos y agrega un término de sesgo.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

Necesitamos compilar el modelo antes de poder entrenarlo. Usaremos el optimizador `sgd`, que es un optimizador de descenso de gradiente simple. También especificaremos la función `pérdida` que el modelo debe minimizar y las `métricas` que queremos rastrear. En este caso, rastrearemos `meanSquaredError` y `meanAbsoluteError`.

```javascript
model.compile({
  optimizer: tf.train.sgd(LEARNING_RATE),
  loss: 'meanSquaredError',
  metrics: ['meanSquaredError', 'meanAbsoluteError']
});
```

## Entrenando al modelo

Ahora que hemos definido el modelo, necesitamos entrenarlo con algunos datos. Usaremos un conjunto de datos simple para este ejemplo, que consta de 10 puntos.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7, 9, 11, 13, 15], [10, 1]);
```

Ahora podemos entrenar el modelo. Especificaremos el `batchSize`, el número de `epochs` y `shuffle` los datos antes de cada época. También especificaremos un conjunto `validationData`, que el modelo usará para evaluar la pérdida y las métricas después de cada época.

```javascript
model.fit(xs, ys, {
  batchSize: BATCH_SIZE,
  epochs: EPOCHS,
  shuffle: true,
  validationData: [xs, ys]
}).then(() => {
  // The model is trained!
});
```

## Guardando el modelo

Una vez que el modelo está entrenado, debemos guardarlo para poder usarlo en el navegador. Podemos usar la función `tf.node.save` para guardar el modelo en un archivo `.pb`.

```javascript
tf.node.save(model, './model.pb');
```

## Cargando el modelo

Ahora que hemos guardado el modelo, podemos cargarlo en el navegador. Usaremos la función `tf.loadFrozenModel` para cargar el modelo. Esta función toma un `modelUrl` y un `weightsManifestUrl`. `modelUrl` es la ruta al archivo `.pb` que guardamos en el paso anterior. `weightsManifestUrl` es la ruta a un archivo JSON que contiene información sobre los pesos del modelo.

```javascript
const modelUrl = './model.pb';
const weightsManifestUrl = './weights_manifest.json';

tf.loadFrozenModel(modelUrl, weightsManifestUrl).then(model => {
  // The model is loaded!
});
```

## Generación de objetos 3D

Ahora que hemos cargado el modelo, podemos usarlo para generar objetos 3D. Usaremos la función `tf.tensor` para crear un tensor a partir de una matriz de números. Este tensor se utilizará como entrada al modelo.

```javascript
const input = tf.tensor([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
```

Ahora podemos usar el método `model.predict` para generar predicciones a partir del tensor de entrada. Este método devuelve un objeto `tf.Tensor`, que podemos usar para generar los objetos 3D.

```javascript
model.predict(input).then(output => {
  // The output tensor can be used to generate 3D objects!
});
```

## Renderizando los objetos 3D

Ahora que hemos generado los objetos 3D, debemos renderizarlos en el navegador. Usaremos la biblioteca `three.js` para hacer esto.

Primero, necesitamos crear un objeto `Scene`. Este objeto contendrá los objetos 3D que queremos renderizar.

```javascript
const scene = new THREE.Scene();
```

A continuación, necesitamos crear un objeto `Cámara`. Este objeto define la perspectiva desde la que queremos ver la escena.

```javascript
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
```

Ahora podemos crear el objeto `Renderer`. Este objeto tomará los objetos `Scene` y `Camera` y los representará en la página.

```javascript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

Finalmente, necesitamos crear los objetos 3D y agregarlos al objeto `Scene`. Usaremos el tensor `output` del paso anterior para generar los objetos 3D.

```javascript
const geometry = new THREE.Geometry();
for (let i = 0; i < output.shape[0]; i++) {
  geometry.vertices.push(new THREE.Vector3(i, output.get(i, 0), 0));
}
const material = new THREE.LineBasicMaterial({ color: 0xff0000 });
const line = new THREE.Line(geometry, material);
scene.add(line);
```

## Animando los objetos 3D

Ahora que hemos renderizado los objetos 3D, necesitamos animarlos. Usaremos la función `requestAnimationFrame` para hacer esto. Esta función le dice al navegador que llame a una función específica antes del próximo repintado.

```javascript
function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
```

## Seguimiento de la cabeza del usuario

Ahora que hemos animado los objetos 3D, necesitamos rastrear la cabeza del usuario para que los objetos 3D aparezcan en la posición correcta. Usaremos la biblioteca `ar.js` para hacer esto.

Primero, necesitamos crear un objeto `ARController`. Este objeto seguirá la cabeza del usuario y mostrará los objetos 3D en la posición correcta.

```javascript
const arController = new ARController(renderer, {
  cameraParametersUrl: './camera_para.dat',
  maxDetectionRate: 60,
  canvasWidth: 640,
  canvasHeight: 480
});
```

A continuación, debemos decirle al `ARController` que rastree la cabeza del usuario. Podemos hacer esto con el método `loadNFTMarker`. Este método toma un `markerUrl`, que es la ruta a un archivo de marcador. Podemos usar `markerUrl` para cargar un archivo de marcador desde el directorio `nft-marker-files`.

```javascript
arController.loadNFTMarker('./nft-marker-files/hiro.jpg');
```

Finalmente, necesitamos decirle al `ARController` que comience a rastrear la cabeza del usuario. Podemos hacer esto con el método `startNFTMarkerTracking`.

```javascript
arController.startNFTMarkerTracking();
```

## Visualización de los objetos 3D

Ahora que hemos rastreado la cabeza del usuario, podemos mostrar los objetos 3D en la posición correcta. Usaremos el método `arController.getNFTMarker` para obtener el marcador que el usuario está mirando actualmente. Este método devuelve un objeto `THREE.Object3D`, que podemos agregar al objeto `Scene`.

```javascript
const marker = arController.getNFTMarker(0);
scene.add(marker);
```

## ¡Eso es todo!

¡Eso es todo al respecto! Ahora debería tener una aplicación AR en funcionamiento que represente objetos 3D en la posición correcta en relación con la cabeza del usuario.

## Recursos

* [TensorFlow.js](https://js.tensorflow.org/)
* [Tres.js](https://tresjs.org/)
* [AR.js](https://github.com/jeromeetienne/AR.js)