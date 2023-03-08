---
title: 052: TensorFlow.js 및 Node.js를 사용한 커스텀 콜백
description: 
published: true
date: 2023-02-02T19:04:49.008Z
tags: 
editor: markdown
dateCreated: 2023-02-02T19:04:47.422Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [052: Custom Callbacks with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/052-custom-callbacks-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 커스텀 콜백

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 사용자 지정 콜백을 만드는 방법을 알아봅니다.

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. 이를 통해 브라우저 또는 Node.js에서 기계 학습 모델을 생성, 교육 및 배포할 수 있습니다.

Node.js는 서버에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다. Node.js는 TensorFlow.js의 중요한 플랫폼이기도 합니다. 기계 학습 모델을 프로덕션에 배포할 수 있기 때문입니다.

TensorFlow.js로 맞춤 콜백을 만드는 것은 기계 학습 모델의 기능을 확장하는 좋은 방법입니다. 콜백을 사용하면 교육 프로세스 중 특정 지점에서 실행되는 사용자 지정 함수를 정의할 수 있습니다. 예를 들어 콜백을 사용하여 교육 손실을 추적하거나 각 에포크 후 모델을 저장할 수 있습니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 사용자 지정 콜백을 만드는 방법을 알아봅니다. 또한 콜백을 사용하여 교육 손실을 추적하고 각 에포크 후에 모델을 저장하는 방법을 배웁니다.

## 콜백이란?

콜백은 학습 과정 중 특정 시점에서 실행되는 함수입니다. 콜백은 기계 학습 모델의 기능을 확장하는 강력한 방법입니다.

TensorFlow.js에는 두 가지 유형의 콜백이 있습니다.

* **레이어 콜백:** 이 콜백은 레이어가 생성될 때 실행됩니다.
* **모델 콜백:** 이러한 콜백은 모델이 컴파일되고 훈련이 시작될 때 실행됩니다.

이 게시물에서는 모델 콜백에 중점을 둘 것입니다.

## 커스텀 콜백 만들기

TensorFlow.js로 맞춤 콜백을 만드는 것은 간단합니다. 먼저 새 JavaScript 파일을 만들고 TensorFlow.js 라이브러리를 가져와야 합니다.

다음으로 Callback 클래스를 확장하는 새 클래스를 만들어야 합니다. 이 클래스에는 사용자 지정 콜백 함수가 포함됩니다.

이 예제에서는 교육 손실을 추적하고 각 에포크 후에 모델을 저장하는 사용자 지정 콜백을 생성합니다.

```javascript
const tf = require('@tensorflow/tfjs');

class CustomCallback extends tf.Callback {
  onTrainBegin(logs) {
    // This function is executed when training begins.
    // We can use it to initialize our custom variables.
    this.losses = [];
  }

  onTrainEnd(logs) {
    // This function is executed when training ends.
    // We can use it to save our custom variables.
    console.log('Final loss: ', this.losses[-1]);
  }

  onBatchEnd(batch, logs) {
    // This function is executed at the end of each training batch.
    // We can use it to track the training loss.
    this.losses.push(logs.loss);
  }

  onEpochEnd(epoch, logs) {
    // This function is executed at the end of each training epoch.
    // We can use it to save the model.
    console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
    this.model.save(`model_at_epoch_${epoch}.h5`);
  }
}
```

이 예에서는 네 가지 사용자 지정 콜백 함수를 만들었습니다.

* onTrainBegin: 학습이 시작되면 실행되는 함수입니다. 이를 사용하여 사용자 지정 변수를 초기화할 수 있습니다.
* onTrainEnd: 학습 종료 시 실행되는 함수입니다. 이를 사용하여 사용자 지정 변수를 저장할 수 있습니다.
* onBatchEnd: 이 함수는 각 훈련 배치가 끝날 때 실행됩니다. 훈련 손실을 추적하는 데 사용할 수 있습니다.
* onEpochEnd: 이 함수는 각 학습 에포크가 끝날 때 실행됩니다. 모델을 저장하는 데 사용할 수 있습니다.

## 커스텀 콜백 사용하기

이제 사용자 지정 콜백을 만들었으므로 사용 방법을 살펴보겠습니다.

먼저 새로운 TensorFlow.js 모델을 생성해야 합니다. 이 예에서는 간단한 순차 모델을 사용합니다.

다음으로 커스텀 콜백을 사용하여 모델을 컴파일해야 합니다.

마지막으로 fit 방법을 사용하여 모델을 훈련할 수 있습니다.

```javascript
const model = tf.sequential();

model.compile({
  optimizer: 'sgd',
  loss: 'binaryCrossentropy',
  callbacks: new CustomCallback()
});

model.fit(x, y, {
  epochs: 10
});
```

이 예에서는 맞춤 콜백을 사용하여 교육 손실을 추적하고 각 에포크 후 모델을 저장했습니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 사용자 지정 콜백을 만드는 방법을 배웠습니다. 또한 콜백을 사용하여 교육 손실을 추적하고 각 에포크 후에 모델을 저장하는 방법도 배웠습니다.

사용자 지정 콜백을 만드는 것은 기계 학습 모델의 기능을 확장하는 좋은 방법입니다. 콜백을 사용하면 교육 프로세스 중 특정 지점에서 실행되는 사용자 지정 함수를 정의할 수 있습니다.

TensorFlow.js에 대해 자세히 알아보려면 TensorFlow.js 웹사이트(https://js.tensorflow.org/)를 확인하세요.