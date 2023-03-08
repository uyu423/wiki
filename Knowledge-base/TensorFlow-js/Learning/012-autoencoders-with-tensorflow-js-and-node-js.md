---
title: 012: TensorFlow.js 및 Node.js를 사용한 자동 인코더
description: 
published: true
date: 2023-02-02T09:36:40.397Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:36:38.723Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [012: Autoencoders with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/012-autoencoders-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 자동 인코더

딥 러닝은 데이터의 복잡한 표현을 학습하기 위한 강력한 도구입니다. 오토인코더는 감독되지 않은 방식으로 이러한 표현을 학습하는 데 사용할 수 있는 일종의 신경망입니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 간단한 자동 인코더를 빌드할 것입니다. 우리는 손으로 쓴 숫자의 이미지로 구성된 MNIST 데이터 세트를 사용할 것입니다.

## 시작하기

먼저 의존성을 설치해야 합니다. 다음 라이브러리를 사용할 것입니다.

* [TensorFlow.js](https://www.tensorflow.org/js)
* [mnist](https://www.npmjs.com/package/mnist)

npm을 사용하여 설치할 수 있습니다.

```
npm install tensorflowjs mnist
```

다음으로 MNIST 데이터 세트를 로드해야 합니다. 이를 위해 mnist 라이브러리를 사용할 것입니다.

```javascript
const mnist = require('mnist');

// Load the dataset
const dataset = mnist.set(0.7, 0.3);

// Get the training and test sets
const [train, test] = dataset.getTrainingAndTestSets();
```

MNIST 데이터 세트는 각각 28x28픽셀인 손글씨 숫자 이미지로 구성됩니다. 이 이미지를 오토인코더의 입력으로 사용하기 전에 크기가 784인 벡터로 병합해야 합니다.

```javascript
// Flatten the images into vectors
const trainX = train.map(example => example.input);
const testX = test.map(example => example.input);
```

## 오토인코더 만들기

이제 데이터 세트가 있으므로 자동 인코더 빌드를 시작할 수 있습니다. 하나의 숨겨진 레이어가 있는 완전히 연결된 신경망을 사용할 것입니다. 히든 레이어는 입력 레이어보다 단위 수가 적어 네트워크가 압축된 데이터 표현을 학습하도록 합니다.

```javascript
// Create the model
const model = tf.sequential();

// Add the input layer
model.add(tf.layers.dense({
  inputShape: [784],
  units: 64
}));

// Add the hidden layer
model.add(tf.layers.dense({
  units: 32
}));

// Add the output layer
model.add(tf.layers.dense({
  units: 784
}));
```

모델에 대한 옵티마이저와 손실 함수를 지정해야 합니다. Adam 옵티마이저와 평균 제곱 오차(MSE) 손실 함수를 사용할 것입니다.

```javascript
// Compile the model
model.compile({
  optimizer: 'adam',
  loss: 'meanSquaredError'
});
```

## Autoencoder 교육

이제 모델이 있으므로 훈련 세트에서 훈련할 수 있습니다. 우리는 20 epoch 동안 모델을 훈련시킬 것입니다.

```javascript
// Train the model
model.fit(tf.tensor2d(trainX), tf.tensor2d(trainX), {
  epochs: 20
}).then(() => {
  // Evaluate the model on the test set
  model.evaluate(tf.tensor2d(testX), tf.tensor2d(testX));
});
```

## 결과 시각화

학습 결과를 시각화하기 위해 `tensorflow-vis` 라이브러리를 사용하여 재구성된 이미지를 플롯할 수 있습니다.

```javascript
// Install the library
npm install @tensorflow/tfjs-vis

// Load the library
const tfvis = require('@tensorflow/tfjs-vis');

// Plot the results
tfvis.show.image3d(
  model.predict(tf.tensor2d(testX)),
  {
    width: 28,
    height: 28
  }
);
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 간단한 자동 인코더를 빌드하는 방법을 살펴보았습니다. 또한 오토인코더를 훈련하고 결과를 시각화하는 방법도 살펴보았습니다.

Autoencoder는 차원 축소, 노이즈 제거, 생성 모델링과 같은 다양한 작업에 사용할 수 있습니다. 자동 인코더에 대해 자세히 알아보려면 다음 리소스를 추천합니다.

* [딥 러닝 101 – 오토인코더 소개](https://towardsdatascience.com/deep-learning-101-introduction-to-autoencoders-3e44bffe2b7d)
* [오토인코더](http://cs.stanford.edu/people/karpathy/convnetjs/demo/autoencoder.html)
* [변형 오토인코더](https://jmetzen.github.io/2015-11-27/vae.html)