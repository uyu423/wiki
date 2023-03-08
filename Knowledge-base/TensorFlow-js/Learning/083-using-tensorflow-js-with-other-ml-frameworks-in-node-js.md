---
title: 083: TensorFlow.js를 Node.js의 다른 ML 프레임워크와 함께 사용
description: 
published: true
date: 2023-02-03T02:17:27.311Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:17:25.696Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [083: Using TensorFlow.js with Other ML Frameworks in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/083-using-tensorflow-js-with-other-ml-frameworks-in-node-js)
{.links-list}


# Node.js의 다른 ML 프레임워크와 함께 TensorFlow.js 사용

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 강력한 JavaScript 라이브러리입니다. TensorFlow Lite와 같은 다른 ML 프레임워크와 함께 사용하여 Node.js에서 추론을 실행할 수 있습니다.

이 게시물에서는 TensorFlow.js를 Node.js의 다른 ML 프레임워크와 함께 사용하는 방법을 보여줍니다. TensorFlow.js를 최대한 활용하는 방법에 대한 몇 가지 팁도 제공합니다.

## TensorFlow Lite와 함께 TensorFlow.js 사용

TensorFlow.js는 TensorFlow Lite와 함께 사용하여 Node.js에서 추론을 실행할 수 있습니다. TensorFlow Lite는 휴대기기에서 기계 학습 모델을 실행하기 위한 경량 프레임워크입니다.

TensorFlow Lite와 함께 TensorFlow.js를 사용하려면 TensorFlow Lite Node.js 바인딩을 설치해야 합니다. npm으로 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

바인딩이 설치되면 `tensorflow.js` 모듈을 사용하여 TensorFlow Lite 모델을 로드하고 추론을 실행할 수 있습니다.

다음은 TensorFlow Lite와 함께 TensorFlow.js를 사용하는 방법의 예입니다.

```javascript
const tf = require('@tensorflow/tfjs-node');

// Load a TensorFlow Lite model.
const model = await tf.loadLiteModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a TensorFlow Lite model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## TensorFlow.js를 다른 ML 프레임워크와 함께 사용

TensorFlow.js는 Keras와 같은 다른 ML 프레임워크와 함께 사용하여 Node.js에서 추론을 실행할 수도 있습니다.

Keras와 함께 TensorFlow.js를 사용하려면 TensorFlow.js Node.js 바인딩을 설치해야 합니다. npm으로 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

바인딩이 설치되면 `tf` 모듈을 사용하여 Keras 모델을 로드하고 추론을 실행할 수 있습니다.

다음은 Keras와 함께 TensorFlow.js를 사용하는 방법의 예입니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load a Keras model.
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_1.0_224/model.json');

// Run inference on a Keras model.
const output = model.predict(tf.zeros([1, 224, 224, 3]));

// Print the output of the model.
console.log(output);
```

## TensorFlow.js 사용 팁

다음은 TensorFlow.js 사용에 대한 몇 가지 팁입니다.

- TensorFlow.js가 처음이라면 [TensorFlow.js 시작하기 가이드](https://js.tensorflow.org/tutorials/getting-started.html)부터 시작하는 것이 좋습니다.
- TensorFlow.js를 다른 ML 프레임워크와 함께 사용하는 경우 [TensorFlow.js Node.js 바인딩](https://www.npmjs.com/package/@tensorflow/tfjs)을 사용하는 것이 좋습니다.
- TensorFlow Lite와 함께 TensorFlow.js를 사용하는 경우 [TensorFlow Lite Node.js 바인딩](https://www.npmjs.com/package/@tensorflow/tfjs-node)을 사용하는 것이 좋습니다.
- 웹 브라우저에서 TensorFlow.js를 사용하는 경우 [WebAssembly 기반 백엔드](https://js.tensorflow.org/api/0.12.0/# enabling-webassembly-support)를 사용하는 것이 좋습니다.