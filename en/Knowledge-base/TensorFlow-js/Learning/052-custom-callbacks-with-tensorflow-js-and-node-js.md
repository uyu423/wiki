---
title: 052: Custom Callbacks with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T19:04:52.051Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:04:47.425Z
---

- [052: Devoluciones de llamadas personalizadas con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}
- [052：使用 TensorFlow.js 和 Node.js 的自定义回调***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}
- [052: TensorFlow.js 및 Node.js를 사용한 커스텀 콜백***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# Custom Callbacks with TensorFlow.js and Node.js

In this post, we'll learn how to create custom callbacks with TensorFlow.js and Node.js.

TensorFlow.js is a powerful tool for machine learning in JavaScript. It allows you to create, train, and deploy machine learning models in the browser or in Node.js.

Node.js is a JavaScript runtime that allows you to run JavaScript code on your server. Node.js is also an important platform for TensorFlow.js, as it allows you to deploy machine learning models to production.

Creating a custom callback with TensorFlow.js is a great way to extend the functionality of your machine learning models. Callbacks allow you to define custom functions that are executed at specific points during the training process. For example, you can use a callback to track the training loss, or to save the model after each epoch.

In this post, we'll learn how to create a custom callback with TensorFlow.js and Node.js. We'll also learn how to use the callback to track the training loss and save the model after each epoch.

## What is a Callback?

A callback is a function that is executed at a specific point during the training process. Callbacks are a powerful way to extend the functionality of your machine learning models.

There are two types of callbacks in TensorFlow.js:

* **Layers callbacks:** These callbacks are executed when a layer is created.
* **Model callbacks:** These callbacks are executed when the model is compiled and training begins.

In this post, we'll focus on model callbacks.

## Creating a Custom Callback

Creating a custom callback with TensorFlow.js is simple. First, we need to create a new JavaScript file and import the TensorFlow.js library.

Next, we need to create a new class that extends the Callback class. This class will contain our custom callback functions.

In our example, we'll create a custom callback that tracks the training loss and saves the model after each epoch.

```javascript
const tf = require('@tensorflow/tfjs');

class CustomCallback extends tf.Callback {
  onTrainBegin(logs) {
    // This function is executed when training begins.
    // We can use it to initialize our custom variables.
    this.losses = [];
  }

  onTrainEnd(logs) {
    // This function is executed when training ends.
    // We can use it to save our custom variables.
    console.log('Final loss: ', this.losses[-1]);
  }

  onBatchEnd(batch, logs) {
    // This function is executed at the end of each training batch.
    // We can use it to track the training loss.
    this.losses.push(logs.loss);
  }

  onEpochEnd(epoch, logs) {
    // This function is executed at the end of each training epoch.
    // We can use it to save the model.
    console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    this.model.save(`model_at_epoch_${epoch}.h5`);
  }
}
```

In this example, we've created four custom callback functions:

* onTrainBegin: This function is executed when training begins. We can use it to initialize our custom variables.
* onTrainEnd: This function is executed when training ends. We can use it to save our custom variables.
* onBatchEnd: This function is executed at the end of each training batch. We can use it to track the training loss.
* onEpochEnd: This function is executed at the end of each training epoch. We can use it to save the model.

## Using the Custom Callback

Now that we've created our custom callback, let's see how to use it.

First, we need to create a new TensorFlow.js model. In this example, we'll use a simple sequential model.

Next, we need to compile the model using the custom callback.

Finally, we can train the model using the fit method.

```javascript
const model = tf.sequential();

model.compile({
  optimizer: 'sgd',
  loss: 'binaryCrossentropy',
  callbacks: new CustomCallback()
});

model.fit(x, y, {
  epochs: 10
});
```

In this example, we've used the custom callback to track the training loss and save the model after each epoch.

## Conclusion

In this post, we've learned how to create custom callbacks with TensorFlow.js and Node.js. We've also learned how to use the callback to track the training loss and save the model after each epoch.

Creating custom callbacks is a great way to extend the functionality of your machine learning models. Callbacks allow you to define custom functions that are executed at specific points during the training process.

If you're interested in learning more about TensorFlow.js, be sure to check out the TensorFlow.js website (https://js.tensorflow.org/).