---
title: 031: Training and Fine-Tuning Models with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T14:17:59.839Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:17:55.376Z
---

- [031: Modelos de entrenamiento y ajuste fino con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}
- [031：使用 TensorFlow.js 和 Node.js 训练和微调模型***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}
- [031: TensorFlow.js 및 Node.js로 모델 훈련 및 미세 조정***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/031-training-and-fine-tuning-models-with-tensorflow-js-and-node-js)
{.links-list}


#031: Training and Fine-Tuning Models with TensorFlow.js and Node.js

TensorFlow.js is an open-source library for numerical computation that allows you to create and train machine learning models in the browser. Node.js is a JavaScript runtime that allows you to run JavaScript code outside of the browser. In this post, we'll show you how to use TensorFlow.js and Node.js to train and fine-tune machine learning models.

##Installing TensorFlow.js

To install TensorFlow.js, you'll need to have Node.js and npm (the Node.js package manager) installed. You can check if you have Node.js installed by running the following command in your terminal:

```
node -v
```

If you don't have Node.js installed, you can download it [here](https://nodejs.org/en/).

Once you have Node.js and npm installed, you can install TensorFlow.js with the following command:

```
npm install @tensorflow/tfjs
```

##Training a Model

Now that you have TensorFlow.js installed, you can start training your own machine learning models. In this section, we'll show you how to train a simple linear regression model.

First, let's create some training data. We'll use the built-in tf.tensor2d() function to create a 2D tensor (an array of arrays) with 10 rows and 1 column. We'll fill the tensor with random numbers from a normal distribution with a mean of 0 and a standard deviation of 1.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4], [6, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7], [6, 1]);
```

Next, we'll define our model. We'll use the tf.sequential() function to create a sequential model, which is a linear stack of layers. Then, we'll use the tf.layers.dense() function to add a dense layer to the model. A dense layer is a fully connected layer, which means that all the nodes in the previous layer are connected to all the nodes in the dense layer. We'll specify that the dense layer has 1 output node and that the input shape is [1].

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

Now that we've defined our model, we need to compile it. Compiling the model will configure the model for training. We'll use the tf.train.sgd() function to create a stochastic gradient descent optimizer. The optimizer will be used to minimize the loss function during training. We'll also specify that we want to optimize for mean squared error.

```javascript
model.compile({optimizer: tf.train.sgd(0.1), loss: 'meanSquaredError'});
```

Now that our model is compiled, we can start training it. We'll use the model.fit() function to train the model. We'll specify the training data (xs and ys), the number of epochs (100), and the batch size (1). Epochs are the number of times the model will go through the training data. The batch size is the number of training examples the model will use before updating the model's weights.

```javascript
model.fit(xs, ys, {epochs: 100, batchSize: 1});
```

##Making Predictions

Now that our model is trained, we can use it to make predictions. We'll use the model.predict() function to make predictions. We'll pass in a 1D tensor with the value 3. The model will output a 1D tensor with the value 9.

```javascript
model.predict(tf.tensor2d([3], [1, 1])).print();
```

##Fine-Tuning a Model

Once you have a trained model, you may want to fine-tune it to improve its performance. In this section, we'll show you how to fine-tune a pre-trained model.

We'll start by loading a pre-trained model. We'll use the tf.loadLayersModel() function to load the model. We'll need to specify the URL of the model. You can find a list of pre-trained models [here](https://github.com/tensorflow/tfjs-models/tree/master/models).

```javascript
const model = tf.loadLayersModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

Now that we've loaded the model, we need to compile it. We'll use the same compile() function as before. However, this time we'll specify that we want to optimize for classification accuracy.

```javascript
model.compile({optimizer: tf.train.sgd(0.0001), loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

Now we can start training the model. We'll use the fit() function again. However, this time we'll specify the number of epochs (5) and the validation data (xs and ys). The validation data is used to evaluate the model after each epoch.

```javascript
model.fit(xs, ys, {epochs: 5, validationData: [xs, ys]});
```

After training the model, we can use it to make predictions. We'll use the predict() function again. This time we'll pass in an image of a dog. The model will output an array of probabilities, one for each class. The highest probability will be the class the model predicts the image belongs to.

```javascript
model.predict(tf.tensor2d([image], [1, 224, 224, 3])).print();
```

##Conclusion

In this post, we've shown you how to use TensorFlow.js and Node.js to train and fine-tune machine learning models.