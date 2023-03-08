---
title: 008: TensorFlow.js 및 Node.js를 사용한 CNN(컨볼루션 신경망)
description: 
published: true
date: 2023-02-02T08:37:03.777Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:36:59.258Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [008: Convolutional Neural Networks (CNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/008-convolutional-neural-networks-cnn-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js에서 CNN(컨볼루션 신경망)을 구축하는 방법을 살펴보겠습니다. 이미지 인식을 위해 잘 알려진 데이터 세트인 MNIST 데이터 세트를 사용하여 CNN을 훈련할 것입니다.

컨벌루션 신경망은 이미지 인식 작업에 특히 적합한 신경망 유형입니다. 이미지의 공간적 구조를 잘 활용할 수 있기 때문이다.

# TensorFlow.js에서 CNN 구축

TensorFlow.js에서 CNN을 구축하는 방법부터 살펴보겠습니다. TensorFlow.js에 익숙하지 않다면 브라우저에서 실행되는 기계 학습용 JavaScript 라이브러리입니다.

먼저 MNIST 데이터 세트를 로드해야 합니다. MNIST 데이터 세트는 각각 28x28픽셀인 손글씨 숫자 이미지 모음입니다.

TensorFlow.js의 `tf.data.mnist` 함수를 사용하여 MNIST 데이터 세트를 로드할 수 있습니다. 이 함수는 `Dataset` 개체를 반환하며 이를 사용하여 CNN을 훈련할 수 있습니다.

```javascript
const mnistData = tf.data.mnist({
  train: true,
  testData: false
});
```

다음으로 컨볼루션 신경망을 정의해야 합니다. 선형 레이어 스택으로 구성된 일종의 신경망인 Sequential 모델을 사용할 것입니다.

28x28 이미지를 가져 와서 784 요소의 단일 벡터로 병합하는 `Flatten` 레이어를 추가하여 시작하겠습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

다음으로 `Dense` 레이어를 추가합니다. 이것은 완전히 연결된 계층으로, 계층의 각 뉴런이 이전 계층의 모든 뉴런에 연결되어 있음을 의미합니다.

128개의 뉴런을 갖고 `relu` 활성화 함수를 사용하도록 `Dense` 레이어를 구성합니다. 'relu' 활성화 함수는 신경망에 대한 일반적인 선택입니다. 0보다 작은 입력에 대해 0을 출력하고 0보다 크거나 같은 입력에 대해 입력을 출력합니다.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

마지막으로, 10개의 뉴런과 `softmax` 활성화 함수가 있는 `Dense` 레이어를 추가합니다. 'softmax' 활성화 함수는 신경망의 출력 계층에 대한 일반적인 선택입니다. 가능한 10자리에 대한 확률 분포를 출력합니다.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

이제 모델을 정의했으므로 컴파일해야 합니다. 모델을 컴파일할 때 손실 함수와 옵티마이저를 지정합니다.

손실 함수는 모델이 얼마나 잘 수행되고 있는지를 측정합니다. 우리는 손실 함수를 최소화하려고 합니다. 즉, 모델이 가능한 한 실제 레이블에 가까운 예측을 수행하기를 원합니다.

옵티마이저는 손실 함수를 최소화하기 위해 모델을 업데이트하는 데 사용되는 알고리즘입니다. 다양한 옵티마이저를 사용할 수 있지만 `sgd` 옵티마이저를 사용할 것입니다.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

이제 모델이 컴파일되었으므로 학습할 수 있습니다. 10 epoch 동안 학습할 것입니다. 즉, 모델이 전체 MNIST 데이터 세트를 10번 보게 됩니다.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# Node.js에서 CNN 만들기

TensorFlow.js에서 CNN을 빌드하는 방법을 살펴보았으니 이제 Node.js에서 이를 수행하는 방법을 살펴보겠습니다.

먼저 MNIST 데이터 세트를 로드해야 합니다. MNIST 데이터 세트는 각각 28x28픽셀인 손글씨 숫자 이미지 모음입니다.

`mnist` 패키지를 사용하여 MNIST 데이터셋을 로드할 수 있습니다. 이 패키지는 `Dataset` 개체를 반환하며 이를 사용하여 CNN을 훈련할 수 있습니다.

```javascript
const mnist = require('mnist');

const mnistData = mnist.training(0, 60000);
```

다음으로 컨볼루션 신경망을 정의해야 합니다. 선형 레이어 스택으로 구성된 일종의 신경망인 Sequential 모델을 사용할 것입니다.

28x28 이미지를 가져 와서 784 요소의 단일 벡터로 병합하는 `Flatten` 레이어를 추가하여 시작하겠습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.flatten({
  inputShape: [28, 28]
}));
```

다음으로 `Dense` 레이어를 추가합니다. 이것은 완전히 연결된 계층으로, 계층의 각 뉴런이 이전 계층의 모든 뉴런에 연결되어 있음을 의미합니다.

128개의 뉴런을 갖고 `relu` 활성화 함수를 사용하도록 `Dense` 레이어를 구성합니다. 'relu' 활성화 함수는 신경망에 대한 일반적인 선택입니다. 0보다 작은 입력에 대해 0을 출력하고 0보다 크거나 같은 입력에 대해 입력을 출력합니다.

```javascript
model.add(tf.layers.dense({
  units: 128,
  activation: 'relu',
  inputShape: [784]
}));
```

마지막으로, 10개의 뉴런과 `softmax` 활성화 함수가 있는 `Dense` 레이어를 추가합니다. 'softmax' 활성화 함수는 신경망의 출력 계층에 대한 일반적인 선택입니다. 가능한 10자리에 대한 확률 분포를 출력합니다.

```javascript
model.add(tf.layers.dense({
  units: 10,
  activation: 'softmax',
  inputShape: [128]
}));
```

이제 모델을 정의했으므로 컴파일해야 합니다. 모델을 컴파일할 때 손실 함수와 옵티마이저를 지정합니다.

손실 함수는 모델이 얼마나 잘 수행되고 있는지를 측정합니다. 우리는 손실 함수를 최소화하려고 합니다. 즉, 모델이 가능한 한 실제 레이블에 가까운 예측을 수행하기를 원합니다.

옵티마이저는 손실 함수를 최소화하기 위해 모델을 업데이트하는 데 사용되는 알고리즘입니다. 다양한 옵티마이저를 사용할 수 있지만 `sgd` 옵티마이저를 사용할 것입니다.

```javascript
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

이제 모델이 컴파일되었으므로 학습할 수 있습니다. 10 epoch 동안 학습할 것입니다. 즉, 모델이 전체 MNIST 데이터 세트를 10번 보게 됩니다.

```javascript
model.fit(mnistData, {
  epochs: 10
});
```

# 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 컨볼루션 신경망을 구축하는 방법을 살펴보았습니다. 또한 MNIST 데이터 세트에서 이러한 네트워크를 교육하는 방법도 살펴보았습니다.