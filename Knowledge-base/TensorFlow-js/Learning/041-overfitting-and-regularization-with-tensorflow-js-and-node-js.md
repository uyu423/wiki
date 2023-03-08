---
title: 041: TensorFlow.js 및 Node.js를 사용한 오버피팅 및 정규화
description: 
published: true
date: 2023-02-02T16:36:23.311Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:36:21.764Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [041: Overfitting and Regularization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/041-overfitting-and-regularization-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 오버피팅 및 정규화

기계 학습에서 과적합은 모델이 학습 데이터에서는 잘 수행되지만 테스트 데이터에서는 제대로 수행되지 않는 현상입니다. 이는 모델이 교육 데이터를 너무 가깝게 기억하고 새 데이터에 잘 일반화되지 않을 때 발생합니다.

과적합을 방지하는 한 가지 방법은 모델에 제약 조건을 추가하여 과적합을 방지하는 프로세스인 정규화를 사용하는 것입니다. 이 게시물에서는 가중치 정규화와 드롭아웃 정규화라는 두 가지 정규화 방법과 이를 TensorFlow.js 및 Node.js에서 구현하는 방법을 살펴보겠습니다.

## 가중치 정규화

가중치 정규화는 과적합을 방지하기 위해 모델의 가중치를 제한하는 방법입니다. 가중치 정규화에는 두 가지 일반적인 유형이 있습니다.

* L1 정규화: 가중치를 0에 가깝게 제한
* L2 정규화: 가중치가 작은 크기를 갖도록 제한

TensorFlow.js에서는 모델을 만들 때 'l1' 또는 'l2' 정규화 강도를 지정하여 가중치 정규화를 구현할 수 있습니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  kernelRegularizer: tf.regularizers.l2({l2: 0.01}),
  inputShape: [inputShape]
}));
```

위의 예에서는 강도가 0.01인 L2 정규화를 사용하고 있습니다.

## 드롭아웃 정규화

드롭아웃 정규화는 모델의 가중치 일부를 0으로 무작위로 설정하는 방법입니다. 이렇게 하면 모델이 더 적은 가중치로 작동하도록 학습하고 과적합을 방지할 수 있습니다.

TensorFlow.js에서 모델을 생성할 때 `dropoutRate`를 지정하여 드롭아웃 정규화를 구현할 수 있습니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({
  units: 100,
  dropoutRate: 0.1,
  inputShape: [inputShape]
}));
```

위의 예에서 우리는 0.1의 비율로 드롭아웃을 사용하고 있습니다. 즉, 가중치의 10%가 0으로 설정됩니다.

## 결론

이 게시물에서는 정규화의 두 가지 방법인 가중치 정규화와 드롭아웃 정규화를 살펴보고 이를 TensorFlow.js와 Node.js에서 구현하는 방법을 살펴보았습니다. 정규화는 과적합을 방지하는 강력한 도구이며 교차 검증과 같은 다른 방법과 함께 사용할 수 있습니다.