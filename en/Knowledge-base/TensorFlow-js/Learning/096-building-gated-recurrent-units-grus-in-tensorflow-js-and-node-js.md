---
title: 096: Building Gated Recurrent Units (GRUs) in TensorFlow.js and Node.js
description: 
published: true
date: 2023-02-03T05:38:04.462Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:37:59.467Z
---

- [096: Creación de unidades recurrentes cerradas (GRU) en TensorFlow.js y Node.js***Spanish** document is available*](/es/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}
- [096：在 TensorFlow.js 和 Node.js 中构建门控循环单元 (GRU)***Chinese Simplified** document is available*](/zh/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}
- [096: TensorFlow.js 및 Node.js에서 게이트 반복 단위(GRU) 빌드***Korean** document is available*](/ko/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}


# GRUs in TensorFlow.js and Node.js

## What are GRUs?

Gated recurrent units (GRUs) are a type of recurrent neural network (RNN) that have been designed to better capture long-term dependencies in sequential data. Unlike traditional RNNs, GRUs have two gates that control the flow of information into and out of the hidden state. The update gate decides how much of the new information to let in, while the reset gate decides how much of the old information to forget.

## Building a GRU in TensorFlow.js

TensorFlow.js is a JavaScript library for training and deploying machine learning models in the browser and in Node.js. In this tutorial, we'll see how to build a GRU in TensorFlow.js and use it to predict the next word in a sequence.

### Installing TensorFlow.js

If you're running this tutorial in the browser, you can install TensorFlow.js using the following script tag:

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
```

If you're running this tutorial in Node.js, you can install TensorFlow.js using the following command:

```
npm install @tensorflow/tfjs
```

### Loading the data

We'll be using a dataset of Amazon product reviews for this tutorial. The dataset contains reviews of different products, along with a star rating for each review.

We'll first need to load the dataset into TensorFlow.js. We can do this using the `tf.data.csv` function:

```
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/amazon_reviews_multilingual_CSV_V2/reviews.csv', {
  columnConfigs: {
    review_body: {
      isLabel: true
    },
    review_title: {
      isLabel: true
    },
    star_rating: {
      isLabel: true
    }
  }
});
```

### Preprocessing the data

We need to preprocess the data before we can train our model. We'll need to do the following preprocessing steps:

- Tokenize the reviews into sentences.
- Tokenize the sentences into words.
- Convert the words into integers.

We can use the `tf.tokenize` and `tf.tensorize` functions to tokenize and convert the reviews into integers, respectively.

```
const sentences = dataset.map(({review_body, review_title}) => tf.tokenize(review_body + ' ' + review_title));

const words = sentences.map(sentence => tf.tensor1d(sentence, 'int32'));
```

### Building the model

We're now ready to build our model. We'll be using a GRU for this tutorial. The first layer in our model will be an `Embedding` layer. This layer will take our words and convert them into vectors of a specific size. We can specify the size of the vectors using the `inputDim` and `outputDim` parameters. We'll also need to specify the `maskZero` parameter, which tells the layer to ignore words with a value of 0 (i.e. padding).

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

The next layer in our model will be the GRU layer. This layer will take the vectors output by the `Embedding` layer and convert them into a single vector that captures the information in the sequence. We can specify the size of the hidden state using the `units` parameter.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

The final layer in our model will be a `Dense` layer. This layer will take the vector output by the GRU layer and convert it into a probability distribution over the words in our vocabulary. We can specify the number of units in the layer using the `units` parameter. We'll also need to specify the `activation` and `kernelInitializer` parameters. The `activation` parameter specifies the activation function to use, while the `kernelInitializer` parameter specifies the initializer for the weights of the layer.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### Compiling the model

Before we can train our model, we need to compile it. We need to specify the following parameters when compiling the model:

- The optimizer to use. We'll be using the `adam` optimizer for this tutorial.
- The loss function to use. We'll be using the `categoricalCrossentropy` loss function for this tutorial.
- The metrics to track. We'll be tracking the `accuracy` metric for this tutorial.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### Training the model

We're now ready to train our model. We can do this using the `model.fit` method. We'll need to specify the following parameters when training the model:

- The training data. This should be a `tf.data.Dataset` object.
- The number of epochs to train for. We'll be training for 10 epochs for this tutorial.
- The batch size to use. We'll be using a batch size of 32 for this tutorial.

We can also specify a `validationData` parameter. This should be a `tf.data.Dataset` object that contains the validation data. If we specify a `validationData` parameter, the model will be evaluated on the validation data at the end of each epoch.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### Making predictions

We can use our trained model to make predictions on new data. We'll need to tokenize and convert the new data into integers before we can make predictions. We can use the `tf.tokenize` and `tf.tensorize` functions to do this:

```
const newSentences = tf.tokenize('this is a new sentence');
const newWords = tf.tensor1d(newSentences, 'int32');
```

We can then use the `model.predict` method to make predictions on the new data:

```
model.predict(newWords).print();
```

## Building a GRU in Node.js

In this section, we'll see how to build a GRU in Node.js. We'll be using the same Amazon product review dataset as in the previous section.

### Installing the dependencies

We'll need to install the following dependencies before we can start coding:

- `@tensorflow/tfjs-node`: This is the TensorFlow.js Node.js bindings.
- `csv-parser`: This is a CSV parser for Node.js.
- `tokenizer`: This is a natural language processing library for Node.js.

We can install these dependencies using the following command:

```
npm install @tensorflow/tfjs-node csv-parser tokenizer
```

### Loading the data

We'll start by loading the dataset into memory. We can do this using the `csv-parser` library:

```
const parser = csvParser();

