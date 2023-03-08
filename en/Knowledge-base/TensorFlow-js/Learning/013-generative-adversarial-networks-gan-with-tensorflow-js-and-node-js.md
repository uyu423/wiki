---
title: 013: Generative Adversarial Networks (GAN) with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T09:44:18.091Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:44:13.596Z
---

- [013: Redes antagónicas generativas (GAN) con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}
- [013：使用 TensorFlow.js 和 Node.js 的生成对抗网络 (GAN)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}
- [013: TensorFlow.js 및 Node.js를 사용한 GAN(Generative Adversarial Networks)***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}


# Generative Adversarial Networks (GAN) with TensorFlow.js and Node.js

In this post, we'll be looking at how to create a generative adversarial network (GAN) using TensorFlow.js and Node.js. We'll be using a GAN to generate new images of handwritten digits, based on the MNIST dataset.

## What is a GAN?

A GAN is a type of neural network that is used for generative modeling. Generative modeling is a task in machine learning where the goal is to generate new data that is similar to the training data.

GANs are made up of two neural networks, a generator and a discriminator. The generator network takes noise as input and generates images that are similar to the training data. The discriminator network takes images as input and tries to classify them as either real or fake.

The generator and discriminator networks are trained together in a zero-sum game, where the goal of the generator is to fool the discriminator into thinking that the generated images are real, and the goal of the discriminator is to correctly classify the images as either real or fake.

## Setting up the project

Before we can start training our GAN, we need to set up our project. We'll be using the following libraries:

