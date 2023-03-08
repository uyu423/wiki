---
title: 067: TensorFlow.js 및 Node.js로 데스크톱 애플리케이션 만들기
description: 
published: true
date: 2023-02-02T22:36:28.311Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:36:26.666Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [067: Creating Desktop Applications with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/067-creating-desktop-applications-with-tensorflow-js-and-node-js)
{.links-list}


# 067: TensorFlow.js 및 Node.js로 데스크톱 애플리케이션 만들기

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 데스크톱 애플리케이션을 만드는 방법을 살펴보겠습니다.

TensorFlow.js는 자바스크립트에서 기계 학습을 위한 강력한 도구입니다. Node.js는 브라우저 외부에서 JavaScript 코드를 실행할 수 있게 해주는 JavaScript 런타임입니다.

이 두 가지 기술을 함께 사용하여 머신 러닝을 사용하는 데스크톱 애플리케이션을 만들 수 있습니다.

## 시작하기

시작하려면 Node.js 및 TensorFlow.js를 설치해야 합니다.

Node.js는 [Node.js 웹사이트](https://nodejs.org/en/)에서 다운로드할 수 있습니다. TensorFlow.js는 [Node.js 패키지 관리자](https://www.npmjs.com/)를 사용하여 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

Node.js와 TensorFlow.js가 설치되면 데스크톱 애플리케이션을 만들 준비가 된 것입니다.

## 데스크톱 애플리케이션 만들기

TensorFlow.js 및 Node.js로 데스크톱 애플리케이션을 만들려면 Node.js 파일과 HTML 파일을 만들어야 합니다.

Node.js 파일은 기계 학습 코드를 실행하는 데 사용됩니다. HTML 파일은 기계 학습 코드의 결과를 표시하는 데 사용됩니다.

`main.js`라는 Node.js 파일을 만드는 것으로 시작하겠습니다. 이 파일에서는 TensorFlow.js 라이브러리가 필요하고 선행 학습된 모델을 로드합니다.

```javascript
const tf = require('@tensorflow/tfjs');

// Load a pre-trained model.
const model = tf.loadModel('https://storage.googleapis.com/tfjs-models/tfjs/mobilenet_v1_0.25_224/model.json');
```

다음으로 `index.html`이라는 HTML 파일을 만듭니다. 이 파일에는 다음 코드가 포함됩니다.

```html
<html>
  <head>
    <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs"></script>
    <script src="main.js"></script>
  </head>
  <body>
    <h1>Hello, TensorFlow.js!</h1>
  </body>
</html>
```

이 코드에는 TensorFlow.js 라이브러리와 `main.js` 파일이 포함되어 있습니다. 간단한 `<h1>` 태그도 포함되어 있습니다.

마지막으로 Node.js를 사용하여 `index.html` 파일을 실행해야 합니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
node index.html
```

이렇게 하면 로컬 서버가 시작되고 기본 웹 브라우저에서 `index.html` 파일이 열립니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 데스크톱 애플리케이션을 만드는 방법을 살펴보았습니다. 사전 학습된 모델을 로드하고 Node.js 파일에서 실행하는 방법도 살펴보았습니다.

TensorFlow.js 및 Node.js에 대해 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- [TensorFlow.js 시작하기](https://js.tensorflow.org/tutorials/getting-started.html)
- [초보자를 위한 TensorFlow.js](https://www.youtube.com/watch?v=HEQDRWMK6yY)
- [초보자를 위한 Node.js](https://www.youtube.com/watch?v=U8XF6AFGqlc)