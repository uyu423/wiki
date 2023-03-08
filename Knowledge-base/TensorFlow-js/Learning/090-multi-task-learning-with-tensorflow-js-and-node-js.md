---
title: 090: TensorFlow.js 및 Node.js를 사용한 멀티태스크 학습
description: 
published: true
date: 2023-02-03T04:04:45.998Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:04:44.403Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [090: Multi-Task Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/090-multi-task-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 090: TensorFlow.js 및 Node.js를 사용한 멀티태스크 학습

이번 포스트에서는 MTL(Multi-Task Learning)에 대해 알아보고 이를 TensorFlow.js와 Node.js를 사용하여 구현하는 방법에 대해 알아보겠습니다.

MTL은 여러 작업에 대해 모델을 동시에 교육하여 모델의 성능을 개선하는 데 사용할 수 있는 기계 학습 기술입니다. 이는 모델이 작업 간의 유사점에서 학습하고 새 데이터에 대해 더 잘 일반화할 수 있도록 하므로 유익합니다.

## 다중 작업 학습이란 무엇입니까?

다중 작업 학습은 모델을 여러 작업에 대해 동시에 교육하여 모델의 성능을 개선하는 데 사용되는 기계 학습 기술입니다. 이는 모델이 작업 간의 유사점에서 학습하고 새 데이터에 대해 더 잘 일반화할 수 있도록 하므로 유익합니다.

다중 작업 학습에는 두 가지 주요 유형이 있습니다.

* **Homogeneous multi-task learning**: 분류 또는 회귀와 같이 작업 유형이 동일한 경우입니다.

* **이기종 다중 작업 학습**: 분류 및 회귀와 같이 작업 유형이 서로 다른 경우입니다.

## TensorFlow.js 및 Node.js로 멀티태스크 학습을 구현하는 방법

이 섹션에서는 TensorFlow.js 및 Node.js를 사용하여 MTL을 구현하는 방법을 알아봅니다.

다음 라이브러리를 사용할 것입니다.

* [TensorFlow.js](https://js.tensorflow.org/)
* [Node.js](https://nodejs.org/en/)

### 1. 라이브러리 설치

먼저 TensorFlow.js 및 Node.js 라이브러리를 설치해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
npm install node
```

### 2. 데이터 로드 및 준비

다음으로 데이터를 로드하고 준비해야 합니다. 붓꽃의 150가지 예가 포함된 [ 붓꽃 데이터세트 ](https://archive.ics.uci.edu/ml/datasets/iris)를 사용할 것입니다. 각 예제에는 네 가지 기능이 있습니다.

* 꽃받침 길이
* 꽃받침 폭
* 꽃잎 길이
* 꽃잎 폭

목표는 아이리스 꽃을 세 가지 다른 종으로 분류하도록 모델을 훈련시키는 것입니다.

* 아이리스 세토사
* 아이리스 버지니카
* 아이리스 버시컬러

다음 코드를 사용하여 데이터 세트를 로드할 수 있습니다.

```javascript
// Load the Iris dataset.
const irisDataset = tf.data.csv('https://storage.googleapis.com/tfjs-examples/multitask-iris/data/iris.csv');

// Prepare the dataset for training.
const irisDataset = irisDataset.map((example) => {
  const features = tf.tensor(example.features);
  const label = tf.tensor(example.label);

  return { features, label };
});
```

### 3. 모델 만들기

이제 모델을 만들어야 합니다. 우리는 두 개의 히든 레이어가 있는 간단한 신경망을 사용할 것입니다.

```javascript
// Create the model.
const model = tf.sequential();

model.add(tf.layers.dense({
  inputShape: [4],
  units: 10,
  activation: 'relu'
}));
model.add(tf.layers.dense({
  units: 10,
  activation: 'relu'
}));
model.add(tf.layers.dense({
  units: 3,
  activation: 'softmax'
}));
```

### 4. 모델 컴파일

이제 모델을 컴파일해야 합니다. 우리는 `categoricalCrossentropy` 손실 함수와 `sgd` 옵티마이저를 사용할 것입니다.

```javascript
// Compile the model.
model.compile({
  loss: 'categoricalCrossentropy',
  optimizer: 'sgd'
});
```

### 5. 모델 교육

이제 모델을 훈련할 수 있습니다. 10 epoch 동안 훈련하고 훈련 데이터에 `irisDataset`을 사용합니다.

```javascript
// Train the model.
model.fit(irisDataset, {
  epochs: 10
});
```

### 6. 모델 사용

이제 모델이 학습되었으므로 모델을 사용하여 새 데이터를 예측할 수 있습니다.

```javascript
// Use the model to make predictions.
model.predict(tf.tensor([
  [5.1, 3.5, 1.4, 0.2],
  [5.9, 3.0, 5.1, 1.8],
  [6.9, 3.1, 5.4, 2.1]
])).print();
```

그러면 다음이 인쇄됩니다.

```
Tensor
  [[0.992154717, 0.007842881, 0.000112332],
   [0.001711595, 0.998276472, 0.000011933],
   [0.000196449, 0.001836509, 0.997308   ]]
```

## 결론

이번 포스팅에서는 멀티태스킹 학습에 대해 알아보고 TensorFlow.js와 Node.js를 사용하여 구현하는 방법에 대해 알아보았습니다.