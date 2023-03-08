---
title: 037: TensorFlow.js 및 Node.js를 사용한 사용자 정의 모델 측정항목
description: 
published: true
date: 2023-02-02T13:57:27.494Z
tags: 
editor: markdown
dateCreated: 2023-02-02T13:57:25.911Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [037: Custom Model Metrics with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/037-custom-model-metrics-with-tensorflow-js-and-node-js)
{.links-list}


# 037: TensorFlow.js 및 Node.js를 사용한 사용자 정의 모델 측정항목

이 게시물에서는 TensorFlow.js 및 Node.js에서 사용자 지정 모델 측정항목을 정의하는 방법을 알아봅니다.

## 커스텀 모델 측정항목이란 무엇인가요?

커스텀 모델 측정항목은 두 가지 인수를 사용하는 함수입니다.

- `yTrue`: 실측 값입니다.
- `yPred`: 예측 값입니다.

그리고 메트릭을 나타내는 단일 값을 반환합니다.

예를 들어 실측 값과 예측 값 사이의 평균 제곱 오차(MSE)를 계산하는 사용자 정의 지표를 정의할 수 있습니다. 다음 함수를 정의하여 이를 수행할 수 있습니다.

```javascript
function mse(yTrue, yPred) {
  // ...
}
```

## TensorFlow.js에서 커스텀 모델 메트릭 정의하기

TensorFlow.js에서는 `CustomCallback`을 생성하고 이를 `fit` 메소드에 전달하여 사용자 정의 모델 지표를 정의할 수 있습니다.

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

model.fit(x, y, {
  epochs: 10,
  callbacks: tf.callbacks.customCallback(['mse'], (logs) => {
    console.log(logs.mse);
  })
});
```

위의 코드에서 `mse` 메트릭을 계산하는 `CustomCallback`을 정의했습니다. 그런 다음 이 콜백을 'fit' 메서드에 전달했습니다. 이 메서드는 모델이 교육 중에 'mse' 메트릭을 계산하도록 지시합니다.

## Node.js에서 커스텀 모델 메트릭 정의하기

Node.js에서는 `tf.Metrics` 인스턴스를 생성하고 이를 `fit` 메소드에 전달하여 사용자 정의 모델 지표를 정의할 수 있습니다.

```javascript
const model = tf.sequential();
// ...

model.compile({
  // ...
  metrics: ['mse']
});

const metrics = new tf.Metrics(['mse']);

model.fit(x, y, {
  epochs: 10,
  callbacks: {
    onEpochEnd: (epoch, logs) => {
      metrics.update(logs);
    }
  }
});

metrics.print();
```

위의 코드에서 `mse` 메트릭을 계산하는 `tf.Metrics` 인스턴스를 만들었습니다. 그런 다음 이 인스턴스를 'fit' 메서드에 전달했습니다. 이 메서드는 훈련 중에 모델이 'mse' 메트릭을 계산하도록 지시합니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 사용자 지정 모델 메트릭을 정의하는 방법을 배웠습니다.