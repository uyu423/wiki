---
title: 036: TensorFlow.js 및 Node.js로 사전 학습된 모델 사용
description: 
published: true
date: 2023-02-02T15:36:43.990Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:36:42.352Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [036: Using Pretrained Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/036-using-pretrained-models-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js와 함께 사전 학습된 모델을 사용하는 방법을 알아봅니다. 미리 훈련된 모델이 무엇이고 왜 유용한지에 대해 논의하는 것으로 시작하겠습니다. 그런 다음 TensorFlow.js에서 사전 훈련된 모델을 로드하고 사용하는 방법을 살펴보겠습니다. 마지막으로 Node.js로 사전 학습된 모델을 배포하는 방법을 살펴보겠습니다.

# 사전 훈련된 모델이란 무엇입니까?

사전 훈련된 모델은 대규모 데이터 세트에서 훈련된 모델입니다. 이러한 모델은 이미지 분류, 개체 감지 및 텍스트 분류와 같은 다양한 작업을 수행하는 데 사용할 수 있습니다.

사전 훈련된 모델은 자체 모델을 처음부터 훈련하지 않고도 대규모 데이터 세트의 지식을 사용할 수 있기 때문에 유용합니다. 이렇게 하면 많은 시간과 노력을 절약할 수 있습니다.

# 사전 훈련된 모델 불러오기

TensorFlow.js는 자체 애플리케이션에서 로드하고 사용할 수 있는 여러 가지 사전 훈련된 모델을 제공합니다. 선행 학습된 모델을 로드하려면 먼저 TensorFlow.js를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js가 설치되면 tf.loadModel() 함수를 사용하여 사전 훈련된 모델을 로드할 수 있습니다. 예를 들어 MobileNet 모델을 로드하려면 다음 코드를 사용합니다.

```javascript
const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

# 사전 훈련된 모델 사용

미리 학습된 모델을 로드하면 이를 사용하여 다양한 작업을 수행할 수 있습니다. 예를 들어 사전 학습된 이미지 분류 모델을 사용하는 경우 모델을 사용하여 이미지를 분류할 수 있습니다.

사전 훈련된 모델을 사용하려면 먼저 모델의 입력 및 출력 계층을 가져와야 합니다. model.inputs 및 model.outputs 속성을 사용하여 이를 수행할 수 있습니다. 예를 들어 MobileNet 모델의 입력 및 출력 계층을 가져오려면 다음 코드를 사용합니다.

```javascript
const inputLayer = model.inputs[0];
const outputLayer = model.outputs[0];
```

모델의 입력 및 출력 레이어가 있으면 tf.tidy() 함수를 사용하여 추론을 실행할 수 있습니다. tf.tidy() 함수는 추론 프로세스 중에 생성된 anytf.js Tensor를 정리합니다. 이것은 tf.js Tensor가 많은 메모리를 차지할 수 있기 때문에 중요합니다.

tf.tidy() 함수를 사용하려면 추론을 실행하기 위한 코드가 포함된 함수를 전달해야 합니다. 이 함수는 깔끔한 컨텍스트 내에서 실행됩니다. 예를 들어 MobileNet 모델에서 추론을 실행하려면 다음 코드를 사용합니다.

```javascript
const results = tf.tidy(() => {
  // inputLayer is a tf.js Tensor with shape [1, 224, 224, 3]
  // outputLayer is a tf.js Tensor with shape [1, 1000]
  const output = model.predict(inputLayer);
  return output.dataSync();
});
```

# 사전 학습된 모델 배포

모델을 교육한 후에는 다른 애플리케이션에서 사용할 수 있도록 모델을 배포해야 합니다. TensorFlow.js는 사전 훈련된 모델을 배포하는 다양한 방법을 제공합니다.

사전 훈련된 모델을 배포하는 한 가지 방법은 tf.model.save() 함수를 사용하는 것입니다. 이 기능은 모델을 JSON 파일에 저장합니다. 예를 들어 MobileNet 모델을 저장하려면 다음 코드를 사용합니다.

```javascript
await model.save('file:///model');
```

그런 다음 tf.loadModel() 함수를 사용하여 JSON 파일에서 모델을 로드할 수 있습니다.

사전 훈련된 모델을 배포하는 또 다른 방법은 tf.model.toJSON() 함수를 사용하는 것입니다. 이 함수는 모델을 JSON 객체로 반환합니다. 예를 들어 MobileNet 모델을 JSON 개체로 가져오려면 다음 코드를 사용합니다.

```javascript
const modelAsJSON = model.toJSON();
```

그런 다음 JSON 객체를 파일이나 데이터베이스에 저장할 수 있습니다.

# 결론

이 게시물에서는 TensorFlow.js 및 Node.js에서 사전 훈련된 모델을 사용하는 방법을 배웠습니다. 사전 훈련된 모델을 로드하고 사용하는 방법과 사전 훈련된 모델을 배포하는 방법을 살펴보았습니다.