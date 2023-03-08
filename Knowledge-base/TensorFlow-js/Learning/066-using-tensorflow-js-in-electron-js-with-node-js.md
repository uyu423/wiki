---
title: 066: Node.js와 함께 Electron.js에서 TensorFlow.js 사용
description: 
published: true
date: 2023-02-02T21:23:21.065Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:23:19.324Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [066: Using TensorFlow.js in Electron.js with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/066-using-tensorflow-js-in-electron-js-with-node-js)
{.links-list}


# Node.js를 사용한 Electron.js의 TensorFlow.js

## 소개

이 게시물에서는 Node.js와 함께 Electron.js에서 TensorFlow.js를 사용하는 방법을 살펴보겠습니다. TensorFlow.js 사용의 기본 사항을 살펴본 다음 Electron.js에서 사용하는 방법을 보여줍니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 이미지 분류, 개체 감지 및 텍스트 분류를 비롯한 다양한 작업에 사용됩니다.

## 시작하기

시작하려면 TensorFlow.js를 설치해야 합니다. 다음 명령으로 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js가 설치되면 다음 줄을 사용하여 JavaScript 코드로 가져올 수 있습니다.

```javascript
import * as tf from '@tensorflow/tfjs';
```

## Electron.js에서 TensorFlow.js 사용

이제 TensorFlow.js가 설치되었으므로 Electron.js에서 사용하는 방법을 살펴보겠습니다.

가장 먼저 해야 할 일은 새로운 Electron.js 프로젝트를 만드는 것입니다. 다음 명령으로 이를 수행할 수 있습니다.

```
npm init electron-app my-app
```

이렇게 하면 Electron.js 앱의 기본 구조로 "my-app"이라는 새 디렉토리가 생성됩니다.

다음으로 프로젝트에 TensorFlow.js를 설치해야 합니다. 다음 명령으로 이를 수행할 수 있습니다.

```
cd my-app
npm install @tensorflow/tfjs
```

TensorFlow.js가 설치되면 다음 줄을 사용하여 Electron.js 앱으로 가져올 수 있습니다.

```javascript
import * as tf from '@tensorflow/tfjs';
```

이제 TensorFlow.js가 설치되었으므로 앱에서 사용할 수 있습니다.

## 결론

이 게시물에서는 Node.js와 함께 Electron.js에서 TensorFlow.js를 사용하는 방법을 살펴보았습니다. TensorFlow.js 사용의 기본 사항을 살펴본 다음 Electron.js에서 사용하는 방법을 보여 주었습니다.