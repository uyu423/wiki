---
title: 098: Building Generative Adversarial Networks (GANs) in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T06:04:55.725Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:04:51.008Z
---

- [098: Creación de redes antagónicas generativas (GAN) en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}
- [098：在 TensorFlow.js 和 Node.js 中构建生成对抗网络 (GAN)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}
- [098: TensorFlow.js 및 Node.js에서 생성적 적대 신경망(GAN) 구축***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 098: Building Generative Adversarial Networks (GANs) in TensorFlow.js and Node.js

Developers looking to build generative models using TensorFlow.js and Node.js can do so by using a Generative Adversarial Network (GAN). In this post, we'll guide you through the process of building a GAN in TensorFlow.js and Node.js.

## What are GANs?

A GAN is a type of neural network that is used to generate new data from scratch. The network consists of two parts: a generator and a discriminator. The generator is responsible for generating new data, while the discriminator is responsible for determining whether the data is real or fake.

## Building a GAN in TensorFlow.js

The first step in building a GAN is to create a new file called `gan.js`. We'll start by requiring the `tensorflow` and `tfjs-node` modules:

```javascript
const tf = require('tensorflow');
const tfNode = require('tfjs-node');
```

Next, we'll define the generator and discriminator models:

```javascript
// Generator
const generator = tf.sequential();
generator.add(tf.layers.dense({units: 100, inputShape: [100]}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());
generator.add(tf.layers.dense({units: 784, activation: 'tanh'}));

// Discriminator
const discriminator = tf.sequential();
discriminator.add(tf.layers.dense({units: 784, inputShape: [784]}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

In the code above, we've defined a generator that takes in 100-dimensional noise vectors and outputs 784-dimensional vectors (i.e. 28x28 images). We've also defined a discriminator that takes in 784-dimensional vectors and outputs a single value that indicates whether the vector is real or fake.

Next, we need to compile the models:

```javascript
// Generator
generator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});

// Discriminator
discriminator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});
```

In the code above, we've specified that the models should be optimized using the Adam optimizer with a learning rate of 0.0001. We've also specified that the loss function for both models should be binary cross entropy.

## Training the GAN

Now that we've defined and compiled the models, we can start training the GAN. The training process consists of two steps: training the discriminator and training the generator.

### Training the Discriminator

The first step in training the GAN is to train the discriminator. We'll do this by generating a batch of fake data using the generator and a batch of real data using a training dataset. We'll then train the discriminator on these two batches of data.

```javascript
// Train the discriminator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of fake data
  const noise = tf.randomNormal([batchSize, 100]);
  const fakeData = generator.predict(noise);

  // Generate a batch of real data
  const realData = tf.data.nextBatch(batchSize, [784]);

  // Train the discriminator
  const xs = tf.concat([fakeData, realData], 0);
  const ys = tf.concat([tf.zeros([batchSize, 1]), tf.ones([batchSize, 1])], 0);
  discriminator.fit(xs, ys);
}
```

In the code above, we've generated a batch of fake data using the generator and a batch of real data using a training dataset. We've then concatenated these two batches of data and trained the discriminator on them.

### Training the Generator

Now that the discriminator has been trained, we can train the generator. We'll do this by generating a batch of noise vectors and passing them through the generator. We'll then train the generator on these noise vectors.

```javascript
// Train the generator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of noise vectors
  const noise = tf.randomNormal([batchSize, 100]);

  // Train the generator
  const ys = tf.ones([batchSize, 1]);
  generator.fit(noise, ys);
}
```

In the code above, we've generated a batch of noise vectors and passed them through the generator. We've then trained the generator on these noise vectors.

## Generating New Data

Now that the GAN has been trained, we can use it to generate new data. To do this, we'll generate a batch of noise vectors and pass them through the generator.

```javascript
// Generate a batch of noise vectors
const noise = tf.randomNormal([batchSize, 100]);

// Generate new data
const generatedData = generator.predict(noise);
```

In the code above, we've generated a batch of noise vectors and passed them through the generator. This has generated a batch of new data that can be used for any purpose.