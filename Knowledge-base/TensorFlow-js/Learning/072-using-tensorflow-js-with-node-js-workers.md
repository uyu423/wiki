---
title: 072: Node.js 작업자와 함께 TensorFlow.js 사용
description: 
published: true
date: 2023-02-02T23:37:03.445Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:37:01.829Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [072: Using TensorFlow.js with Node.js Workers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/072-using-tensorflow-js-with-node-js-workers)
{.links-list}


# Node.js 작업자와 함께 TensorFlow.js 사용

TensorFlow.js는 JavaScript에서 기계 학습을 위한 강력한 도구이며 Node.js 작업자는 멀티 코어 시스템을 활용하고 기본 이벤트 루프를 원활하게 실행할 수 있는 훌륭한 방법을 제공합니다.

이 게시물에서는 TensorFlow.js를 Node.js 작업자와 함께 사용하여 기계 학습 모델을 교육하는 방법을 살펴보겠습니다. 작업을 시작하고 실행하기 위한 간단한 예제로 시작한 다음 작업자 풀을 사용하여 여러 모델을 병렬로 교육하는 방법을 보여주는 더 복잡한 예제를 살펴보겠습니다.

## TensorFlow.js 및 Workers 시작하기

시작하려면 TensorFlow.js 및 @tensorflow/tfjs-node Worker 플러그인을 설치해야 합니다. npm으로 다음과 같이 할 수 있습니다.

```
npm install @tensorflow/tfjs @tensorflow/tfjs-node
```

TensorFlow.js와 Worker 플러그인이 설치되면 일부 코드 작성을 시작할 수 있습니다.

MNIST 데이터 세트에서 손으로 쓴 숫자를 분류하는 간단한 모델을 훈련하는 것으로 시작하겠습니다. 먼저 데이터세트를 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset
const mnistData = tf.data.web('https://storage.googleapis.com/tfjs-examples/mnist_train_small.csv');
```

다음으로 데이터 세트를 TensorFlow.js가 이해할 수 있는 형식으로 변환하는 함수를 정의합니다. 이 함수는 숫자 배열을 사용하여 TensorFlow.js 텐서를 반환합니다.

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

데이터 세트가 로드되고 변환 함수가 정의되면 모델을 교육할 준비가 된 것입니다. 두 개의 조밀한 계층으로 간단한 순차 모델을 정의합니다.

```javascript
// Define a simple sequential model
const model = tf.sequential();
model.add(tf.layers.dense({ units: 784, activation: 'relu', inputShape: [784] }));
model.add(tf.layers.dense({ units: 10, activation: 'softmax' }));
```

다음으로 Adam 옵티마이저와 범주형 교차 엔트로피 손실 함수를 사용하여 모델을 컴파일합니다.

```javascript
// Compile the model
model.compile({
  optimizer: tf.train.adam(),
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy'],
});
```

이제 모델을 훈련할 준비가 되었습니다. 우리는 tf.data.Dataset 객체를 가져오고 데이터 세트에서 모델을 훈련시키는 fitDataset() 메서드를 사용할 것입니다.

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

그게 다야! 이제 TensorFlow.js 및 Node.js 작업자를 사용하여 간단한 기계 학습 모델을 교육했습니다.

## 병렬로 여러 모델 훈련

이전 섹션에서는 TensorFlow.js를 Node.js 작업자와 함께 사용하여 단일 모델을 교육하는 방법을 살펴보았습니다. 그러나 Node.js 작업자를 사용하여 여러 모델을 병렬로 훈련할 수도 있습니다.

이렇게 하려면 먼저 작업자 풀을 만들어야 합니다. tf.js-node Worker 플러그인을 사용하여 이를 수행할 수 있습니다.

```javascript
const { WorkerPool } = require('@tensorflow/tfjs-node');

// Create a Worker pool with two workers
const pool = new WorkerPool({ numWorkers: 2 });
```

작업자 풀이 있으면 데이터 세트에서 모델을 교육하는 함수를 정의할 수 있습니다. 이 함수는 데이터 세트와 모델을 사용하고 훈련된 모델로 확인되는 Promise를 반환합니다.

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

trainModel() 함수를 정의하면 이제 여러 모델을 병렬로 훈련할 수 있습니다. trainModel() 함수를 데이터 세트 배열에 매핑하여 이를 수행합니다.

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

이 코드에서는 Promise.all() 메서드를 사용하여 여러 모델을 병렬로 교육합니다. Promise.all() 메서드는 Promise 배열을 사용하고 배열의 모든 Promise가 확인되면 확인되는 단일 Promise를 반환합니다.

## 마무리

이 게시물에서는 TensorFlow.js를 Node.js 작업자와 함께 사용하여 기계 학습 모델을 교육하는 방법을 살펴보았습니다. 시작하기 위한 간단한 예제를 살펴보고 작업자 풀을 사용하여 여러 모델을 병렬로 교육하는 방법을 살펴보았습니다.

TensorFlow.js에 대해 자세히 알아보려면 TensorFlow.js 웹사이트(https://js.tensorflow.org/)와 TensorFlow.js 예제(https://github.com/)를 확인하세요. tensorflow/tfjs-예제).