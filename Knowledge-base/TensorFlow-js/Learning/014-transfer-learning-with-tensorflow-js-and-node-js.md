---
title: 014: TensorFlow.js 및 Node.js를 사용한 전이 학습
description: 
published: true
date: 2023-02-02T10:04:41.398Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:04:39.809Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [014: Transfer Learning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/014-transfer-learning-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js로 전이 학습을 사용하는 방법을 살펴보겠습니다. 전이 학습은 자체 기계 학습 모델에 대한 학습 프로세스를 가속화하는 데 도움이 되는 강력한 기술입니다. 사전 훈련된 모델로 시작하면 모델을 처음부터 훈련하는 데 소요되는 많은 시간과 노력을 절약할 수 있습니다.

이 게시물에서는 다음 주제를 다룹니다.

- 전이학습이란?
- TensorFlow.js로 전이 학습을 사용하는 방법
- Node.js로 전이 학습을 사용하는 방법

# 전이학습이란?

전이 학습은 사전 학습된 모델을 새 데이터 세트에서 재사용할 수 있게 해주는 기계 학습 기술입니다. 이는 모델을 처음부터 훈련하기에 충분한 데이터가 없을 때 특히 유용합니다.

전이 학습에는 두 가지 주요 유형이 있습니다.

- **미세 조정:** 사전 훈련된 모델을 가져온 다음 자체 데이터 세트에서 훈련시키는 곳입니다. 이것은 일반적으로 데이터 세트가 사전 훈련된 모델을 교육하는 데 사용된 것과 유사할 때 사용됩니다.
- **기능 추출:** 사전 훈련된 모델을 사용하여 자체 데이터 세트에서 기능을 추출하는 곳입니다. 이것은 일반적으로 데이터 세트가 사전 학습된 모델을 교육하는 데 사용된 데이터 세트와 다른 경우에 사용됩니다.

# TensorFlow.js로 전이 학습을 사용하는 방법

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 사전 훈련된 모델 세트를 제공하여 TensorFlow.js 모델과 함께 전이 학습을 사용할 수 있습니다.

사전 훈련된 모델은 대규모 데이터 세트에서 훈련된 후 다른 사람들이 사용할 수 있도록 만들어진 모델입니다. 이러한 모델을 자신의 모델 학습을 위한 시작점으로 사용할 수 있습니다.

TensorFlow.js에서 선행 학습된 모델을 사용하려면 먼저 TensorFlow.js 라이브러리를 설치해야 합니다. 다음 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js 라이브러리가 설치되면 `loadModel()` 함수를 사용하여 선행 학습된 모델을 로드할 수 있습니다. 예를 들어 MobileNet 사전 학습 모델을 로드하려면 다음 코드를 사용합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

모델이 로드되면 이를 전이 학습에 사용할 수 있습니다. 예를 들어 이를 사용하여 자신의 데이터 세트에서 모델을 미세 조정할 수 있습니다.

# Node.js에서 전이 학습을 사용하는 방법

Node.js는 JavaScript를 사용하여 확장 가능한 네트워크 애플리케이션을 구축할 수 있게 해주는 JavaScript 런타임입니다.

TensorFlow.js와 함께 Node.js를 사용하여 전이 학습을 사용하는 애플리케이션을 빌드할 수 있습니다. TensorFlow.js와 함께 Node.js를 사용하려면 먼저 TensorFlow.js 라이브러리를 설치해야 합니다. 다음 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js 라이브러리가 설치되면 `loadModel()` 함수를 사용하여 선행 학습된 모델을 로드할 수 있습니다. 예를 들어 MobileNet 사전 학습 모델을 로드하려면 다음 코드를 사용합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

모델이 로드되면 이를 전이 학습에 사용할 수 있습니다. 예를 들어 이를 사용하여 자신의 데이터 세트에서 모델을 미세 조정할 수 있습니다.

# 결론

이번 포스트에서는 TensorFlow.js와 Node.js로 전이 학습을 사용하는 방법을 살펴보았습니다. 전이 학습은 자체 기계 학습 모델에 대한 학습 프로세스를 가속화하는 데 도움이 되는 강력한 기술입니다. 사전 훈련된 모델로 시작하면 모델을 처음부터 훈련하는 데 소요되는 많은 시간과 노력을 절약할 수 있습니다.