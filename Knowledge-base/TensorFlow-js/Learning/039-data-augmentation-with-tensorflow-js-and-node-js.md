---
title: 039: TensorFlow.js 및 Node.js를 사용한 데이터 증대
description: 
published: true
date: 2023-02-02T16:04:31.532Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:04:29.952Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [039: Data Augmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/039-data-augmentation-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 데이터 증대

## 소개

데이터 증대는 기존 데이터 샘플에서 새로운 데이터 샘플을 생성하여 데이터 세트의 크기를 인위적으로 늘리는 데 사용되는 기술입니다. 이는 원본 데이터 세트가 작고 가능한 한 많은 데이터로 기계 학습 모델을 교육하려는 경우에 특히 유용합니다.

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. Node.js는 웹 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임 환경입니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 데이터 증대를 수행하는 방법을 배웁니다. 데이터 증대가 무엇이고 왜 유용한지 살펴보는 것으로 시작하겠습니다. 그런 다음 TensorFlow.js에서 데이터 증대를 구현하는 방법을 살펴보겠습니다. 마지막으로 Node.js를 사용하여 데이터 증대 코드를 실행하는 방법을 배웁니다.

## 데이터 증강이란 무엇입니까?

데이터 증대는 기존 데이터 샘플에서 새로운 데이터 샘플을 생성하여 데이터 세트의 크기를 인위적으로 늘리는 데 사용되는 기술입니다. 이는 원본 데이터 세트가 작고 가능한 한 많은 데이터로 기계 학습 모델을 교육하려는 경우에 특히 유용합니다.

데이터 증대는 기존 데이터 샘플에 일련의 변환을 적용하여 작동합니다. 변환된 샘플은 새로운 데이터 샘플로 사용됩니다. 예를 들어 이미지 데이터 세트가 있는 경우 이미지에 회전, 자르기 및 뒤집기와 같은 변환을 적용하여 데이터 증대를 수행할 수 있습니다. 이렇게 하면 데이터 세트의 일부로 사용할 수 있는 새 이미지가 생성됩니다.

데이터 확대의 이점은 기계 학습 모델의 성능을 개선하는 데 도움이 될 수 있다는 것입니다. 이것은 증강 데이터셋이 원래 데이터셋보다 더 크고 더 다양하기 때문입니다. 이것은 모델이 보다 일반화 가능한 패턴을 학습하는 데 도움이 될 수 있습니다.

## TensorFlow.js의 데이터 증강

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 브라우저 또는 Node.js 환경에서 사용할 수 있습니다.

TensorFlow.js에서 `tf.data.Dataset` API를 사용하여 데이터 증대를 수행할 수 있습니다. 이 API를 사용하면 데이터 세트에 변환을 적용할 수 있습니다. `tf.image` 모듈에는 이미지 증대를 수행하는 데 사용할 수 있는 함수 세트가 포함되어 있습니다.

TensorFlow.js에서 데이터 증대를 사용하려면 먼저 `tf.data.Dataset` 객체를 생성해야 합니다. 그런 다음 `tf.image` 모듈을 사용하여 이 데이터 세트에 변환을 적용할 수 있습니다. 마지막으로 `.forEachAsync()` 메서드를 사용하여 각 데이터 샘플에서 확장 코드를 실행할 수 있습니다.

## Node.js

Node.js는 웹 브라우저 외부에서 JavaScript 코드를 실행할 수 있는 JavaScript 런타임 환경입니다. 서버 측 응용 프로그램을 만드는 데 사용할 수 있습니다.

Node.js는 다양한 작업을 수행하는 데 사용할 수 있는 내장 모듈 세트와 함께 제공됩니다. 데이터 증대를 위해 파일을 읽고 쓸 수 있는 `fs` 모듈을 사용할 것입니다.

## 예

이 예에서는 MNIST 데이터 세트를 사용합니다. 이 데이터 세트에는 손으로 쓴 숫자의 이미지가 포함되어 있습니다. 우리는 `tf.image` 모듈을 사용하여 이 데이터 세트에 대한 데이터 증대를 수행할 것입니다.

먼저 MNIST 데이터 세트를 로드해야 합니다. 우리는 `fs` 모듈을 사용하여 이것을 할 수 있습니다.


```javascript
var fs = require('fs');

var mnistData = fs.readFileSync('mnist.csv', {encoding: 'utf-8'});
```

다음으로 MNIST 데이터를 구문 분석해야 합니다. `tf.data.csv` 모듈을 사용하여 이를 수행할 수 있습니다.


```javascript
var csv = require('@tensorflow/tfjs-data/src/data/csv');

var mnistDataset = csv.parse(mnistData, {
  columnConfigs: {
    label: {
      isLabel: true
    }
  }
});
```

이제 데이터 세트가 있으므로 데이터 확대 적용을 시작할 수 있습니다. `tf.data.Dataset` 개체를 만드는 것으로 시작하겠습니다.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: sample.xs,
    ys: sample.ys
  };
});
```

다음으로 `tf.image.resizeBilinear()` 변환을 데이터세트에 적용합니다. 이 변환은 이미지의 크기를 조정합니다.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.resizeBilinear(sample.xs, [28, 28]),
    ys: sample.ys
  };
});
```

`tf.image.rotate()` 변환을 데이터 세트에 적용할 수도 있습니다. 이 변환은 이미지를 회전시킵니다.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.rotate(sample.xs, tf.scalar(Math.random() * 2.0 * Math.PI)),
    ys: sample.ys
  };
});
```

마지막으로 `tf.image.flipLeftRight()` 변환을 데이터 세트에 적용합니다. 이 변환은 이미지를 가로로 뒤집습니다.


```javascript
var mnistDataset = mnistDataset.map(function(sample) {
  return {
    xs: tf.image.flipLeftRight(sample.xs),
    ys: sample.ys
  };
});
```

이제 변환을 적용했으므로 `.forEachAsync()` 메서드를 사용하여 각 데이터 샘플에서 데이터 증대 코드를 실행할 수 있습니다.


```javascript
mnistDataset.forEachAsync(function(sample) {
  // augment data here
});
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 데이터 증대를 수행하는 방법을 배웠습니다. `tf.data.Dataset` API를 사용하여 데이터 세트에 변환을 적용하는 방법을 살펴보았습니다. 또한 `.forEachAsync()` 메서드를 사용하여 각 데이터 샘플에서 데이터 증대 코드를 실행하는 방법도 살펴보았습니다.