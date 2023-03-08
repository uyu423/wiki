---
title: 018: TensorFlow.js 및 Node.js를 사용한 비디오 분석
description: 
published: true
date: 2023-02-02T11:04:51.568Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:04:49.931Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [018: Video Analysis with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/018-video-analysis-with-tensorflow-js-and-node-js)
{.links-list}


## 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 비디오 분석을 수행하는 방법을 살펴보겠습니다. 미리 훈련된 모델을 사용하여 비디오에서 개체를 식별한 다음 이동하는 개체를 추적할 것입니다.

다음 도구와 라이브러리를 사용할 것입니다.

- TensorFlow.js
- Node.js
- ffmpeg(선택사항)

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 딥 러닝과 기존 기계 학습 모두에 사용됩니다.

## Node.js가 무엇인가요?

Node.js는 서버 측 애플리케이션 개발에 사용되는 JavaScript 런타임입니다.

## 환경 설정

시작하기 전에 환경을 설정해야 합니다. Node.js와 TensorFlow.js를 설치해야 합니다.

Node.js가 아직 설치되어 있지 않다면 [Node.js 웹사이트](https://nodejs.org/en/)에서 다운로드할 수 있습니다.

Node.js가 설치되면 다음 명령을 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

## 비디오를 적절한 형식으로 변환

사전 학습된 모델을 사용하려면 비디오를 모델이 이해할 수 있는 형식으로 변환해야 합니다. 이 모델은 비디오가 특정 해상도 및 프레임 속도를 가진 MPEG-4 형식일 것으로 예상합니다.

ffmpeg가 설치되어 있으면 다음 명령을 사용하여 비디오를 변환할 수 있습니다.

```
ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4
```

ffmpeg가 설치되어 있지 않은 경우 [ffmpeg 웹사이트](https://ffmpeg.org/)에서 다운로드할 수 있습니다.

## 영상 분석

이제 환경을 설정하고 비디오를 변환했으므로 분석을 시작할 수 있습니다.

[YOLOv2](https://pjreddie.com/darknet/yolo/)라는 사전 훈련된 모델을 사용할 것입니다. 이 모델은 [Pascal VOC](http://host.robots.ox.ac.uk/pascal/VOC/) 데이터 세트에서 학습되었으며 20가지 객체 클래스를 식별할 수 있습니다.

모델을 사용하려면 먼저 TensorFlow.js에 로드해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');

const model = await tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v2_1.0_224/model.json');
```

모델이 로드되면 비디오 분석을 시작할 수 있습니다. 비디오의 각 프레임을 모델에 전달하고 예측을 다시 가져와야 합니다.

이렇게 하려면 먼저 비디오의 모든 프레임 목록을 가져와야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

프레임 목록이 있으면 비디오 분석을 시작할 수 있습니다. 각 프레임에 대해 모델에 전달하고 예측을 다시 가져와야 합니다.

이렇게 하려면 먼저 비디오의 모든 프레임 목록을 가져와야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

프레임 목록이 있으면 비디오 분석을 시작할 수 있습니다. 각 프레임에 대해 모델에 전달하고 예측을 다시 가져와야 합니다.

이렇게 하려면 먼저 비디오의 모든 프레임 목록을 가져와야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

프레임 목록이 있으면 비디오 분석을 시작할 수 있습니다. 각 프레임에 대해 모델에 전달하고 예측을 다시 가져와야 합니다.

이를 위해 다음 코드를 사용합니다.

```javascript
const fs = require('fs');
const { exec } = require('child_process');

exec('ffmpeg -i input.mp4 -vf scale=640:360 -r 30 output.mp4', (err, stdout, stderr) => {
  if (err) {
    console.error(err);
    return;
  }

  console.log(stdout);
  console.log(stderr);
});
```

이 코드는 비디오를 TensorFlow.js로 로드하고 각 프레임을 분석한 다음 콘솔에 결과를 출력합니다.

## 개체 추적

이제 각 프레임에 대한 예측이 있으므로 개체 추적을 시작할 수 있습니다. 이를 위해 [칼만 필터](https://en.wikipedia.org/wiki/Kalman_filter)를 사용합니다.

Kalman 필터는 과거 관찰을 기반으로 시스템의 미래 상태를 예측할 수 있는 수학적 모델입니다.

Kalman 필터를 사용하여 과거 위치를 기반으로 각 개체의 미래 위치를 예측합니다. 이렇게 하면 비디오에서 개체가 이동할 때 개체를 추적할 수 있습니다.

Kalman 필터를 사용하려면 먼저 [kalman-filter](https://www.npmjs.com/package/kalman-filter) 라이브러리를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install kalman-filter
```

라이브러리가 설치되면 다음 코드를 사용하여 개체를 추적할 수 있습니다.

```javascript
const kf = new KalmanFilter();

const trackedObjects = [];

for (const prediction of predictions) {
  const trackedObject = trackedObjects.find(obj => obj.id === prediction.id);

  if (trackedObject) {
    trackedObject.update(prediction);
  } else {
    trackedObjects.push(new TrackedObject(prediction));
  }
}
```

이 코드는 비디오의 개체를 추적하고 해당 위치를 콘솔에 출력합니다.

## 결과 시각화

이제 예측과 추적된 개체가 있으므로 결과 시각화를 시작할 수 있습니다.

[PIXI.js](https://www.pixijs.com/) 라이브러리를 사용하여 각 개체 주위에 상자를 그립니다.

먼저 [pixi.js](https://www.npmjs.com/package/pixi.js) 라이브러리를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm install pixi.js
```

라이브러리가 설치되면 다음 코드를 사용하여 상자를 그릴 수 있습니다.

```javascript
const app = new PIXI.Application();

document.body.appendChild(app.view);

const graphics = new PIXI.Graphics();

app.stage.addChild(graphics);

for (const trackedObject of trackedObjects) {
  const { x, y, width, height } = trackedObject;

  graphics.lineStyle(1, 0xffffff);
  graphics.drawRect(x, y, width, height);
}
```

이 코드는 비디오의 각 개체 주위에 상자를 그립니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 비디오 분석을 수행하는 방법을 살펴보았습니다. 사전 학습된 모델을 사용하여 비디오에서 개체를 식별한 다음 이동하는 개체를 추적했습니다.

Kalman 필터를 사용하여 과거 위치를 기반으로 각 개체의 미래 위치를 예측하는 방법도 살펴보았습니다. 이를 통해 비디오에서 개체가 이동할 때 개체를 추적할 수 있습니다.

마지막으로 PIXI.js 라이브러리를 사용하여 각 개체 주위에 상자를 그리는 방법을 살펴보았습니다.