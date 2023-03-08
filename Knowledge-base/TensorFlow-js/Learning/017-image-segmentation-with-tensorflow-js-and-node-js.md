---
title: 017: TensorFlow.js 및 Node.js를 사용한 이미지 분할
description: 
published: true
date: 2023-02-02T10:44:35.943Z
tags: 
editor: markdown
dateCreated: 2023-02-02T10:44:34.180Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [017: Image Segmentation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/017-image-segmentation-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이미지 분할을 수행하는 방법을 살펴보겠습니다. 이미지 분할은 이미지를 별개의 영역으로 분할하는 프로세스입니다. 이것은 컴퓨터 비전 응용 프로그램에서 이미지의 개체를 식별하는 데 자주 사용됩니다.

이미지 분할을 위해 [TensorFlow.js](https://js.tensorflow.org/) 라이브러리를 사용할 것입니다. TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 브라우저와 Node.js 모두에서 딥 러닝에 사용됩니다.

예제에서는 [Node.js](https://nodejs.org/) 런타임을 사용합니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다. 서버 측 프로그래밍에 자주 사용됩니다.

## 시작하기

시작하기 전에 TensorFlow.js 및 Node.js 종속 항목을 설치해야 합니다. [npm](https://www.npmjs.com/) 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

먼저 프로젝트를 위한 새 디렉터리를 만듭니다.

```
mkdir image-segmentation
```

다음으로 새 npm 프로젝트를 초기화해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
npm init -y
```

이렇게 하면 프로젝트 디렉토리에 `package.json`이라는 새 파일이 생성됩니다. 이 파일에는 설치해야 하는 종속성과 같은 프로젝트에 대한 정보가 포함되어 있습니다.

이제 TensorFlow.js 및 Node.js 종속성을 설치할 수 있습니다. Node.js에서 TensorFlow.js를 실행할 수 있는 [tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node) 패키지를 사용할 것입니다.

종속 항목을 설치하려면 다음 명령을 실행합니다.

```
npm install @tensorflow/tfjs-node
```

이렇게 하면 프로젝트에 TensorFlow.js 및 Node.js 종속성이 설치됩니다.

## 이미지 불러오기

이제 의존성을 설치했으므로 이미지 분할 프로그램 작성을 시작할 수 있습니다.

먼저 이미지를 로드해야 합니다. [tf.node.decodeImage](https://js.tensorflow.org/api/latest/# node.decodeImage) 함수를 사용하여 이미지를 로드합니다. 이 함수는 이미지 데이터가 포함된 `buffer`를 받아서 이미지 데이터가 포함된 `tf.Tensor3D`를 반환합니다.

Node.js 표준 라이브러리의 일부인 [fs](https://nodejs.org/api/fs.html) 모듈을 사용하여 이미지 데이터를 읽을 수 있습니다. [fs.readFile](https://nodejs.org/api/fs.html# fs_fs_readfile_path_options_callback) 함수는 이미지 경로를 받아 이미지 데이터를 '버퍼'로 반환합니다.

`fs` 모듈을 사용하려면 프로그램으로 가져와야 합니다. [require](https://nodejs.org/api/modules.html# modules_require_id) 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');
```

이제 `fs` 모듈을 가져왔으므로 `fs.readFile` 함수를 사용하여 이미지 데이터를 읽을 수 있습니다.

```javascript
const imageData = fs.readFileSync('image.jpg');
```

`imageData` 변수는 이제 이미지 데이터를 `buffer`로 포함합니다.

다음으로 이미지 데이터를 디코딩해야 합니다. `tf.node.decodeImage` 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const imageTensor = tf.node.decodeImage(imageData);
```

`imageTensor` 변수는 이제 이미지 데이터를 `tf.Tensor3D`로 포함합니다.

## 이미지 전처리

이미지 분할을 수행하기 전에 이미지를 사전 처리해야 합니다. 여기에는 분할을 준비하기 위해 이미지 데이터에 대한 몇 가지 작업을 수행하는 것이 포함됩니다.

먼저 이미지 크기를 조정해야 합니다. [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear) 함수를 사용하여 이미지 크기를 조정합니다. 이 함수는 이미지 `tf.Tensor`와 크기(`[높이, 너비]`)를 받아서 크기가 조정된 이미지 `tf.Tensor`를 반환합니다.

이미지 크기를 `[128, 128]` 크기로 조정합니다.

```javascript
const imageSize = [128, 128];
const imageTensor = tf.image.resizeBilinear(imageTensor, imageSize);
```

이제 `imageTensor` 변수에는 크기가 조정된 이미지 데이터가 `tf.Tensor3D`로 포함됩니다.

다음으로 이미지 데이터를 정규화해야 합니다. [tf.image.normalize](https://js.tensorflow.org/api/latest/# tf.image.normalize) 함수를 사용하여 이미지를 정규화합니다. 이 함수는 이미지 `tf.Tensor`를 가져와 정규화된 이미지 `tf.Tensor`를 반환합니다.

평균을 빼고 표준 편차로 나누어 이미지를 정규화합니다.

```javascript
const imageTensor = tf.image.normalize(imageTensor, [0, 255], -1, 1);
```

`imageTensor` 변수는 이제 정규화된 이미지 데이터를 `tf.Tensor3D`로 포함합니다.

## 이미지 분할 수행

이제 이미지를 사전 처리했으므로 이미지 분할을 수행할 수 있습니다. [tf.image.segmentation.segmentationKMeans](https://js.tensorflow.org/api/latest/# tf.image.segmentation.segmentationKMeans) 함수를 사용하여 이미지 분할을 수행합니다. 이 함수는 이미지 `tf.Tensor`를 가져와 분할 맵 `tf.Tensor`를 반환합니다.

이미지를 `4` 영역으로 분할합니다.

```javascript
const numSegments = 4;
const segmentationMap = tf.image.segmentation.segmentationKMeans(imageTensor, numSegments);
```

`segmentationMap` 변수는 이제 분할 지도를 `tf.Tensor3D`로 포함합니다.

## 세분화 맵 시각화

이제 이미지를 분할했으므로 분할 맵을 시각화해야 합니다. [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 함수를 사용하여 이를 수행할 수 있습니다. 이 함수는 숫자 배열을 받아 `tf.Tensor3D`를 반환합니다.

먼저 분할 맵 `tf.Tensor`를 배열로 변환해야 합니다. [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const segmentationMapArray = segmentationMap.arraySync();
```

`segmentationMapArray` 변수는 이제 분할 맵을 배열로 포함합니다.

다음으로 분할 지도 배열을 `tf.Tensor3D`로 변환해야 합니다. [tf.tensor3d](https://js.tensorflow.org/api/latest/# tf.tensor3d) 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const segmentationMapTensor = tf.tensor3d(segmentationMapArray);
```

`segmentationMapTensor` 변수는 이제 분할 맵을 `tf.Tensor3D`로 포함합니다.

마지막으로 [tf.image.resizeBilinear](https://js.tensorflow.org/api/latest/# tf.image.resizeBilinear) 함수를 사용하여 세분화 맵을 시각화할 수 있습니다. 이 함수는 이미지 `tf.Tensor`와 크기(`[높이, 너비]`)를 받아서 크기가 조정된 이미지 `tf.Tensor`를 반환합니다.

분할 맵의 크기를 이미지의 원래 크기로 조정합니다.

```javascript
const segmentationMapImage = tf.image.resizeBilinear(segmentationMapTensor, [imageHeight, imageWidth]);
```

`segmentationMapImage` 변수는 이제 분할 맵을 `tf.Tensor3D`로 포함합니다.

## 분할 맵 저장

이제 세분화 맵을 시각화했으므로 저장해야 합니다. [tf.node.encodePng](https://js.tensorflow.org/api/latest/# node.encodePng) 함수를 사용하여 이를 수행할 수 있습니다. 이 함수는 이미지 `tf.Tensor`를 가져오고 PNG 데이터를 포함하는 `buffer`를 반환합니다.

[fs](https://nodejs.org/api/fs.html) 모듈을 사용하여 이 데이터를 파일에 쓸 수 있습니다. [fs.writeFile](https://nodejs.org/api/fs.html# fs_fs_writefile_file_data_options_callback) 함수는 파일 경로, 쓸 데이터, 콜백 함수를 받습니다.

`fs` 모듈을 사용하려면 프로그램으로 가져와야 합니다. [require](https://nodejs.org/api/modules.html# modules_require_id) 함수를 사용하여 이를 수행할 수 있습니다.

```javascript
const fs = require('fs');
```

이제 `fs` 모듈을 가져왔으므로 `fs.writeFile` 함수를 사용하여 세분화 맵 데이터를 파일에 쓸 수 있습니다.

```javascript
const segmentationMapData = tf.node.encodePng(segmentationMapImage);
fs.writeFileSync('segmentation-map.png', segmentationMapData);
```

이렇게 하면 분할 맵 데이터를 `segmentation-map.png`라는 파일에 씁니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 이미지 분할을 수행하는 방법을 살펴보았습니다. 또한 분할 맵을 시각화하고 파일에 저장하는 방법도 살펴보았습니다.

이미지 분할은 컴퓨터 비전 애플리케이션을 위한 강력한 도구입니다. TensorFlow.js를 사용하면 브라우저와 Node.js에서 이미지 분할을 쉽게 수행할 수 있습니다.