parser.on('data', (data) => {
  // do something with the data
});

parser.on('end', () => {
  // do something when the parsing is finished
});

fs.createReadStream('reviews.csv').pipe(parser);
```

### Preprocessing the data

We need to preprocess the data before we can train our model. We'll need to do the following preprocessing steps:

- Tokenize the reviews into sentences.
- Tokenize the sentences into words.
- Convert the words into integers.

We can use the `tokenizer` library to tokenize the reviews into sentences and words. We can then use the `tf.tensor1d` function to convert the words into integers:

```
const sentences = reviews.map((review) => tokenizer.sentences(review));

const words = sentences.map((sentence) => tf.tensor1d(sentence.map((word) => tokenizer.words(word))));
```

### Building the model

We're now ready to build our model. We'll be using a GRU for this tutorial. The first layer in our model will be an `Embedding` layer. This layer will take our words and convert them into vectors of a specific size. We can specify the size of the vectors using the `inputDim` and `outputDim` parameters. We'll also need to specify the `maskZero` parameter, which tells the layer to ignore words with a value of 0 (i.e. padding).

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

The next layer in our model will be the GRU layer. This layer will take the vectors output by the `Embedding` layer and convert them into a single vector that captures the information in the sequence. We can specify the size of the hidden state using the `units` parameter.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

The final layer in our model will be a `Dense` layer. This layer will take the vector output by the GRU layer and convert it into a probability distribution over the words in our vocabulary. We can specify the number of units in the layer using the `units` parameter. We'll also need to specify the `activation` and `kernelInitializer` parameters. The `activation` parameter specifies the activation function to use, while the `kernelInitializer` parameter specifies the initializer for the weights of the layer.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### Compiling the model

Before we can train our model, we need to compile it. We need to specify the following parameters when compiling the model:

- The optimizer to use. We'll be using the `adam` optimizer for this tutorial.
- The loss function to use. We'll be using the `categoricalCrossentropy` loss function for this tutorial.
- The metrics to track. We'll be tracking the `accuracy` metric for this tutorial.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### Training the model

We're now ready to train our model. We can do this using the `model.fit` method. We'll need to specify the following parameters when training the model:

- The training data. This should be a `tf.data.Dataset` object.
- The number of epochs to train for. We'll be training for 10 epochs for this tutorial.
- The batch size to use. We'll be using a batch size of 32 for this tutorial.

We can also specify a `validationData` parameter. This should be a `tf.data.Dataset` object that contains the validation data. If we specify a `validationData` parameter, the model will be evaluated on the validation data at the end of each epoch.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### Making predictions

We can use our trained model to make predictions on new data. We'll need to tokenize and convert the new data into integers before we can make predictions. We can use the `tokenizer` and `tf.tensor1d` libraries to do this:

```
const newSentences = tokenizer.sentences('this is a new sentence');
const newWords = tf.tensor1d(newSentences.map((sentence) => tokenizer.words(sentence)));
```

We can then use the `model.predict` method to make predictions on the new data:

```
model.predict(newWords).print();
```

## Resources

- [Gated recurrent units](https://en.wikipedia.org/wiki/Gated_recurrent_unit)
- [TensorFlow.js](https://js.tensorflow.org/)
- [TensorFlow.js for Node.js](https://js.tensorflow.org/api/latest/#tensorflowjs_node)
- [csv-parser](https://www.npmjs.com/package/csv-parser)
- [tokenizer](https://www.npmjs.com/package/tokenizer)