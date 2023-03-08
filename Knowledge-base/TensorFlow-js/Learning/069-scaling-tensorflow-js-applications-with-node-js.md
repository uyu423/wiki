---
title: 069: Node.js로 TensorFlow.js 애플리케이션 확장
description: 
published: true
date: 2023-02-02T23:04:23.318Z
tags: 
editor: markdown
dateCreated: 2023-02-02T23:04:21.726Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [069: Scaling TensorFlow.js Applications with Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/069-scaling-tensorflow-js-applications-with-node-js)
{.links-list}


# 069: Node.js로 TensorFlow.js 애플리케이션 확장

TensorFlow.js는 JavaScript에서 기계 학습을 위한 강력한 도구이지만 TensorFlow.js 애플리케이션이 브라우저보다 커질 때 어떻게 해야 할까요? 이 게시물에서는 Node.js로 TensorFlow.js 애플리케이션을 확장하는 방법을 살펴보겠습니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 자바스크립트 기계 학습을 위한 오픈 소스 라이브러리입니다. 개발자가 브라우저 또는 Node.js에서 실행되는 정교한 기계 학습 모델을 만드는 데 사용됩니다.

## TensorFlow.js에 Node.js를 사용하는 이유는 무엇인가요?

Node.js는 TensorFlow.js 애플리케이션 확장을 위한 훌륭한 선택입니다. 빠르고 효율적이며 라이브러리 및 도구의 대규모 에코 시스템이 있습니다.

## Node.js로 TensorFlow.js를 확장하는 방법

Node.js로 TensorFlow.js 애플리케이션을 확장하는 두 가지 주요 방법이 있습니다.

1. `tensorflow.js` Node.js 모듈을 사용합니다.
2. `tfjs-node`와 같은 TensorFlow.js 호환 라이브러리를 사용합니다.

아래에서 이러한 각 방법을 자세히 살펴보겠습니다.

### `tensorflow.js` Node.js 모듈 사용

`tensorflow.js` Node.js 모듈은 Node.js에서 TensorFlow.js를 실행하는 공식적인 방법입니다. 설치 및 사용이 쉽습니다.

`tensorflow.js` Node.js 모듈을 설치하려면 다음 명령을 실행하십시오.

```
npm install @tensorflow/tfjs
```

`tensorflow.js` Node.js 모듈을 사용하려면 코드에 다음과 같이 요구하세요.

```javascript
const tf = require('@tensorflow/tfjs');
```

이제 Node.js 애플리케이션에서 모든 TensorFlow.js API를 사용할 수 있습니다.

### TensorFlow.js 호환 라이브러리 사용

`tfjs-node`와 같은 TensorFlow.js 호환 라이브러리를 사용하려면 먼저 설치해야 합니다.

`tfjs-node`를 설치하려면 다음 명령을 실행하십시오.

```
npm install tfjs-node
```

`tfjs-node`를 사용하려면 코드에 필요합니다.

```javascript
const tf = require('tfjs-node');
```

이제 Node.js 애플리케이션에서 모든 TensorFlow.js API를 사용할 수 있습니다.

## 추가 자료

- [TensorFlow.js 문서](https://js.tensorflow.org/)
- [tfjs-node 문서](https://github.com/tensorflow/tfjs-node)
- [Node.js 문서](https://nodejs.org/en/docs/)