---
title: 092: Using Variational Autoencoders (VAEs) in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T04:36:28.799Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:36:27.085Z
---

- [092: Uso de codificadores automáticos variacionales (VAEs) en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}
- [092：在 TensorFlow.js 和 Node.js 中使用变分自动编码器 (VAE)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}
- [092: TensorFlow.js 및 Node.js에서 VAE(Variational Autoencoder) 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}


# Using Variational Autoencoders (VAEs) in TensorFlow.js and Node.js

Variational autoencoders (VAEs) are a powerful tool for learning latent representations of data. In this post, we'll see how to use a VAE to learn a latent representation of MNIST data in TensorFlow.js and Node.js.

## What is a VAE?

A VAE is a probabilistic model that can be used to learn a latent representation of data. VAEs are similar to autoencoders in that they learn to compress data into a latent space. However, VAEs are probabilistic models, which means that they can be used to generate new data samples from the latent space.

## How do VAEs work?

VAEs work by learning a latent representation of data. The latent space is a lower-dimensional space that captures the essential features of the data. The VAE then uses this latent space to generate new data samples.

## How do I use a VAE in TensorFlow.js?

To use a VAE in TensorFlow.js, you need to first install the TensorFlow.js library. You can do this using the Node.js package manager:

```
npm install @tensorflow/tfjs
```

Next, you need to load the MNIST data. You can do this using the tf.data.Dataset API:

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

Now, you need to create the VAE. You can do this using the tf.layers.vae() function:

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

Finally, you need to train the VAE. You can do this using the fit() method:

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## How do I use a VAE in Node.js?

To use a VAE in Node.js, you need to first install the TensorFlow.js library. You can do this using the Node.js package manager:

```
npm install @tensorflow/tfjs
```

Next, you need to load the MNIST data. You can do this using the tf.data.Dataset API:

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

Now, you need to create the VAE. You can do this using the tf.layers.vae() function:

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

Finally, you need to train the VAE. You can do this using the fit() method:

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## Conclusion

In this post, we've seen how to use a VAE to learn a latent representation of MNIST data in TensorFlow.js and Node.js. VAEs are a powerful tool for learning latent representations of data.