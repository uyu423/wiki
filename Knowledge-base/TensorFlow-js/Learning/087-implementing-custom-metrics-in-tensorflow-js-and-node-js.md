---
title: 087: TensorFlow.js 및 Node.js에서 맞춤 측정항목 구현
description: 
published: true
date: 2023-02-03T03:17:26.664Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:17:25.101Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [087: Implementing Custom Metrics in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/087-implementing-custom-metrics-in-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js에서 맞춤 측정항목 구현

이 게시물에서는 TensorFlow.js 및 Node.js에서 맞춤 측정항목을 구현하는 방법을 알아봅니다.

## 맞춤 측정항목이란 무엇인가요?

사용자 지정 메트릭은 기계 학습 모델의 성능을 추적하는 데 사용할 수 있는 사용자 정의 메트릭입니다. 모델의 정확도에서 교육 반복 횟수에 이르기까지 무엇이든 추적하는 데 사용할 수 있습니다.

## 맞춤 측정항목을 사용하는 이유는 무엇인가요?

사용자 지정 메트릭을 사용하여 기본 제공 메트릭보다 더 세분화된 방식으로 기계 학습 모델의 성능을 추적할 수 있습니다. 또한 여러 교육 실행에서 모델의 성능을 추적하는 데 사용할 수도 있습니다.

## TensorFlow.js에서 맞춤 측정항목을 구현하는 방법은 무엇인가요?

TensorFlow.js는 맞춤 측정항목을 구현하는 데 사용할 수 있는 CustomCallback 클래스를 제공합니다. CustomCallback 클래스는 함수를 인수로 사용합니다. 이 함수는 두 가지 인수를 사용합니다.

- 첫 번째 인수는 현재 데이터 배치입니다.
- 두 번째 인수는 현재 에포크입니다.

이 함수는 메트릭 이름과 메트릭 값이 있는 개체를 반환해야 합니다.

다음은 CustomCallback 클래스를 사용하여 기계 학습 모델의 정확도를 추적하는 방법의 예입니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

const callback = tf.callbacks.CustomCallback((batch, epoch) => {
  const acc = model.evaluate(batch.x, batch.y)[1].dataSync()[0];
  console.log('Accuracy: ', acc);
  return {'accuracy': acc};
});

model.fit(x, y, {
  epochs: 10,
  callbacks: [callback]
});
```

이 예에서는 모델의 정확도를 추적하기 위해 사용자 지정 지표를 정의했습니다. CustomCallback 클래스는 각 시대가 끝날 때 정의한 함수를 호출합니다. 이 함수는 현재 데이터 배치에서 모델을 평가하고 정확도를 반환합니다.

## Node.js에서 커스텀 측정항목을 구현하는 방법은 무엇인가요?

Node.js는 async/await 키워드를 사용하여 TensorFlow.js와 유사한 기능을 제공합니다.

다음은 기계 학습 모델의 정확성을 추적하기 위해 async/await를 사용하는 방법의 예입니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 100, activation: 'relu', inputShape: [784]}));
model.add(tf.layers.dense({units: 10, activation: 'softmax'}));

model.compile({
  optimizer: 'sgd',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});

async function run() {
  for (let i = 0; i < 10; i++) {
    const res = await model.fit(x, y);
    console.log('Accuracy: ', res.history.acc);
  }
}

run();
```

이 예에서는 모델의 정확도를 추적하기 위해 사용자 지정 지표를 정의했습니다. async/await 키워드는 각 시대가 끝날 때 정의한 함수를 호출합니다. 이 함수는 현재 데이터 배치에서 모델을 평가하고 정확도를 반환합니다.