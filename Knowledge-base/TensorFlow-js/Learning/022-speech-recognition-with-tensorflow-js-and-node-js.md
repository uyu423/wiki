---
title: 022: TensorFlow.js 및 Node.js를 사용한 음성 인식
description: 
published: true
date: 2023-02-02T12:04:36.236Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:04:34.676Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [022: Speech Recognition with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/022-speech-recognition-with-tensorflow-js-and-node-js)
{.links-list}


# 022: TensorFlow.js 및 Node.js를 사용한 음성 인식

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 음성 인식 시스템을 구축하는 방법을 살펴보겠습니다.

먼저 환경 설정 방법을 살펴본 다음 코드를 살펴보겠습니다.

## 환경 설정

가장 먼저 해야 할 일은 TensorFlow.js를 설치하는 것입니다. 다음 명령으로 그렇게 할 수 있습니다.

```
npm install @tensorflow/tfjs
```

완료되면 TensorFlow.js용 Node.js 바인딩을 설치해야 합니다. 다음 명령으로 그렇게 할 수 있습니다.

```
npm install @tensorflow/tfjs-node
```

이제 코드로 넘어갈 수 있습니다.

## 코드

TensorFlow.js 라이브러리와 Node.js 바인딩을 로드하여 시작하겠습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');
require('@tensorflow/tfjs-node');
```

다음으로 음성 인식 라이브러리를 로드해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const speech = require('@tensorflow-models/speech-commands');
```

이제 재미있는 부분인 코드로 넘어갈 수 있습니다.

새로운 음성 인식 모델을 만드는 것으로 시작하겠습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const model = speech.createModel();
```

다음으로 모델을 교육해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
model.train({
  fileNames: [
    'file1.wav',
    'file2.wav',
    'file3.wav',
  ],
  labels: [
    'label1',
    'label2',
    'label3',
  ]
});
```

모델이 훈련되면 이제 이를 사용하여 음성을 인식할 수 있습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
model.recognize(audio, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

그리고 그게 다야! 이제 작동하는 음성 인식 시스템이 있습니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 음성 인식 시스템을 구축하는 방법을 살펴보았습니다. 우리는 환경을 설정하는 방법을 살펴보는 것으로 시작한 다음 코드에 들어갔습니다.

더 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- 공식 TensorFlow.js 문서: https://js.tensorflow.org/
- TensorFlow.js 설명서의 공식 Node.js 바인딩: https://js.tensorflow.org/tfjs-node/
- 공식 음성 인식 라이브러리 문서: https://js.tensorflow.org/speech-commands/