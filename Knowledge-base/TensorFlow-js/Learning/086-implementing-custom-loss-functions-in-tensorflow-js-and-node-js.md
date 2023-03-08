---
title: 086: TensorFlow.js 및 Node.js에서 사용자 지정 손실 함수 구현
description: 
published: true
date: 2023-02-03T03:04:38.617Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:04:33.668Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [086: Implementing Custom Loss Functions in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/086-implementing-custom-loss-functions-in-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js에서 사용자 지정 손실 함수 구현

이 게시물에서는 TensorFlow.js 및 Node.js에서 사용자 지정 손실 함수를 구현하는 방법을 살펴보겠습니다.

손실 함수는 기계 학습 모델 훈련의 중요한 부분입니다. 주어진 데이터 세트에서 모델의 오류를 계산하는 데 사용됩니다. 그런 다음 모델은 이 오류를 사용하여 가중치를 업데이트하고 예측을 개선합니다.

사용할 수 있는 다양한 손실 함수가 있으며 올바른 모델을 선택하는 것이 정확한 모델을 교육하는 데 중요합니다. 경우에 따라 표준 라이브러리에서 사용할 수 없는 사용자 지정 손실 함수를 사용할 수 있습니다.

TensorFlow.js에서는 실제 레이블과 예측 레이블이라는 두 가지 인수를 사용하는 함수를 만들어 사용자 지정 손실 함수를 구현할 수 있습니다. 함수는 손실을 나타내는 Tensor를 반환해야 합니다.

Node.js에서는 tf.losses 모듈을 사용하여 사용자 지정 손실 함수를 구현할 수 있습니다. 이 모듈은 사용할 수 있는 다양한 손실 함수를 제공하거나 tf.losses.Reduction 클래스를 구현하여 직접 생성할 수 있습니다.

## TensorFlow.js에서 커스텀 손실 함수 구현하기

TensorFlow.js에서 사용자 지정 손실 함수를 구현하려면 실제 레이블과 예측 레이블이라는 두 가지 인수를 사용하는 함수를 만들어야 합니다. 함수는 손실을 나타내는 Tensor를 반환해야 합니다.

예를 들어 평균 제곱 오류 손실 함수를 구현한다고 가정해 보겠습니다. 실제 레이블과 예측 레이블을 인수로 사용하고 평균 제곱 오차를 반환하는 함수를 생성하여 이를 수행할 수 있습니다.

```javascript
function meanSquaredError(trueLabels, predictedLabels) {
  // compute the mean squared error
  const loss = tf.losses.meanSquaredError(trueLabels, predictedLabels);
 
  // return the loss
  return loss;
}
```

그런 다음 이 함수를 사용하여 주어진 데이터 세트에서 모델의 손실을 계산할 수 있습니다.

```javascript
// true labels
const trueLabels = tf.tensor([1, 2, 3, 4]);
 
// predicted labels
const predictedLabels = tf.tensor([1, 2, 3, 4]);
 
// compute the loss
const loss = meanSquaredError(trueLabels, predictedLabels);
 
// print the loss
console.log(loss.dataSync()); // [0]
```

## Node.js에서 커스텀 손실 함수 구현하기

Node.js에서는 tf.losses 모듈을 사용하여 사용자 지정 손실 함수를 구현할 수 있습니다. 이 모듈은 우리가 사용할 수 있는 다양한 손실 함수를 제공하거나 tf.losses.Reduction 클래스를 구현하여 직접 생성할 수 있습니다.

예를 들어 평균 제곱 오류 손실 함수를 구현한다고 가정해 보겠습니다. tf.losses.Reduction을 상속하고 computeLoss() 메서드를 구현하는 클래스를 생성하여 이를 수행할 수 있습니다.

```javascript
class MeanSquaredError extends tf.losses.Reduction {
  computeLoss(labels, predictions) {
    // compute the mean squared error
    const loss = tf.losses.meanSquaredError(labels, predictions);
 
    // return the loss
    return loss;
  }
}
```

그런 다음 이 클래스를 사용하여 주어진 데이터 세트에서 모델의 손실을 계산할 수 있습니다.

```javascript
// true labels
const trueLabels = tf.tensor([1, 2, 3, 4]);
 
// predicted labels
const predictedLabels = tf.tensor([1, 2, 3, 4]);
 
// compute the loss
const loss = new MeanSquaredError().computeLoss(trueLabels, predictedLabels);
 
// print the loss
console.log(loss.dataSync()); // [0]
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 사용자 지정 손실 함수를 구현하는 방법을 살펴보았습니다. 실제 레이블과 예측 레이블을 인수로 사용하고 손실을 반환하는 함수를 만드는 방법을 살펴보았습니다. 또한 tf.losses 모듈을 사용하여 Node.js에서 사용자 지정 손실 함수를 구현하는 방법도 살펴보았습니다.