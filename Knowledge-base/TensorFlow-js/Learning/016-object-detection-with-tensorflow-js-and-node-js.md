---
title: 016: TensorFlow.js 및 Node.js를 사용한 객체 감지
description: 
published: true
date: 2023-02-02T10:36:34.060Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:36:32.420Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [016: Object Detection with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/016-object-detection-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 객체 감지

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이미지에서 실시간 객체 감지를 수행하는 방법을 알아봅니다.

개발 환경을 설정하는 것으로 시작한 다음 TensorFlow.js 및 종속 항목을 설치합니다. 다음으로 Node.js 스크립트를 작성하여 이미지를 로드하고 객체 감지를 실행하고 결과를 화면에 그립니다. 마지막으로 추가 학습에 사용할 수 있는 일부 리소스를 살펴보겠습니다.

## 개발 환경 설정

시작하기 전에 개발 환경을 설정해야 합니다. 이 게시물에서는 Node.js를 사용합니다.

Node.js가 아직 설치되어 있지 않다면 [Node.js 웹사이트](https://nodejs.org/en/)에서 다운로드할 수 있습니다. Node.js가 설치되면 새 프로젝트 디렉토리를 만들고 다음 명령으로 초기화할 수 있습니다.

```
mkdir object-detection
cd object-detection
npm init -y
```

## TensorFlow.js 및 종속 항목 설치

이제 프로젝트 디렉토리가 설정되었으므로 TensorFlow.js 및 해당 종속 항목을 설치할 수 있습니다. Node.js에서 사용할 수 있는 TensorFlow.js 구현을 제공하는 [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node) 패키지를 사용할 것입니다.

tfjs-node 및 해당 종속 항목을 설치하려면 다음 명령을 실행합니다.

```
npm install @tensorflow/tfjs-node
```

## 객체 감지 스크립트 작성

TensorFlow.js가 설치되면 이제 이미지에서 객체 감지를 수행하는 스크립트를 작성할 수 있습니다. 먼저 이미지를 로드한 다음 [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) 메서드를 사용하여 객체 감지를 실행합니다. 이미지. 마지막으로 결과를 화면에 그립니다.

전체 스크립트는 [여기](https://github.com/tensorflow/tfjs-models/blob/master/tfjs-models/src/object_detection/index.js)에서 사용할 수 있지만 아래에서 주요 부분을 살펴보겠습니다. .

먼저 tfjs-node 패키지를 로드해야 합니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
```

다음으로 객체 감지에 사용할 [ coco-ssd 모델 ](https://github.com/tensorflow/tfjs-models/tree/master/tfjs-models/detection)을 로드합니다. coco-ssd 모델은 [COCO(Common Objects in Context) 데이터 세트](http://cocodataset.org/# home)에서 훈련된 단일 샷 감지 모델입니다.

```javascript
const cocoSSD = require('@tensorflow-models/coco-ssd');
```

모델이 로드되면 이제 이미지를 로드하고 객체 감지를 실행하는 코드를 작성할 수 있습니다. [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# tf.node.decodeImage) 메서드를 사용하여 이미지를 로드하는 것으로 시작하겠습니다. 이 메서드는 이미지 데이터를 포함하는 텐서로 확인되는 약속을 반환합니다.

```javascript
const image = tf.node.decodeImage(
  fs.readFileSync('./test-image.jpg')
);
```

이미지가 로드되면 [tf.data.detectObjects](https://js.tensorflow.org/api/latest/# tf.data.detectObjects) 메서드를 사용하여 객체 감지를 실행할 수 있습니다. 이 메서드는 개체의 클래스와 이미지 내 위치를 포함하여 감지된 개체에 대한 정보를 포함하는 개체 배열로 확인되는 약속을 반환합니다.

```javascript
const predictions = await cocoSSD.detectObjects(image);
```

마지막으로 결과를 화면에 그립니다. [tf.node.drawBoxes](https://js.tensorflow.org/api/latest/# tf.node.drawBoxes) 메서드를 사용하여 감지된 객체 주위에 상자를 그리고 [tf.node. writeFile](https://js.tensorflow.org/api/latest/#tf.node.writeFile) 메서드를 사용하여 결과를 새 이미지 파일에 씁니다.

```javascript
const drawnImage = tf.node.drawBoxes(
  image,
  predictions.map(prediction => prediction.bbox)
);
tf.node.writeFile('./test-image-output.jpg', drawnImage.toBuffer());
```

## 객체 감지 스크립트 실행

스크립트가 작성되었으므로 이제 이를 실행하여 이미지에서 개체 감지를 수행할 수 있습니다. 스크립트를 실행하려면 다음 명령을 사용하십시오.

```
node index.js
```

이미지 `test-image.jpg`에서 객체 감지 스크립트를 실행하고 결과를 `test-image-output.jpg`에 기록합니다.

## 추가 학습을 위한 리소스

- [TensorFlow.js 객체 감지](https://js.tensorflow.org/tutorials/object-detection.html)
- [TensorFlow.js 및 Node.js를 사용한 실시간 개체 감지](https://www.twilio.com/blog/real-time-object-detection-tensorflow-js-node-js)
- [웹캠을 사용하여 물체 감지](https://codelabs.developers.google.com/codelabs/tensorflowjs-object-detection/index.html)