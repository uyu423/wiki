---
title: 088: TensorFlow.js 및 Node.js를 사용한 전이 학습
description: 
published: true
date: 2023-02-03T03:36:19.488Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:36:17.927Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [088: Transfer Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/088-transfer-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 088: TensorFlow.js 및 Node.js를 사용한 전이 학습

이 게시물에서는 전이 학습을 사용하여 TensorFlow.js 및 Node.js로 만든 모델을 재교육하는 방법을 알아봅니다.

전이 학습은 사전 훈련된 모델을 사용하고 이를 우리 자신의 데이터와 작업에 적용할 수 있게 해주는 기술입니다. 이는 처음부터 모델을 교육하기에 충분한 데이터가 없거나 유사한 작업에 대해 이미 교육된 모델을 사용하려는 경우에 유용합니다.

TensorFlow.js Model Zoo에서 사전 훈련된 모델을 사용할 것입니다. 우리가 사용할 모델은 ImageNet 데이터 세트에서 훈련된 MobileNetV2 모델입니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

## Node.js가 무엇인가요?

Node.js는 서버 측 코드를 실행하기 위한 JavaScript 런타임입니다.

## 선행 학습된 모델이란 무엇인가요?

선행 학습된 모델은 데이터 세트에서 학습된 모델입니다.

## ImageNet 데이터세트란 무엇인가요?

ImageNet은 이미지 분류 모델 학습에 자주 사용되는 대규모 이미지 데이터 세트입니다.

## 전이학습이란?

전이 학습은 사전 훈련된 모델을 사용하고 이를 우리 자신의 데이터와 작업에 적용할 수 있게 해주는 기술입니다.

## TensorFlow.js에서 전이 학습을 사용하려면 어떻게 해야 하나요?

TensorFlow.js에서 전이 학습을 사용하는 방법에는 두 가지가 있습니다.

1. TensorFlow.js Model Zoo에서 선행 학습된 모델을 사용할 수 있습니다.
2. TensorFlow, Keras 또는 PyTorch와 같은 다른 프레임워크의 사전 훈련된 모델을 사용할 수 있습니다.

## TensorFlow.js Model Zoo에서 선행 학습된 모델을 어떻게 사용하나요?

TensorFlow.js Model Zoo에서 선행 학습된 모델을 사용하려면 다음을 수행해야 합니다.

1. 사전 학습된 모델을 선택합니다.
2. 모델을 로드합니다.
3. 자신의 데이터로 모델을 재교육합니다.

## 선행 학습된 모델을 선택하려면 어떻게 해야 하나요?

선행 학습된 모델을 선택할 때 다음 사항을 고려해야 합니다.

1. 모델의 크기.
2. 모델의 정확성.
3. 모델의 계산 비용.

## 모델을 어떻게 불러오나요?

모델을 로드하려면 `tf.loadModel` 함수를 사용해야 합니다. 이 함수는 URL 또는 `tf.Model` 인스턴스를 사용합니다.

## 모델을 재교육하려면 어떻게 해야 하나요?

모델을 재교육하려면 `tf.train` 함수를 사용해야 합니다. 이 함수는 `tf.Model` 인스턴스와 `tf.Tensor` 인스턴스를 사용합니다. `tf.Tensor` 인스턴스에는 교육 데이터가 포함되어 있습니다.

## 전이 학습을 사용하면 어떤 이점이 있나요?

전이 학습을 사용하면 다음과 같은 몇 가지 이점이 있습니다.

1. 처음부터 모델을 교육하는 것보다 빠릅니다.
2. 더 적은 데이터가 필요합니다.
3. 새로운 작업에 대해 모델을 교육하는 데 사용할 수 있습니다.
4. 모델의 성능을 향상시키는 데 사용할 수 있습니다.

## 전이 학습 사용의 단점은 무엇인가요?

전이 학습을 사용하면 다음과 같은 몇 가지 단점이 있습니다.

1. 사전 훈련된 모델이 어떻게 작동하는지 이해하기 어려울 수 있습니다.
2. 사전 훈련된 모델을 디버깅하기 어려울 수 있습니다.
3. 사전 학습된 모델이 새 작업에 적합하지 않을 수 있습니다.

## 결론

이 게시물에서는 전이 학습을 사용하여 TensorFlow.js 및 Node.js로 만든 모델을 재교육하는 방법을 배웠습니다.