- [TensorFlow.js](https://js.tensorflow.org/)
- [node-fetch](https://www.npmjs.com/package/node-fetch)
- [@tensorflow/tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node)

You can install these libraries using npm:

```
npm install tensorflowjs node-fetch @tensorflow/tfjs-node
```

## Loading the MNIST dataset

We'll be using the MNIST dataset for our GAN. The MNIST dataset is a collection of handwritten digits, each of which is represented as a 28x28 grayscale image.

We can use the node-fetch library to load the MNIST dataset from the TensorFlow.js Datasets repository:

```javascript
const tf = require('@tensorflow/tfjs-node');
const fetch = require('node-fetch');

// Load the MNIST dataset from the TensorFlow.js Datasets repository.
const mnistDataset = await tf.data.web('https://storage.googleapis.com/tfjs-datasets/mnist.json');
```

## Preprocessing the MNIST dataset

Once we've loaded the MNIST dataset, we need to preprocess it so that it can be used for training our GAN.

First, we'll convert the 28x28 grayscale images into 32x32 RGB images. We'll also normalize the pixel values to be in the range [-1, 1].

```javascript
// Convert the 28x28 grayscale images into 32x32 RGB images.
const mnistImages = mnistDataset.images.map(image => tf.image.resizeBilinear(image, [32, 32]));

// Normalize the pixel values to be in the range [-1, 1].
const mnistImages = mnistImages.map(image => image.toFloat().div(tf.scalar(255)).sub(tf.scalar(1)));
```

## Creating the generator network

Now that we've preprocessed the MNIST dataset, we can start creating our GAN.

First, we'll create the generator network. The generator network takes a noise vector as input and generates an image that is similar to the training data.

We'll use a noise vector with 100 dimensions. We'll use the tf.layers.dense layer to map the noise vector to an image with 32x32x3 dimensions.

```javascript
// Create the generator network.
const generator = tf.sequential();

// Map the noise vector to an image with 32x32x3 dimensions.
generator.add(tf.layers.dense({inputShape: [100], units: 32 * 32 * 3}));
generator.add(tf.layers.reshape({targetShape: [32, 32, 3]}));
```

## Creating the discriminator network

Next, we'll create the discriminator network. The discriminator network takes an image as input and tries to classify it as either real or fake.

We'll use the tf.layers.conv2d layer to create a convolutional neural network for the discriminator. We'll also use the tf.layers.leakyReLU layer to add nonlinearity to the network.

```javascript
// Create the discriminator network.
const discriminator = tf.sequential();

// Add a convolutional layer.
discriminator.add(tf.layers.conv2d({inputShape: [32, 32, 3], filters: 16, kernelSize: 3, strides: 2, padding: 'same'}));

// Add a Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add another convolutional layer.
discriminator.add(tf.layers.conv2d({filters: 32, kernelSize: 3, strides: 2, padding: 'same'}));

// Add another Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add a flatten layer.
discriminator.add(tf.layers.flatten());

// Add a fully connected layer.
discriminator.add(tf.layers.dense({units: 1}));

// Add a sigmoid activation layer.
discriminator.add(tf.layers.activation({activation: 'sigmoid'}));
```

## Training the GAN

Now that we've created the generator and discriminator networks, we can train our GAN.

First, we'll create a GAN model that combines the generator and discriminator networks.

Next, we'll compile the GAN model using the tf.train.adamOptimizer optimizer.

Finally, we'll train the GAN model using the tf.train.ganTrain() method.

```javascript
// Create a GAN model that combines the generator and discriminator.
const gan = tf.sequential();

// Add the generator to the GAN.
gan.add(generator);

// Freeze the generator.
generator.trainable = false;

// Add the discriminator to the GAN.
gan.add(discriminator);

// Compile the GAN using the Adam optimizer.
gan.compile({loss: 'binaryCrossentropy', optimizer: tf.train.adamOptimizer()});

// Train the GAN.
for (let i = 0; i < 100; i++) {
  // Get a batch of real images.
  const realImages = mnistImages.slice(i * 10, (i + 1) * 10);

  // Generate a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);

  // Create a batch of labels for the real and fake images.
  const realLabels = tf.ones([10, 1]);
  const fakeLabels = tf.zeros([10, 1]);

  // Train the discriminator on the real and fake images.
  const loss = await gan.fit([realImages, fakeImages], [realLabels, fakeLabels], {
    epochs: 1,
    batchSize: 10
  });

  // Generate and show a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);
  fakeImages.forEach((image, i) => {
    const canvas = document.createElement('canvas');
    canvas.width = 28;
    canvas.height = 28;
    const ctx = canvas.getContext('2d');
    const imageData = new ImageData(28, 28);
    const data = image.dataSync();
    for (let j = 0; j < 28 * 28; j++) {
      const k = j * 4;
      const imgIdx = j;
      imageData.data[k + 0] = (data[imgIdx + 0] + 1) * 127;
      imageData.data[k + 1] = (data[imgIdx + 1] + 1) * 127;
      imageData.data[k + 2] = (data[imgIdx + 2] + 1) * 127;
      imageData.data[k + 3] = 255;
    }
    ctx.putImageData(imageData, 0, 0);
    document.body.appendChild(canvas);
  });
}
```

## Generating new images

Once the GAN has been trained, we can use it to generate new images.

First, we'll generate a noise vector with 100 dimensions.

Next, we'll use the generator network to generate an image from the noise vector.

Finally, we'll show the generated image on the screen.

```javascript
// Generate a noise vector with 100 dimensions.
const noise = tf.randomNormal([1, 100]);

// Use the generator to generate an image from the noise vector.
const generatedImage = generator.predict(noise);

// Show the generated image.
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageData = new ImageData(28, 28);
const data = generatedImage.dataSync();
for (let i = 0; i < 28 * 28; i++) {
  const j = i * 4;
  const imgIdx = i;
  imageData.data[j + 0] = (data[imgIdx + 0] + 1) * 127;
  imageData.data[j + 1] = (data[imgIdx + 1] + 1) * 127;
  imageData.data[j + 2] = (data[imgIdx + 2] + 1) * 127;
  imageData.data[j + 3] = 255;
}
ctx.putImageData(imageData, 0, 0);
document.body.appendChild(canvas);
```

## Conclusion

In this post, we've seen how to create a GAN using TensorFlow.js and Node.js. We've also seen how to use the GAN to generate new images of handwritten digits.

If you want to learn more about GANs, I recommend the following resources:

- [Generative Adversarial Networks](https://arxiv.org/abs/1406.2661) (research paper)
- [Deep Learning with JavaScript](https://www.manning.com/livevideo/deep-learning-with-javascript) (video course)
- [Generative Adversarial Networks in TensorFlow](https://www.tensorflow.org/tutorials/generative/gan) (tutorial)