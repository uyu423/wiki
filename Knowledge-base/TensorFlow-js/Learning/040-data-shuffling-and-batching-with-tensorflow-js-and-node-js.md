---
title: 040: TensorFlow.js 및 Node.js를 사용한 데이터 셔플링 및 일괄 처리
description: 
published: true
date: 2023-02-02T16:17:34.752Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:17:33.107Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [040: Data Shuffling and Batching with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/040-data-shuffling-and-batching-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 데이터 셔플링 및 일괄 처리

TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

이 튜토리얼에서는 TensorFlow.js로 데이터를 섞고 일괄 처리하는 방법을 배웁니다. 다음 주제를 다룹니다.

* 데이터 셔플링이란 무엇이며 왜 중요한가요?
* TensorFlow.js로 데이터를 섞는 방법은 무엇입니까?
* TensorFlow.js로 데이터를 일괄 처리하는 방법은 무엇입니까?
* TensorFlow.js와 함께 데이터를 섞고 일괄 처리하는 방법은 무엇입니까?

## 데이터 셔플링이란 무엇이며 왜 중요한가요?

기계 학습 모델을 교육할 때 각 시대 전에 데이터를 섞는 것이 중요합니다. 이는 데이터를 섞지 않으면 모델이 데이터 세트의 처음 몇 개 샘플에 과적합될 수 있기 때문입니다.

데이터 셔플링은 데이터 세트의 샘플을 무작위로 재정렬하는 프로세스입니다. 이는 각 에포크 전이나 후에 수행할 수 있습니다.

데이터 섞기에는 두 가지 주요 이점이 있습니다.

* 모델이 데이터 세트의 처음 몇 개 샘플에 과적합되는 것을 방지하는 데 도움이 됩니다.
* 각 에포크마다 다른 샘플을 보기 때문에 모델이 더 빨리 수렴하는 데 도움이 될 수 있습니다.

## TensorFlow.js로 데이터를 섞는 방법은 무엇입니까?

TensorFlow.js로 데이터를 섞으려면 먼저 데이터를 `tf.data.Dataset`으로 변환해야 합니다.

`tf.data.array()` 또는 `tf.data.tensor()` 메서드를 사용하여 이를 수행할 수 있습니다.

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

데이터 세트가 있으면 `tf.data를 사용할 수 있습니다. 데이터를 섞는 shuffle()` 메서드:

```js
const shuffledDataset = dataset.shuffle();
```

## TensorFlow.js로 데이터를 일괄 처리하는 방법은 무엇인가요?

TensorFlow.js로 데이터를 일괄 처리하려면 먼저 데이터를 `tf.data.Dataset`으로 변환해야 합니다.

`tf.data.array()` 또는 `tf.data.tensor()` 메서드를 사용하여 이를 수행할 수 있습니다.

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

데이터 세트가 있으면 `tf.data를 사용할 수 있습니다. 데이터를 일괄 처리하는 batch()` 메서드:

```js
const batchedDataset = dataset.batch(2);
```

## TensorFlow.js와 함께 데이터를 섞고 일괄 처리하는 방법은 무엇인가요?

TensorFlow.js와 함께 데이터를 섞고 일괄 처리하려면 먼저 데이터를 `tf.data.Dataset`으로 변환해야 합니다.

`tf.data.array()` 또는 `tf.data.tensor()` 메서드를 사용하여 이를 수행할 수 있습니다.

```js
// Convert an array into a dataset
const dataset = tf.data.array([1, 2, 3, 4, 5]);

// Convert a tensor into a dataset
const dataset = tf.data.tensor([1, 2, 3, 4, 5]);
```

데이터 세트가 있으면 `tf.data를 사용할 수 있습니다. shuffle()` 및 `tf.data. 데이터를 섞고 일괄 처리하는 batch()` 메서드:

```js
const shuffledAndBatchedDataset = dataset.shuffle().batch(2);
```