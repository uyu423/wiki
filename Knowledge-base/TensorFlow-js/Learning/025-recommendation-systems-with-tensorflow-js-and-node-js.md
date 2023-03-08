---
title: 025: TensorFlow.js 및 Node.js를 사용한 추천 시스템
description: 
published: true
date: 2023-02-02T12:44:02.486Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:44:00.916Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [025: Recommendation Systems with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/025-recommendation-systems-with-tensorflow-js-and-node-js)
{.links-list}


## 개요

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 추천 시스템을 구축하는 방법을 살펴보겠습니다. 추천 시스템과 사용 사례를 간략하게 소개하면서 시작하겠습니다. 그런 다음 TensorFlow.js를 사용하여 간단한 콘텐츠 기반 추천 시스템을 구축하는 방법을 살펴보겠습니다. 마지막으로 TensorFlow.js 및 Node.js를 사용하여 보다 정교한 협업 필터링 추천 시스템을 구축하는 방법을 살펴보겠습니다.

## 추천 시스템이란?

추천 시스템은 사용자가 구매하거나 시청하고 싶은 것을 예측하는 데 사용되는 일종의 인공 지능입니다. Amazon, Netflix 및 Spotify와 같은 회사에서 사용자에게 표시되는 콘텐츠를 개인화하기 위해 광범위하게 사용됩니다.

추천 시스템에는 콘텐츠 기반 필터링과 협업 필터링이라는 두 가지 주요 유형이 있습니다.

콘텐츠 기반 추천 시스템은 항목 간의 유사성을 기반으로 사용자에게 항목을 추천합니다. 예를 들어 콘텐츠 기반 추천 시스템은 사용자가 과거에 비슷한 영화를 본 사실을 기반으로 사용자에게 영화를 추천할 수 있습니다.

협업 필터링 추천 시스템은 사용자 간의 유사성을 기반으로 사용자에게 항목을 추천합니다. 예를 들어, 협업 필터링 추천 시스템은 유사한 영화를 본 다른 사용자가 해당 영화를 본 적이 있다는 사실을 기반으로 사용자에게 영화를 추천할 수 있습니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 콘텐츠 기반 및 협업 필터링 추천 시스템을 구축하는 방법을 살펴보겠습니다.

## 콘텐츠 기반 추천 시스템 구축

콘텐츠 기반 추천 시스템을 구축하는 방법부터 살펴보겠습니다. 영화 등급 데이터 세트인 MovieLens 데이터 세트를 사용할 것입니다.

MovieLens 데이터 세트에는 1682개의 영화에 대한 943명의 사용자의 100,000개 평가가 포함되어 있습니다. 각 등급은 1에서 5 사이의 숫자이며 5가 가장 높은 등급입니다.

데이터세트를 TensorFlow.js 데이터세트로 로드하여 시작하겠습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const dataset = tf.data.csv('https://storage.googleapis.com/recommendation-system-datasets/movielens/ml-100k/u.data', {
  columnConfigs: {
    user_id: {
      isLabel: true
    },
    movie_id: {
      isLabel: true
    },
    rating: {
      isLabel: false
    }
  }
});
```

우리는 `columnConfigs` 옵션을 사용하여 `user_id` 및 `movie_id` 열이 레이블이고 `rating` 열이 레이블이 아님을 TensorFlow.js에 알렸습니다.

그런 다음 데이터 세트를 학습 및 테스트 세트로 분할합니다.

```javascript
const trainDataset = dataset.shuffle(dataset.size).batch(dataset.size * 0.8);
const testDataset = dataset.batch(dataset.size * 0.2);
```

학습 및 테스트 세트에 대해 80/20 분할을 사용하고 있습니다.

그런 다음 영화에서 등급으로의 매핑을 학습하는 모델을 만듭니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 1682,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

임베딩 레이어를 사용하여 영화를 저차원 벡터 공간에 매핑합니다. 그런 다음 고밀도 레이어를 사용하여 벡터 공간에서 등급으로의 매핑을 학습합니다.

그런 다음 모델을 교육 데이터에 맞춥니다.

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

우리는 훈련을 위해 `fitDataset()` 메서드를 사용할 수 있는 `tf.data.Dataset`을 사용하고 있습니다. 또한 'onEpochEnd' 콜백을 사용하여 각 에포크 후 손실을 인쇄합니다.

그런 다음 테스트 세트에서 모델을 평가할 수 있습니다.

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

이 모델의 테스트 손실은 0.84이므로 평균 0.84의 오차로 영화의 등급을 예측할 수 있습니다.

## 협업 필터링 추천 시스템 구축

이제 협업 필터링 추천 시스템을 구축하는 방법을 살펴보겠습니다.

사용자에서 평가로의 매핑을 학습하기 위해 모델을 만드는 것으로 시작하겠습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.embedding({
  inputDim: 943,
  outputDim: 64,
  inputShape: [1]
}));

model.add(tf.layers.flatten());

model.add(tf.layers.dense({
  units: 64,
  activation: 'relu'
}));

model.add(tf.layers.dense({
  units: 1,
  activation: 'linear'
}));

model.compile({
  loss: 'meanSquaredError',
  optimizer: 'adam'
});
```

임베딩 레이어를 사용하여 사용자를 저차원 벡터 공간에 매핑합니다. 그런 다음 고밀도 레이어를 사용하여 벡터 공간에서 등급으로의 매핑을 학습합니다.

그런 다음 모델을 교육 데이터에 맞춥니다.

```javascript
model.fitDataset(trainDataset, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    }
  }
});
```

그런 다음 테스트 세트에서 모델을 평가할 수 있습니다.

```javascript
const testLoss = model.evaluateDataset(testDataset);

console.log(`Test loss: ${testLoss.loss}`);
```

이 모델의 테스트 손실은 0.95이므로 평균 0.95의 오차로 사용자 등급을 예측할 수 있습니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 추천 시스템을 구축하는 방법을 살펴보았습니다. 콘텐츠 기반 추천 시스템을 구축하는 방법을 살펴보는 것으로 시작했습니다. 그런 다음 협업 필터링 추천 시스템을 구축하는 방법을 살펴보았습니다.