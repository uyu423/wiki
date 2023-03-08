---
title: 072: Using TensorFlow.js with Node.js Workers
description: 
published: true
date: 2023-02-02T23:37:06.482Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:37:01.835Z
---

- [072: Uso de TensorFlow.js con trabajadores de Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}
- [072：将 TensorFlow.js 与 Node.js Worker 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}
- [072: Node.js 작업자와 함께 TensorFlow.js 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}


# Using TensorFlow.js with Node.js Workers

TensorFlow.js is a powerful tool for machine learning in JavaScript, and Node.js Workers provide a great way to take advantage of multi-core systems and keep your main event loop running smoothly.

In this post, we'll look at how to use TensorFlow.js with Node.js Workers to train machine learning models. We'll start with a simple example to get things up and running, and then we'll look at a more complex example that shows how to use a Worker pool to train multiple models in parallel.

## Getting started with TensorFlow.js and Workers

To get started, we'll need to install TensorFlow.js and the @tensorflow/tfjs-node Worker plugin. We can do this with npm:

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

Once we have TensorFlow.js and the Worker plugin installed, we can start writing some code.

We'll start by training a simple model to classify handwritten digits from the MNIST dataset. First, we'll need to load the dataset:

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset
const mnistData = tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv');
```

Next, we'll define a function to convert the dataset into a format that TensorFlow.js can understand. This function will take an array of numbers and return a TensorFlow.js tensor:

```javascript
// Convert the dataset into a format that TensorFlow.js can understand
const convertToTensor = (data) => {
  // Wrapping this in a tidy will dispose the tensor when we're done
  return tf.tidy(() => {
    // Convert the data to a TensorFlow.js tensor
    const tensor = tf.tensor2d(data, [data.length, 784]);
    
    // Normalize the data
    return tensor.div(tf.scalar(255));
  });
};
```

With our dataset loaded and our conversion function defined, we're ready to train our model. We'll define a simple sequential model with two dense layers:

```javascript
// Define a simple sequential model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 784, activation: 'relu', inputShape: [784] }));
model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));
```

Next, we'll compile the model using the Adam optimizer and the categorical cross entropy loss function:

```javascript
// Compile the model
model.compile({
  optimizer: tf.train.adam(),
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy'],
});
```

Now we're ready to train the model. We'll use the fitDataset() method, which takes a tf.data.Dataset object and trains the model on the dataset:

```javascript
// Train the model
model.fitDataset(mnistData, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
    },
  },
});
```

That's it! We've now trained a simple machine learning model using TensorFlow.js and Node.js Workers.

## Training multiple models in parallel

In the previous section, we saw how to use TensorFlow.js with Node.js Workers to train a single model. However, Node.js Workers can also be used to train multiple models in parallel.

To do this, we'll first need to create a Worker pool. We can do this with the tf.js-node Worker plugin:

```javascript
const { WorkerPool } = require('@tensorflow/tfjs-node');

// Create a Worker pool with two workers
const pool = new WorkerPool({ numWorkers: 2 });
```

Once we have a Worker pool, we can define a function to train a model on a dataset. This function will take a dataset and a model, and it will return a Promise that resolves to the trained model:

```javascript
// Define a function to train a model on a dataset
const trainModel = (dataset, model) => {
  return new Promise((resolve, reject) => {
    // Use a tidy to clean up when we're done
    tf.tidy(() => {
      // Train the model
      model.fitDataset(dataset, {
        epochs: 10,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}, accuracy = ${logs.acc}`);
          },
        },
      })
      .then(() => {
        // Resolve the promise with the trained model
        resolve(model);
      })
      .catch((err) => {
        // Reject the promise with the error
        reject(err);
      });
    });
  });
};
```

With our trainModel() function defined, we can now train multiple models in parallel. We'll do this by mapping our trainModel() function over an array of datasets:

```javascript
// Create an array of datasets
const datasets = [
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv'),
  tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_test.csv'),
];

// Train multiple models in parallel
Promise.all(datasets.map((dataset) => {
  return trainModel(dataset, model);
}))
.then(() => {
  // All models have been trained
  console.log('All models have been trained');
})
.catch((err) => {
  // One or more models failed to train
  console.error(err);
});
```

In this code, we're using the Promise.all() method to train multiple models in parallel. The Promise.all() method takes an array of Promises and returns a single Promise that resolves when all of the Promises in the array have resolved.

## Wrapping up

In this post, we've seen how to use TensorFlow.js with Node.js Workers to train machine learning models. We've looked at a simple example to get started, and we've seen how to use a Worker pool to train multiple models in parallel.

If you're interested in learning more about TensorFlow.js, be sure to check out the TensorFlow.js website (https://js.tensorflow.org/) and the TensorFlow.js examples (https://github.com/tensorflow/tfjs-examples).