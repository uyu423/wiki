---
title: 080: TensorFlow.js를 Node.js에서 AR/VR과 통합
description: 
published: true
date: 2023-02-03T01:36:51.296Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:36:49.568Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [080: Integrating TensorFlow.js with AR/VR in Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/080-integrating-tensorflow-js-with-arvr-in-node-js)
{.links-list}


# 080: TensorFlow.js와 Node.js의 AR/VR 통합

TensorFlow.js는 기계 학습 모델을 만들고 브라우저에서 실행할 수 있게 해주는 강력한 도구입니다. 따라서 강력한 서버 없이도 사용자 장치의 처리 능력을 활용할 수 있는 애플리케이션을 만드는 데 이상적입니다.

이 게시물에서는 TensorFlow.js를 사용하여 간단한 증강 현실(AR) 애플리케이션을 만드는 방법을 살펴보겠습니다. Three.js 라이브러리를 사용하여 브라우저에서 3D 개체를 렌더링하고 AR.js 라이브러리를 사용하여 사용자의 머리를 추적하고 올바른 위치에 3D 개체를 표시합니다.

## 프로젝트 설정

새 Node.js 프로젝트를 설정하는 것으로 시작하겠습니다. 프로젝트의 새 디렉터리를 만들고 `npm init`를 실행하여 `package.json` 파일을 만듭니다.

이 프로젝트에는 몇 가지 라이브러리가 필요합니다. `npm` 명령으로 다음 라이브러리를 설치합니다.

* `텐서플로우`
* `@tensorflow/tfjs-node`
* `셋`
* `ar.js`

## 모델 만들기

이제 3D 개체를 생성하는 데 사용할 기계 학습 모델을 만들 수 있습니다. 이 예제에서는 간단한 선형 회귀 모델을 사용합니다.

`model.js`라는 새 파일을 만들고 `@tensorflow/tfjs-node` 라이브러리를 가져옵니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
```

다음으로 모델 학습에 사용할 몇 가지 상수를 정의합니다. 'LEARNING_RATE' 상수는 모델이 얼마나 빨리 학습해야 하는지를 정의합니다. 'BATCH_SIZE' 상수는 모델을 교육할 때 사용할 데이터 포인트 수를 정의합니다. 'EPOCHS' 상수는 모델이 훈련 데이터를 거쳐야 하는 횟수를 정의합니다.

```javascript
const LEARNING_RATE = 0.01;
const BATCH_SIZE = 10;
const EPOCHS = 10;
```

이제 모델을 정의할 수 있습니다. `sequential` 모델을 사용하고 `dense` 레이어를 추가합니다. 'dense' 레이어는 입력 데이터에 일련의 가중치를 곱하고 편향 항을 추가하는 완전 연결 레이어입니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({ units: 1, inputShape: [1] }));
```

훈련하기 전에 모델을 컴파일해야 합니다. 간단한 그래디언트 디센트 옵티마이저인 `sgd` 옵티마이저를 사용할 것입니다. 또한 모델이 최소화해야 하는 `loss` 함수와 추적하려는 `metrics`를 지정합니다. 이 경우 `meanSquaredError` 및 `meanAbsoluteError`를 추적합니다.

```javascript
model.compile({
  optimizer: tf.train.sgd(LEARNING_RATE),
  loss: 'meanSquaredError',
  metrics: ['meanSquaredError', 'meanAbsoluteError']
});
```

## 모델 교육

이제 모델을 정의했으므로 일부 데이터에서 모델을 교육해야 합니다. 이 예제에서는 10개의 포인트로 구성된 간단한 데이터 세트를 사용합니다.

```javascript
const xs = tf.tensor2d([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
const ys = tf.tensor2d([-3, -1, 1, 3, 5, 7, 9, 11, 13, 15], [10, 1]);
```

이제 모델을 훈련할 수 있습니다. `batchSize`, `epochs` 수를 지정하고 각 epoch 전에 데이터를 `shuffle`합니다. 모델이 각 에포크 후 손실 및 메트릭을 평가하는 데 사용할 'validationData' 세트도 지정합니다.

```javascript
model.fit(xs, ys, {
  batchSize: BATCH_SIZE,
  epochs: EPOCHS,
  shuffle: true,
  validationData: [xs, ys]
}).then(() => {
  // The model is trained!
});
```

## 모델 저장

모델이 훈련되면 브라우저에서 사용할 수 있도록 모델을 저장해야 합니다. `tf.node.save` 함수를 사용하여 모델을 `.pb` 파일에 저장할 수 있습니다.

```javascript
tf.node.save(model, './model.pb');
```

## 모델 불러오기

이제 모델을 저장했으므로 브라우저에서 로드할 수 있습니다. `tf.loadFrozenModel` 함수를 사용하여 모델을 로드합니다. 이 함수는 `modelUrl` 및 `weightsManifestUrl`을 사용합니다. `modelUrl`은 이전 단계에서 저장한 `.pb` 파일의 경로입니다. `weightsManifestUrl`은 모델의 가중치에 대한 정보가 포함된 JSON 파일의 경로입니다.

