---
title: 011: TensorFlow.js 및 Node.js를 사용하는 GRU(Gated Recurrent Unit)
description: 
published: true
date: 2023-02-02T09:17:22.432Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:17:20.855Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [011: Gated Recurrent Unit (GRU) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/011-gated-recurrent-unit-gru-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용하는 GRU(Gated Recurrent Unit)

이 게시물에서는 GRU(Gated Recurrent Unit)에 대해 알아보고 이를 TensorFlow.js 및 Node.js로 구현하는 방법을 알아봅니다.

## Gated Recurrent Unit이 무엇인가요?

GRU는 순환 신경망(RNN)의 한 유형입니다. RNN은 텍스트, 오디오 또는 시계열 데이터와 같은 데이터 시퀀스를 처리할 수 있는 신경망입니다.

GRU는 게이트를 사용하여 네트워크의 정보 흐름을 제어하는 일종의 RNN입니다. 게이트는 네트워크가 장기 종속성을 더 잘 학습하도록 도와줍니다.

## TensorFlow.js로 GRU 구현

TensorFlow.js를 사용하여 GRU를 구현합니다. TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

먼저 TensorFlow.js를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 모델 학습에 사용할 데이터를 로드해야 합니다. 우리는 손으로 쓴 숫자의 데이터 세트인 MNIST 데이터 세트를 사용할 것입니다.

다음 코드를 사용하여 MNIST 데이터 세트를 로드할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

이제 데이터를 로드했으므로 모델을 정의할 수 있습니다. 우리는 64개의 유닛이 있는 GRU를 사용할 것입니다.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

다음으로 모델을 컴파일해야 합니다. Adam 옵티마이저와 범주형 교차 엔트로피 손실 함수를 사용합니다.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

이제 모델을 훈련할 수 있습니다. 우리는 그것을 10 epoch 동안 훈련시킬 것입니다.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

그게 다야! 우리는 이제 손으로 쓴 숫자를 분류하도록 GRU를 훈련시켰습니다.

## Node.js로 GRU 구현

Node.js를 사용하여 GRU를 훈련할 수도 있습니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

먼저 TensorFlow.js를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 모델 학습에 사용할 데이터를 로드해야 합니다. 우리는 손으로 쓴 숫자의 데이터 세트인 MNIST 데이터 세트를 사용할 것입니다.

다음 코드를 사용하여 MNIST 데이터 세트를 로드할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MNIST dataset.
const mnistData = require('mnist-data');

// Convert the MNIST data to a TensorFlow.js tensor.
const mnistTensor = tf.tensor3d(mnistData.images, [mnistData.images.length, 28, 28]);
```

이제 데이터를 로드했으므로 모델을 정의할 수 있습니다. 우리는 64개의 유닛이 있는 GRU를 사용할 것입니다.

```javascript
// Define the model.
const model = tf.sequential();
model.add(tf.layers.gru({units: 64, inputShape: [28, 28]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));
```

다음으로 모델을 컴파일해야 합니다. Adam 옵티마이저와 범주형 교차 엔트로피 손실 함수를 사용합니다.

```javascript
// Compile the model.
model.compile({optimizer: 'adam', loss: 'categoricalCrossentropy', metrics: ['accuracy']});
```

이제 모델을 훈련할 수 있습니다. 우리는 그것을 10 epoch 동안 훈련시킬 것입니다.

```javascript
// Train the model.
model.fit(mnistTensor, mnistData.labels, {epochs: 10}).then(() => {
  // The model is trained!
});
```

그게 다야! 우리는 이제 손으로 쓴 숫자를 분류하도록 GRU를 훈련시켰습니다.