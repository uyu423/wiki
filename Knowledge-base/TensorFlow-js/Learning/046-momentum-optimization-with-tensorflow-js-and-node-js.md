---
title: 046: TensorFlow.js 및 Node.js를 사용한 모멘텀 최적화
description: 
published: true
date: 2023-02-02T17:43:33.307Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:43:28.641Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [046: Momentum Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/046-momentum-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# 046: TensorFlow.js 및 Node.js를 사용한 모멘텀 최적화

이 게시물에서는 **운동량 최적화**에 대해 알아봅니다. 이 기술은 신경망을 더 빠르게 훈련하고 로컬 최소값에 갇히는 것을 방지하는 데 도움이 되는 신경망 훈련 기술입니다.

## 모멘텀 최적화란?

모멘텀 최적화는 신경망을 더 빠르게 훈련하고 로컬 최소값에 갇히는 것을 방지하는 데 도움이 되는 신경망 훈련 기술입니다. 아이디어는 그래디언트 업데이트 방정식에 모멘텀 항을 추가하는 것입니다. 이 모멘텀 항은 훈련 과정이 보다 원활하게 "움직이는" 데 도움이 되는 "질량"과 같습니다.

모멘텀 항은 일반적으로 0과 1 사이의 값으로 설정됩니다. 0의 값은 모멘텀 항이 전혀 사용되지 않음을 의미하고 1의 값은 모멘텀 항이 최대한 사용됨을 의미합니다.

## TensorFlow.js에서 모멘텀 최적화를 사용하는 방법

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. TensorFlow.js를 사용하여 모멘텀 최적화를 사용하여 모델을 훈련할 수 있습니다.

TensorFlow.js에서 모멘텀 최적화를 사용하려면 `model.compile()` 함수의 `optimizer` 매개변수를 `'sgd'`로 설정해야 합니다. 그런 다음 `momentum` 매개변수를 원하는 값으로 설정할 수 있습니다.

예를 들면 다음과 같습니다.

```javascript
const model = tf.sequential();

model.add(tf.layers.dense({units: 10, inputShape: [5]}));
model.add(tf.layers.dense({units: 1}));

model.compile({
  optimizer: 'sgd',
  momentum: 0.9
});
```

이 예에서는 'optimizer' 매개변수를 ''sgd''로 설정하여 모멘텀 최적화와 함께 확률적 경사 하강법을 사용했습니다. 또한 `momentum` 매개변수를 `0.9`로 설정했습니다. 이는 모멘텀 항이 0.9의 가중치로 사용됨을 의미합니다.

## 모멘텀 최적화 사용의 이점

모멘텀 최적화를 사용하면 두 가지 주요 이점이 있습니다.

1. 모델을 더 빠르게 학습시키는 데 도움이 될 수 있습니다.

2. 지역 최소값에 갇히지 않도록 도와줍니다.

## 모멘텀 최적화를 사용해야 하는 경우

모멘텀 최적화를 사용할 수 있는 두 가지 주요 상황이 있습니다.

1. 모델을 더 빨리 훈련시키고 싶을 때.

2. 지역 최소값에 갇히는 것을 피하고 싶을 때.

## 모멘텀 최적화를 사용하지 않는 경우

모멘텀 최적화를 사용하지 않으려는 두 가지 상황도 있습니다.

1. 보다 안정적인 훈련을 원할 때.

2. 보다 신뢰할 수 있는 교육을 원할 때.

## 모멘텀 최적화 사용 팁

모멘텀 최적화를 사용하기 위한 몇 가지 팁은 다음과 같습니다.

1. 낮은 운동량 값으로 시작하여 점차적으로 증가시킵니다.

2. 확실하지 않은 경우 모멘텀 값 0.9를 사용합니다.

3. 훈련이 발산하지 않을 것이라고 확신하는 경우에만 모멘텀 값 1.0을 사용하십시오.

4. 훈련이 발산하는 경우 모멘텀 값을 줄여 보십시오.

5. 훈련이 너무 느리면 모멘텀 값을 높여보십시오.

## 더 읽을 수 있는 리소스

- [신경망 및 딥 러닝 초보자 가이드](https://www.digitalocean.com/community/tutorials/a-beginner-s-guide-to-neural-networks-and-deep-learning)

- [초보자를 위한 딥러닝: 올바른 옵티마이저 선택하기](https://www.analyticsvidhya.com/blog/2017/03/introduction-to-deep-learning-optimizers/)

- [모멘텀 최적화로 신경망을 빠르게 훈련시키는 방법](https://machinelearningmastery.com/how-to-train-your-neural-network-quickly-with-momentum-optimization/)