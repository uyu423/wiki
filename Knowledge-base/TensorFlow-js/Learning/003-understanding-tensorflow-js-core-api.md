---
title: 003: TensorFlow.js 핵심 API 이해하기
description: 
published: true
date: 2023-02-02T07:23:28.188Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:23:26.577Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [003: Understanding TensorFlow.js Core API***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/003-understanding-tensorflow-js-core-api)
{.links-list}


# TensorFlow.js 핵심 API 이해하기

TensorFlow.js는 개발자가 브라우저에서 기계 학습 모델을 교육하고 배포할 수 있는 오픈 소스 웹 프레임워크입니다. TensorFlow.js Core API는 개발자가 JavaScript에서 수치 계산을 생성, 조작 및 최적화할 수 있는 하위 수준 API입니다.

## 텐서란?

텐서는 선형 변환을 나타내는 데이터 구조입니다. 간단히 말해서 텐서는 숫자의 배열입니다. TensorFlow.js에서 텐서에는 모양과 데이터 유형이 있습니다. 텐서의 모양은 배열의 크기와 차원이며, 데이터 유형은 텐서에 포함된 데이터 유형(예: `float32`, `int32`, `string`)입니다.

## 텐서 만들기

TensorFlow.js에서 텐서를 만드는 몇 가지 방법이 있습니다. 가장 간단한 방법은 `tf.tensor` 함수를 사용하여 JavaScript 배열에서 텐서를 생성하는 것입니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
```

`tf.tensor` 함수를 사용하면 텐서의 모양과 데이터 유형을 지정할 수도 있습니다.

```javascript
const b = tf.tensor([1, 2, 3, 4], [2, 2], 'int32');
```

스칼라(단일 숫자)에서 텐서를 만들 수도 있습니다.

```javascript
const c = tf.scalar(5);
```

## 텐서 조작

TensorFlow.js API의 다양한 기능을 사용하여 Tensor를 조작할 수 있습니다. 예를 들어 `tf.add` 함수를 사용하여 두 개의 텐서를 추가할 수 있습니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.add(a, b);
```

텐서에서 요소별 연산을 수행할 수도 있습니다. 요소별 작업은 텐서의 각 요소에 독립적으로 적용되는 작업입니다. 예를 들어 `tf.mul` 함수를 사용하여 두 개의 텐서를 요소별로 곱할 수 있습니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.mul(a, b);
```

## 텐서 변환하기

Tensor는 `.toXXX` 메서드를 사용하여 다른 데이터 구조로 변환할 수 있습니다. 예를 들어 `.toArray` 메서드를 사용하여 텐서를 JavaScript 배열로 변환할 수 있습니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toArray(); // [1, 2, 3, 4]
```

`.toString` 메서드를 사용하여 텐서를 문자열로 변환할 수도 있습니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = a.toString(); // "1 2 3 4"
```

## 계산 최적화

TensorFlow.js는 수치 계산을 최적화하는 데 사용할 수 있는 다양한 최적화 기능을 제공합니다. 예를 들어 `tf.clipByValue` 함수를 사용하여 텐서 값을 지정된 범위로 자를 수 있습니다.

```javascript
const a = tf.tensor([-5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5]);
const b = tf.clipByValue(a, -2, 2);
```

`tf.addN` 함수를 사용하여 텐서 목록에서 요소별 추가를 수행할 수도 있습니다.

```javascript
const a = tf.tensor([1, 2, 3, 4]);
const b = tf.tensor([5, 6, 7, 8]);
const c = tf.tensor([9, 10, 11, 12]);
const d = tf.addN([a, b, c]);
```

## 자세히 알아보기

TensorFlow.js는 개발자가 JavaScript에서 수치 계산을 생성, 조작 및 최적화할 수 있는 강력한 도구입니다. TensorFlow.js Core API는 JavaScript에서 수치 계산을 생성, 조작 및 최적화하기 위한 빌딩 블록을 제공하는 저수준 API입니다.

TensorFlow.js에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- TensorFlow.js 문서: https://js.tensorflow.org/
- TensorFlow.js GitHub 저장소: https://github.com/tensorflow/tfjs
- TensorFlow.js Core API 참조: https://js.tensorflow.org/api/core.html