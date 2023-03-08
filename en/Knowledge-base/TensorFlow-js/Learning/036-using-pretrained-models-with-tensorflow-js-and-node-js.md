---
title: 036: Using Pretrained Models with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T15:36:46.897Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:36:42.356Z
---

- [036: Uso de modelos previamente entrenados con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}
- [036：将预训练模型与 TensorFlow.js 和 Node.js 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}
- [036: TensorFlow.js 및 Node.js로 사전 학습된 모델 사용***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}


# Introduction

In this post, we'll learn how to use pretrained models with TensorFlow.js and Node.js. We'll start by discussing what pretrained models are and why they're useful. We'll then go over how to load and use pretrained models in TensorFlow.js. Finally, we'll see how to deploy a pretrained model with Node.js.

# What are Pretrained Models?

Pretrained models are models that have been trained on a large dataset. These models can be used to perform various tasks, such as image classification, object detection, and text classification.

Pretrained models are useful because they allow us to use the knowledge of a large dataset without having to train our own model from scratch. This can save us a lot of time and effort.

# Loading Pretrained Models

TensorFlow.js provides a number ofpretrained models that can be loaded and used in your own applications. To load a pretrained model, you'll first need to install TensorFlow.js. You can do this using npm:

```
npm install @tensorflow/tfjs
```

Once TensorFlow.js is installed, you can load a pretrained model using the tf.loadModel() function. For example, to load the MobileNet model, you would use the following code:

```javascript
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

# Using Pretrained Models

Once you've loaded a pretrained model, you can use it to perform various tasks. For example, if you're using a pretrained image classification model, you can use the model to classify images.

To use a pretrained model, you'll first need to get the model's input and output layers. You can do this using the model.inputs and model.outputs properties. For example, to get the input and output layers of the MobileNet model, you would use the following code:

```javascript
const inputLayer = model.inputs[0];
const outputLayer = model.outputs[0];
```

Once you have the model's input and output layers, you can use the tf.tidy() function to run inference. The tf.tidy() function will clean up anytf.js Tensors that are created during the inference process. This is important because tf.js Tensors can take up a lot of memory.

To use the tf.tidy() function, you'll need to pass a function that contains the code for running inference. This function will be executed within a tidy context. For example, to run inference on the MobileNet model, you would use the following code:

```javascript
const results = tf.tidy(() => {
  // inputLayer is a tf.js Tensor with shape [1, 224, 224, 3]
  // outputLayer is a tf.js Tensor with shape [1, 1000]
  const output = model.predict(inputLayer);
  return output.dataSync();
});
```

# Deploying Pretrained Models

Once you've trained a model, you'll need to deploy it so that it can be used by other applications. TensorFlow.js provides a number of ways to deploy pretrained models.

One way to deploy a pretrained model is to use the tf.model.save() function. This function will save the model to a JSON file. For example, to save the MobileNet model, you would use the following code:

```javascript
await model.save('file:///model');
```

You can then load the model from the JSON file using the tf.loadModel() function.

Another way to deploy a pretrained model is to use the tf.model.toJSON() function. This function will return the model as a JSON object. For example, to get the MobileNet model as a JSON object, you would use the following code:

```javascript
const modelAsJSON = model.toJSON();
```

You can then save the JSON object to a file or database.

# Conclusion

In this post, we've learned how to use pretrained models with TensorFlow.js and Node.js. We've seen how to load and use pretrained models, and how to deploy pretrained models.