```javascript
const modelUrl = './model.pb';
const weightsManifestUrl = './weights_manifest.json';

tf.loadFrozenModel(modelUrl, weightsManifestUrl).then(model => {
  // The model is loaded!
});
```

## 3D 객체 생성

이제 모델을 로드했으므로 모델을 사용하여 3D 개체를 생성할 수 있습니다. `tf.tensor` 함수를 사용하여 숫자 배열에서 텐서를 생성합니다. 이 텐서는 모델에 대한 입력으로 사용됩니다.

```javascript
const input = tf.tensor([-1, 0, 1, 2, 3, 4, 5, 6, 7, 8], [10, 1]);
```

이제 `model.predict` 메서드를 사용하여 입력 텐서에서 예측을 생성할 수 있습니다. 이 메서드는 3D 객체를 생성하는 데 사용할 수 있는 `tf.Tensor` 객체를 반환합니다.

```javascript
model.predict(input).then(output => {
  // The output tensor can be used to generate 3D objects!
});
```

## 3D 개체 렌더링

이제 3D 객체를 생성했으므로 브라우저에서 렌더링해야 합니다. 이를 위해 `three.js` 라이브러리를 사용할 것입니다.

먼저 `Scene` 개체를 만들어야 합니다. 이 개체에는 렌더링하려는 3D 개체가 포함됩니다.

```javascript
const scene = new THREE.Scene();
```

다음으로 `Camera` 개체를 만들어야 합니다. 이 개체는 장면을 보려는 관점을 정의합니다.

```javascript
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
```

이제 `Renderer` 개체를 만들 수 있습니다. 이 객체는 `Scene` 및 `Camera` 객체를 가져와서 페이지에 렌더링합니다.

```javascript
const renderer = new THREE.WebGLRenderer();
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);
```

마지막으로 3D 개체를 만들고 `Scene` 개체에 추가해야 합니다. 이전 단계의 `output` 텐서를 사용하여 3D 객체를 생성합니다.

```javascript
const geometry = new THREE.Geometry();
for (let i = 0; i < output.shape[0]; i++) {
  geometry.vertices.push(new THREE.Vector3(i, output.get(i, 0), 0));
}
const material = new THREE.LineBasicMaterial({ color: 0xff0000 });
const line = new THREE.Line(geometry, material);
scene.add(line);
```

## 3D 개체 애니메이션

이제 3D 개체를 렌더링했으므로 애니메이션을 적용해야 합니다. 이를 위해 `requestAnimationFrame` 함수를 사용합니다. 이 함수는 다음에 다시 그리기 전에 지정된 함수를 호출하도록 브라우저에 지시합니다.

```javascript
function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}
animate();
```

## 사용자의 머리 추적

이제 3D 개체에 애니메이션을 적용했으므로 3D 개체가 올바른 위치에 나타나도록 사용자의 머리를 추적해야 합니다. 이를 위해 `ar.js` 라이브러리를 사용할 것입니다.

먼저 `ARController` 개체를 만들어야 합니다. 이 개체는 사용자의 머리를 추적하고 올바른 위치에 3D 개체를 표시합니다.

```javascript
const arController = new ARController(renderer, {
  cameraParametersUrl: './camera_para.dat',
  maxDetectionRate: 60,
  canvasWidth: 640,
  canvasHeight: 480
});
```

다음으로 사용자의 머리를 추적하도록 `ARController`에 지시해야 합니다. 우리는 이것을 `loadNFTMarker` 방법으로 할 수 있습니다. 이 메서드는 마커 파일의 경로인 'markerUrl'을 사용합니다. `markerUrl`을 사용하여 `nft-marker-files` 디렉토리에서 마커 파일을 로드할 수 있습니다.

```javascript
arController.loadNFTMarker('./nft-marker-files/hiro.jpg');
```

마지막으로 사용자 머리 추적을 시작하도록 `ARController`에 지시해야 합니다. 우리는 `startNFTMarkerTracking` 방법으로 이것을 할 수 있습니다.

```javascript
arController.startNFTMarkerTracking();
```

## 3D 개체 표시

이제 사용자의 머리를 추적했으므로 올바른 위치에 3D 개체를 표시할 수 있습니다. 사용자가 현재 보고 있는 마커를 가져오기 위해 `arController.getNFTMarker` 메서드를 사용할 것입니다. 이 메서드는 `THREE.Object3D` 객체를 반환하며 이를 `Scene` 객체에 추가할 수 있습니다.

```javascript
const marker = arController.getNFTMarker(0);
scene.add(marker);
```

## 바로 그거야!

그게 전부입니다! 이제 사용자의 머리를 기준으로 올바른 위치에 3D 개체를 렌더링하는 작동하는 AR 애플리케이션이 있어야 합니다.

## 자원

* [TensorFlow.js](https://js.tensorflow.org/)
* [Three.js](https://threejs.org/)
* [AR.js](https://github.com/jeromeetienne/AR.js)