---
title: 080: Integrating TensorFlow.js with AR/VR in Node.js
description: 
published: true
date: 2023-02-03T01:36:54.339Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:36:49.571Z
---

- [080: Integrando TensorFlow.js con AR/VR en Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}
- [080：在 Node.js 中将 TensorFlow.js 与 AR/VR 集成***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}
- [080: TensorFlow.js를 Node.js에서 AR/VR과 통합***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}


#080: Integrating TensorFlow.js with AR/VR in Node.js

TensorFlow.js is a powerful tool that allows us to create machine learning models and run them in the browser. This makes it ideal for creating applications that can take advantage of the processing power of the user's device, without the need for a powerful server.

In this post, we'll explore how to use TensorFlow.js to create a simple augmented reality (AR) application. We'll use the Three.js library to render 3D objects in the browser, and the AR.js library to track the user's head and display the 3D objects in the correct position.

## Setting up the project

We'll start by setting up a new Node.js project. Create a new directory for the project, and run `npm init` to create a `package.json` file.

We'll need a few libraries for this project. Install the following libraries with the `npm` command:

* `tensorflow`
* `@tensorflow/tfjs-node`
* `three`
* `ar.js`

## Creating the model

Now we can create the machine learning model that we'll use to generate the 3D objects. We'll use a simple linear regression model for this example.

Create a new file called `model.js` and import the `@tensorflow/tfjs-node` library.

```javascript
const tf = require('@tensorflow/tfjs-node');
```

Next, we'll define some constants that we'll use to train the model. The `LEARNING_RATE` constant defines how quickly the model should learn. The `BATCH_SIZE` constant defines how many data points to use when training the model. The `EPOCHS` constant defines how many times the model should go through the training data.

```javascript
const LEARNING_RATE = 0.01;
const BATCH_SIZE = 10;
const EPOCHS = 10;
```

Now we can define the model. We'll use a `sequential` model and add a `dense` layer. The `dense` layer is a fully connected layer that multiplies the input data by a set of weights and adds a bias term.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

We need to compile the model before we can train it. We'll use the `sgd` optimizer, which is a simple gradient descent optimizer. We'll also specify the `loss` function that the model should minimize, and the `metrics` that we want to track. In this case, we'll track the `meanSquaredError` and the `meanAbsoluteError`.

```javascript
model.compile({
  optimizer: tf.train.sgd(LEARNING_RATE),
  loss: 'meanSquaredError',
  metrics: ['meanSquaredError', 'meanAbsoluteError']
});
```

## Training the model

Now that we've defined the model, we need to train it on some data. We'll use a simple dataset for this example, consisting of 10 points.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7, 9, 11, 13, 15], [10, 1]);
```

We can now train the model. We'll specify the `batchSize`, the number of `epochs`, and `shuffle` the data before each epoch. We'll also specify a `validationData` set, which the model will use to evaluate the loss and metrics after each epoch.

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

## Saving the model

Once the model is trained, we need to save it so that we can use it in the browser. We can use the `tf.node.save` function to save the model to a `.pb` file.

```javascript
tf.node.save(model, './model.pb');
```

## Loading the model

Now that we've saved the model, we can load it in the browser. We'll use the `tf.loadFrozenModel` function to load the model. This function takes a `modelUrl` and a `weightsManifestUrl`. The `modelUrl` is the path to the `.pb` file that we saved in the previous step. The `weightsManifestUrl` is the path to a JSON file that contains information about the model's weights.

```javascript
const modelUrl = './model.pb';
const weightsManifestUrl = './weights_manifest.json';

tf.loadFrozenModel(modelUrl, weightsManifestUrl).then(model => {
  // The model is loaded!
});
```

## Generating 3D objects

Now that we've loaded the model, we can use it to generate 3D objects. We'll use the `tf.tensor` function to create a tensor from an array of numbers. This tensor will be used as the input to the model.

```javascript
const input = tf.tensor([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
```

We can now use the `model.predict` method to generate predictions from the input tensor. This method returns a `tf.Tensor` object, which we can use to generate the 3D objects.

```javascript
model.predict(input).then(output => {
  // The output tensor can be used to generate 3D objects!
});
```

## Rendering the 3D objects

Now that we've generated the 3D objects, we need to render them in the browser. We'll use the `three.js` library to do this.

First, we need to create a `Scene` object. This object will contain the 3D objects that we want to render.

```javascript
const scene = new THREE.Scene();
```

Next, we need to create a `Camera` object. This object defines the perspective from which we want to view the scene.

```javascript
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
```

Now we can create the `Renderer` object. This object will take the `Scene` and `Camera` objects and render them to the page.

```javascript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

Finally, we need to create the 3D objects and add them to the `Scene` object. We'll use the `output` tensor from the previous step to generate the 3D objects.

```javascript
const geometry = new THREE.Geometry();
for (let i = 0; i < output.shape[0]; i++) {
  geometry.vertices.push(new THREE.Vector3(i, output.get(i, 0), 0));
}
const material = new THREE.LineBasicMaterial({ color: 0xff0000 });
const line = new THREE.Line(geometry, material);
scene.add(line);
```

## Animating the 3D objects

Now that we've rendered the 3D objects, we need to animate them. We'll use the `requestAnimationFrame` function to do this. This function tells the browser to call a specified function before the next repaint.

```javascript
function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
```

## Tracking the user's head

Now that we've animated the 3D objects, we need to track the user's head so that the 3D objects appear in the correct position. We'll use the `ar.js` library to do this.

First, we need to create an `ARController` object. This object will track the user's head and display the 3D objects in the correct position.

```javascript
const arController = new ARController(renderer, {
  cameraParametersUrl: './camera_para.dat',
  maxDetectionRate: 60,
  canvasWidth: 640,
  canvasHeight: 480
});
```

Next, we need to tell the `ARController` to track the user's head. We can do this with the `loadNFTMarker` method. This method takes a `markerUrl`, which is the path to a marker file. We can use the `markerUrl` to load a marker file from the `nft-marker-files` directory.

```javascript
arController.loadNFTMarker('./nft-marker-files/hiro.jpg');
```

Finally, we need to tell the `ARController` to start tracking the user's head. We can do this with the `startNFTMarkerTracking` method.

```javascript
arController.startNFTMarkerTracking();
```

## Displaying the 3D objects

Now that we've tracked the user's head, we can display the 3D objects in the correct position. We'll use the `arController.getNFTMarker` method to get the marker that the user is currently looking at. This method returns a `THREE.Object3D` object, which we can add to the `Scene` object.

```javascript
const marker = arController.getNFTMarker(0);
scene.add(marker);
```

## That's it!

That's all there is to it! You should now have a working AR application that renders 3D objects in the correct position relative to the user's head.

## Resources

* [TensorFlow.js](https://js.tensorflow.org/)
* [Three.js](https://threejs.org/)
* [AR.js](https://github.com/jeromeetienne/AR.js)