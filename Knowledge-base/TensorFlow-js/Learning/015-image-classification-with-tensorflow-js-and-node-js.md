---
title: 015: TensorFlow.js 및 Node.js를 사용한 이미지 분류
description: 
published: true
date: 2023-02-02T10:17:57.503Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:17:55.929Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [015: Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/015-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이미지 분류 모델을 빌드하는 방법을 살펴보겠습니다. 대규모 이미지 데이터 세트에서 훈련된 사전 훈련된 모델인 MobileNet 모델을 사용할 것입니다.

다음 라이브러리를 사용할 것입니다.

* [TensorFlow.js](https://js.tensorflow.org/)
* [ Node.js](https://nodejs.org/en/)

## 전제 조건

시작하기 전에 설정해야 할 몇 가지 사항이 있습니다.

* 텍스트 편집기. [Visual Studio Code](https://code.visualstudio.com/)를 추천합니다.
* [Node.js](https://nodejs.org/en/). 이것은 코드를 실행하는 데 사용됩니다.
* [TensorFlow.js](https://js.tensorflow.org/). 기계 학습을 위한 JavaScript 라이브러리입니다.

## 시작하기

1. 프로젝트를 위한 새 디렉터리를 만듭니다.

2. 프로젝트 디렉터리에 `index.js`라는 파일을 만듭니다.

3. 다음 코드를 `index.js`에 복사합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load the MobileNet model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');

// Make a prediction through the model on our image.
const imgEl = document.getElementById('img');
model.predict(tf.fromPixels(imgEl)).then(predictions => {
  console.log('Predictions: ');
  console.log(predictions);
});
```

4. 프로젝트 디렉토리에 `index.html`이라는 파일을 만듭니다.

5. 다음 코드를 `index.html`에 복사합니다.

```html
<html>
  <body>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.11.3"> </script>
    <script src="index.js"></script>
    <img id="img" src="https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/test_images/grace_hopper.jpg">
  </body>
</html>
```

6. 다음 명령을 실행하여 서버를 시작합니다.

```
node index.js
```

다음 출력이 표시되어야 합니다.

```
Predictions:
[
  {
    className: 'daisy',
    probability: 0.9911273956298828
  },
  {
    className: 'tulip',
    probability: 0.008872604370117188
  },
  {
    className: 'sunflower',
    probability: 0.0001983642578125
  },
  {
    className: 'dandelion',
    probability: 0.0000457763671875
  },
  {
    className: 'roses',
    probability: 0.0000095367431640625
  }
]
```

## 무슨 일이야?

위의 코드에서 우리는 MobileNet 모델을 사용하여 이미지를 분류하고 있습니다. MobileNet은 대규모 이미지 데이터 세트에 대해 훈련된 사전 훈련된 모델입니다.

`predict` 메서드를 실행하면 TensorFlow.js는 각각 `className`과 `probability`가 포함된 예측 배열을 반환합니다. 'className'은 모델이 이미지가 속한 것으로 예측하는 클래스의 이름이고, 'probability'는 해당 예측에서 모델이 갖는 신뢰도입니다.

## 웹캠으로 예측하기

위의 예에서는 미리 학습된 모델을 사용하여 이미지를 예측합니다. 하지만 라이브 웹캠 피드에서 예측을 하고 싶다면 어떻게 해야 할까요?

이렇게 하려면 `tf.data` 및 `tf.layers` API를 사용해야 합니다.

먼저 ` webcam ` 개체를 만듭니다. 라이브 웹캠 피드를 캡처하는 데 사용됩니다.

```javascript
const webcam = new tf.data.webcam(document.getElementById('webcam'));
```

다음으로 ` convolutional ` 계층을 만듭니다. 이 레이어는 라이브 웹캠 피드를 처리하는 데 사용됩니다.

```javascript
const layer = tf.layers.conv2d({
  kernelSize: 5,
  filters: 20,
  strides: 1,
  activation: 'relu',
  kernelInitializer: 'varianceScaling',
  inputShape: [28, 28, 1]
});
```

이제 라이브 웹캠 피드를 예측하는 데 사용할 ` 함수 `를 만들겠습니다. 이 함수는 이미지를 가져와 ` convolutional ` 레이어를 통해 처리하고 예측을 반환합니다.

```javascript
async function predict(image) {
  // Make a prediction through the model on the image.
  const predictions = await model.predict(image);

  // Return the highest confidence prediction.
  return predictions.as1D().argMax();
}
```

마지막으로 라이브 웹캠 피드에서 지속적으로 예측을 수행하는 ` 루프 `를 만듭니다.

```javascript
while (true) {
  // Get the next image from the webcam.
  const img = await webcam.capture();

  // Get the prediction from our model.
  const prediction = await predict(img);

  // Convert the prediction into a human-readable string.
  const classNames = ['daisy', 'tulip', 'sunflower', 'dandelion', 'roses'];
  const className = classNames[prediction.dataSync()[0]];

  // Display the string on the page.
  document.getElementById('prediction').innerText = className;

  // Dispose the image when we're done.
  img.dispose();

  // Give some breathing room by waiting for the next animation frame to
  // fire before making another prediction.
  await tf.nextFrame();
}
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이미지 분류 모델을 빌드하는 방법을 살펴보았습니다. 또한 모델을 사용하여 라이브 웹캠 피드에 대한 예측을 수행하는 방법도 살펴보았습니다.