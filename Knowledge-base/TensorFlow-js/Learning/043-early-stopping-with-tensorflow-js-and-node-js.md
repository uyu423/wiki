---
title: 043: TensorFlow.js 및 Node.js로 조기 중지
description: 
published: true
date: 2023-02-02T17:04:41.506Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:04:37.001Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [043: Early Stopping with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/043-early-stopping-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js로 조기 중지

딥 러닝은 컴퓨터 비전, 자연어 처리, 예측 모델링 등 많은 분야에 혁명을 일으킨 신경망 기술입니다. TensorFlow.js는 JavaScript에서 딥 러닝 모델을 교육하고 배포하기 위한 강력한 오픈 소스 라이브러리입니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 과적합을 방지하는 데 도움이 되는 신경망 훈련 기술인 조기 중지를 구현하는 방법을 알아봅니다.

## 조기 중지가 무엇인가요?

조기 중지는 과적합을 방지하는 데 도움이 되는 신경망 훈련 기술입니다. 과적합은 모델이 너무 작거나 너무 단순한 데이터 세트에서 훈련되고 모델이 해당 데이터 세트에 특정한 패턴을 학습하기 시작할 때 발생합니다. 이로 인해 모델이 새 데이터에서 성능이 저하될 수 있습니다.

조기 중지는 모델이 이러한 패턴을 학습할 기회를 갖기 전에 훈련 프로세스를 중지하여 과적합을 방지하는 방법입니다. 검증 세트에서 모델의 성능을 모니터링하고 검증 세트의 성능이 떨어지기 시작하면 교육 프로세스를 중지하여 이를 수행할 수 있습니다.

## TensorFlow.js로 조기 중지 구현

TensorFlow.js를 사용하여 간단한 신경망을 만드는 것부터 시작하겠습니다. 이 네트워크는 두 개의 입력 값을 사용하고 세 번째 연속 출력 값을 예측합니다. 우리는 100포인트의 데이터 세트에서 훈련할 것입니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Create a neural network with two input nodes,
// one hidden layer with two nodes, and one output node
const model = tf.sequential();
model.add(tf.layers.dense({units: 2, inputShape: [2]}));
model.add(tf.layers.dense({units: 1}));

// Compile the model
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training
const xs = tf.tensor2d([[0, 0], [0, 1], [1, 0], [1, 1]]);
const ys = tf.tensor2d([[0], [1], [1], [0]]);

// Train the model
model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);
    }
  }
});
```

다음으로 검증 세트의 손실이 증가하기 시작하면 교육 프로세스를 중지하는 콜백을 추가합니다. 각 epoch에서 손실을 추적하고 현재 epoch의 손실을 이전 epoch의 손실과 비교하여 이를 수행합니다. 손실이 증가하면 학습 프로세스를 중지합니다.

```javascript
let previousLoss;

model.fit(xs, ys, {
  epochs: 100,
  validationData: [xs, ys],
  callbacks: {
    onEpochEnd: (epoch, log) => {
      console.log(`Epoch ${epoch}: loss = ${log.loss}`);

      if (previousLoss && log.loss > previousLoss) {
        model.stopTraining = true;
      }
      previousLoss = log.loss;
    }
  }
});
```

## 사용해 보세요

[이 코드를 직접 사용해 볼 수 있습니다](https://jsfiddle.net/jimmykim/9h5b7eLp/).

## 추가 정보

- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js](https://nodejs.org/en/)

## 추가 자료

- [TensorFlow.js를 사용한 과적합 및 과소적합](https://js.tensorflow.org/tutorials/overfitting_and_underfitting.html)
- [조기 중지](https://machinelearningmastery.com/how-to-avoid-overfitting-with-early-stopping/)