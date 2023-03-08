---
title: 035: Saving and Loading Models with TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-02T15:17:23.523Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:17:18.814Z
---

- [035: Guardar y cargar modelos con TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}
- [035：使用 TensorFlow.js 和 Node.js 保存和加载模型***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}
- [035: TensorFlow.js 및 Node.js로 모델 저장 및 로드***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}


## Saving and Loading Models with TensorFlow.js and Node.js

In this post, we'll learn how to save and load models with TensorFlow.js and Node.js. We'll cover the following topics:

- Saving a model with TensorFlow.js
- Loading a model with TensorFlow.js
- Using a model with Node.js

### Saving a model with TensorFlow.js

The first step is to save our model. We can do this with the `tf.Model.save` method. This method takes two arguments:

- `path`: The path to save the model to.
- `overwrite`: A boolean indicating whether or not to overwrite the existing model at the specified path.

Here's an example of saving a model:

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

model.save('/tmp/model/1/model.json', true);
```

In this example, we've saved our model to the `/tmp/model/1` directory. The `overwrite` parameter is set to `true`, so if there was already a model in that directory, it would be overwritten.

### Loading a model with TensorFlow.js

Now that we've saved our model, let's learn how to load it. We can do this with the `tf.loadModel` method. This method takes one argument:

- `path`: The path to the saved model.

Here's an example of loading a model:

```javascript
const model = await tf.loadModel('/tmp/model/1/model.json');
```

In this example, we've loaded our model from the `/tmp/model/1` directory.

### Using a model with Node.js

Once we've loaded our model, we can use it to make predictions. We can do this with the `model.predict` method. This method takes one argument:

- `inputs`: The input data to make predictions on. This can be a single `tf.Tensor` or an `Array` of `tf.Tensor`s.

Here's an example of using a model to make predictions:

```javascript
const input = tf.tensor2d([[1.0]]);
const output = model.predict(input);

output.print();
```

In this example, we've created a `tf.Tensor` with the value `[[1.0]]`. We've passed this tensor to the `model.predict` method, which returns a prediction. We've then printed the prediction to the console.