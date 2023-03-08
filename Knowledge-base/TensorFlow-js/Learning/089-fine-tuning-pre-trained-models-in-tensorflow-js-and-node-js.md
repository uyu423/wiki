---
title: 089: TensorFlow.js 및 Node.js에서 사전 학습된 모델 미세 조정
description: 
published: true
date: 2023-02-03T03:44:04.110Z
tags: 
editor: markdown
dateCreated: 2023-02-03T03:43:59.387Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [089: Fine-Tuning Pre-Trained Models in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/089-fine-tuning-pre-trained-models-in-tensorflow-js-and-node-js)
{.links-list}


# 089: TensorFlow.js 및 Node.js에서 사전 학습된 모델 미세 조정

TensorFlow.js는 브라우저에서 기계 학습 모델을 훈련하고 배포할 수 있게 해주는 강력한 도구입니다. 이 게시물에서는 TensorFlow.js 및 Node.js에서 사전 훈련된 모델을 미세 조정하는 방법을 알아봅니다.

## 선행 학습된 모델이란 무엇인가요?

사전 훈련된 모델은 대규모 데이터 세트에서 훈련된 기계 학습 모델입니다. 이러한 모델은 이미지 분류, 개체 감지 및 텍스트 분류와 같은 작업을 수행하는 데 사용할 수 있습니다.

## 선행 학습된 모델을 미세 조정하는 이유는 무엇입니까?

사전 훈련된 모델을 미세 조정하는 것은 기계 학습의 일반적인 기술입니다. 이를 통해 사전 훈련된 모델을 자체 데이터 세트에 적용할 수 있습니다. 이는 데이터 세트가 작거나 데이터 세트에서 사전 훈련된 모델의 성능을 개선하려는 경우에 유용할 수 있습니다.

## 선행 학습된 모델을 미세 조정하는 방법은 무엇입니까?

사전 훈련된 모델을 미세 조정하는 두 가지 일반적인 방법이 있습니다.

1. **전이 학습**: 사전 훈련된 모델을 시작점으로 사용한 다음 자체 데이터 세트에서 훈련할 수 있습니다. 이것은 데이터 세트가 작을 때 일반적인 기술입니다.

2. **미세 조정**: 사전 훈련된 모델을 사용한 다음 자체 데이터 세트에서 미세 조정할 수 있습니다. 이것은 데이터 세트에서 사전 훈련된 모델의 성능을 향상시키려는 일반적인 기술입니다.

이 게시물에서는 사전 훈련된 모델을 미세 조정하는 데 중점을 둘 것입니다.

## TensorFlow.js에서 선행 학습된 모델 미세 조정

TensorFlow.js는 선행 학습된 모델을 미세 조정하기 위한 고급 API를 제공합니다. 미리 훈련된 모델을 미세 조정하기 위해 `tf.fineTuneModel()` 함수를 사용할 것입니다.

먼저 사전 학습된 모델을 로드해야 합니다. URL에서 사전 훈련된 모델을 로드하기 위해 `tf.loadLayersModel()` 함수를 사용할 것입니다.

다음으로 모델의 입력과 출력을 정의해야 합니다. `tf.input()` 및 `tf.output()` 함수를 사용하여 모델의 입력 및 출력을 정의합니다.

마지막으로 사전 훈련된 모델을 미세 조정하기 위해 `tf.fineTuneModel()` 함수를 호출해야 합니다. 옵티마이저, 손실 및 메트릭을 지정해야 합니다.

다음은 TensorFlow.js에서 선행 학습된 모델을 미세 조정하는 방법의 예입니다.

```javascript
// Load a pre-trained model
const model = tf.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## Node.js에서 선행 학습된 모델 미세 조정

TensorFlow.js는 선행 학습된 모델을 미세 조정하기 위한 Node.js API를 제공합니다. 미리 훈련된 모델을 미세 조정하기 위해 `tf.node.fineTuneModel()` 함수를 사용할 것입니다.

먼저 사전 학습된 모델을 로드해야 합니다. URL에서 미리 훈련된 모델을 로드하기 위해 `tf.node.loadLayersModel()` 함수를 사용할 것입니다.

다음으로 모델의 입력과 출력을 정의해야 합니다. `tf.node.input()` 및 `tf.node.output()` 함수를 사용하여 모델의 입력 및 출력을 정의합니다.

마지막으로 사전 훈련된 모델을 미세 조정하기 위해 `tf.node.fineTuneModel()` 함수를 호출해야 합니다. 옵티마이저, 손실 및 메트릭을 지정해야 합니다.

다음은 Node.js에서 선행 학습된 모델을 미세 조정하는 방법의 예입니다.

```javascript
// Load a pre-trained model
const model = tf.node.loadLayersModel('https://model-url');

// Define the inputs and outputs of the model
const input = tf.node.input({shape: [28, 28, 1]});
const output = model.outputs[0];

// Fine-tune the model
const model = tf.node.fineTuneModel(
    model,
    {
      optimizer: tf.train.adam(0.001),
      loss: tf.losses.softmaxCrossEntropy,
      metrics: ['accuracy']
    },
    {
      // We will use a validation split of 0.1
      validationSplit: 0.1
    }
);
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 사전 훈련된 모델을 미세 조정하는 방법을 배웠습니다. 우리는 TensorFlow.js가 사전 훈련된 모델을 미세 조정하기 위한 높은 수준의 API를 제공한다는 것을 확인했습니다. 우리는 또한 TensorFlow.js가 사전 훈련된 모델을 미세 조정하기 위한 Node.js API를 제공한다는 것을 확인했습니다.