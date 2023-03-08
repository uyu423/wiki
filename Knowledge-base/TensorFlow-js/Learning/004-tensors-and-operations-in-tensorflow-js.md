---
title: 004: TensorFlow.js의 텐서 및 작업
description: 
published: true
date: 2023-02-02T07:36:26.983Z
tags: 
editor: markdown
dateCreated: 2023-02-02T07:36:25.429Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [004: Tensors and Operations in TensorFlow.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/004-tensors-and-operations-in-tensorflow-js)
{.links-list}


# 소개

TensorFlow.js는 기계 학습을 위한 강력한 JavaScript 라이브러리이며 주요 기능 중 하나는 텐서 작업 기능입니다. 이 게시물에서는 TensorFlow.js에서 Tensor가 무엇이고 어떻게 작동하는지 살펴보겠습니다.

# 텐서란?

텐서는 벡터의 일반화입니다. 벡터는 종종 1차원 숫자 배열로 생각되지만 텐서는 모든 차원의 배열로 생각할 수 있습니다. 벡터를 더하고 스칼라를 곱할 수 있는 것처럼 텐서도 가능합니다.

Tensor는 다양한 방식으로 데이터를 나타내는 데 사용할 수 있기 때문에 기계 학습에 자주 사용됩니다. 예를 들어 이미지는 이미지의 높이, 너비 및 깊이가 3차원인 3차원 텐서로 나타낼 수 있습니다.

# TensorFlow.js

TensorFlow.js는 다양한 방식으로 텐서를 사용할 수 있게 해주는 기계 학습용 JavaScript 라이브러리입니다. 이 게시물에서는 TensorFlow.js에서 텐서를 사용할 수 있는 몇 가지 방법을 살펴보겠습니다.

# 텐서 생성

Tensor는 tf.tensor 함수를 사용하여 JavaScript 배열에서 만들 수 있습니다. 예를 들어, 다음 코드는 값이 1, 2, 3, 4인 2차원 텐서를 생성합니다.

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
```

tf.ones, tf.zeros 및 tf.fill 함수를 사용하여 특정 값으로 텐서를 생성할 수도 있습니다. 예를 들어, 다음 코드는 값이 1, 0, 1, 0인 2차원 텐서를 생성합니다.

```javascript
const t = tf.ones([2, 2]);
```

# 텐서 조작

텐서는 다양한 방법으로 조작할 수 있습니다. 텐서를 조작하는 가장 일반적인 방법은 tf.transpose 함수를 사용하는 것입니다. 이 함수는 텐서의 차원을 치환합니다. 예를 들어 다음 코드는 값이 1, 2, 3, 4인 2차원 텐서를 만든 다음 차원을 치환하여 값이 1, 3, 2, 4인 새 텐서를 만듭니다.

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.transpose();
```

텐서는 tf.reshape 함수를 사용하여 재구성할 수도 있습니다. 이 함수는 원래 텐서와 값은 같지만 모양이 다른 새 텐서를 반환합니다. 예를 들어 다음 코드는 값이 1, 2, 3, 4인 2차원 텐서를 만든 다음 값이 1, 2, 3, 4인 1차원 텐서로 모양을 변경합니다.

```javascript
const t = tf.tensor([[1, 2], [3, 4]]);
const t2 = t.reshape([4]);
```

# TensorFlow.js에서 Tensor로 작업하기

TensorFlow.js는 텐서 작업을 위한 다양한 기능을 제공합니다. 이 섹션에서는 가장 일반적으로 사용되는 몇 가지 기능을 살펴보겠습니다.

tf.tensor 함수는 JavaScript 배열에서 텐서를 생성하는 데 사용할 수 있습니다. tf.ones 및 tf.zeros 함수는 각각 모두 1 또는 모두 0인 텐서를 생성하는 데 사용할 수 있습니다. tf.fill 함수는 주어진 값으로 텐서를 생성하는 데 사용할 수 있습니다.

tf.transpose 함수는 텐서의 차원을 치환하는 데 사용할 수 있습니다. tf.reshape 함수는 텐서를 재구성하는 데 사용할 수 있습니다.

tf.concat 함수는 주어진 차원을 따라 두 개 이상의 텐서를 연결하는 데 사용할 수 있습니다. tf.split 함수는 주어진 차원을 따라 텐서를 분할하는 데 사용할 수 있습니다.

tf.add, tf.sub, tf.mul 및 tf.div 함수는 각각 두 개의 텐서에서 요소별 덧셈, 뺄셈, 곱셈 및 나눗셈을 수행하는 데 사용할 수 있습니다.

tf.matMul 함수는 두 개의 2차원 텐서에서 행렬 곱셈을 수행하는 데 사용할 수 있습니다.

tf.sum 함수는 텐서의 모든 요소의 합을 계산하는 데 사용할 수 있습니다. tf.mean 함수는 텐서에 있는 모든 요소의 평균을 계산하는 데 사용할 수 있습니다.

# 결론

이 게시물에서는 TensorFlow.js에서 Tensor가 무엇인지, TensorFlow.js에서 어떻게 작동하는지 살펴보았습니다. 우리는 텐서를 생성하는 방법과 이를 조작하는 방법을 살펴보았습니다. 또한 다양한 기능을 사용하여 TensorFlow.js에서 텐서로 작업하는 방법도 살펴보았습니다.