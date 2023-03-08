---
title: 009: TensorFlow.js 및 Node.js를 사용한 순환 신경망(RNN)
description: 
published: true
date: 2023-02-02T08:44:02.992Z
tags: 
editor: markdown
dateCreated: 2023-02-02T08:43:58.500Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [009: Recurrent Neural Networks (RNN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/009-recurrent-neural-networks-rnn-with-tensorflow-js-and-node-js)
{.links-list}


# 소개

순환 신경망(RNN)은 텍스트, 오디오 및 비디오와 같은 순차적 데이터를 처리하는 데 매우 적합한 신경망 유형입니다. 이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 문자별로 새 텍스트를 생성할 수 있는 RNN을 빌드할 것입니다.

# 프로젝트 설정

시작하기 전에 프로젝트를 설정해야 합니다. Node.js용 Express 웹 프레임워크를 사용할 것이므로 먼저 설치해야 합니다.

```
$ npm install express --save
```

다음으로 TensorFlow.js를 설치해야 합니다. Node.js API를 사용할 것이므로 `@tensorflow/tfjs-node` 패키지를 설치해야 합니다.

```
$ npm install @tensorflow/tfjs-node --save
```

이제 필요한 모든 종속성이 있으므로 프로젝트의 루트 디렉터리에 `index.js`라는 파일을 만들고 코딩을 시작할 수 있습니다.

# RNN 구축

가장 먼저 해야 할 일은 RNN 훈련에 사용할 데이터를 로드하는 것입니다. [여기](https://storage.googleapis.com/tfjs-examples/shakespeare.txt)에서 다운로드할 수 있는 셰익스피어 텍스트 코퍼스를 사용할 것입니다.

텍스트 파일을 다운로드했으면 `fs` 모듈을 사용하여 Node.js 프로그램에 로드할 수 있습니다.

```javascript
const fs = require('fs');

const text = fs.readFileSync('shakespeare.txt', 'utf8');
```

이제 텍스트를 로드했으므로 RNN 교육에 적합하도록 전처리해야 합니다. 모든 문자를 소문자로 변환하고 영숫자가 아닌 모든 문자를 제거하는 것으로 시작합니다.

```javascript
const text = text.toLowerCase();
const text = text.replace(/[^a-zA-Z0-9]/g, '');
```

다음으로 텍스트를 개별 문자 배열로 분할해야 합니다.

```javascript
const chars = Array.from(text);
```

이제 텍스트가 사전 처리되었으므로 RNN 구축을 시작할 수 있습니다. 순차적 데이터 처리에 적합한 RNN 셀 유형인 LSTM(Long Short-Term Memory) 셀을 사용할 것입니다.

다음 코드를 사용하여 TensorFlow.js에서 LSTM 셀을 만들 수 있습니다.

```javascript
const lstmCell = tf.layers.lstmCell({
  units: 512,
  recurrentInputSize: 512,
  inputShape: [1, chars.length],
  kernelInitializer: 'glorotNormal',
  recurrentInitializer: 'orthogonal',
  biasInitializer: 'zeros',
  unitForgetBias: true,
  activation: 'tanh',
  recurrentActivation: 'sigmoid',
  useBias: true,
  kernelRegularizer: null,
  recurrentRegularizer: null,
  biasRegularizer: null,
  activityRegularizer: null,
  kernelConstraint: null,
  recurrentConstraint: null,
  biasConstraint: null,
  dropout: 0.0,
  recurrentDropout: 0.0
});
```

다음으로 RNN 자체를 생성해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const rnn = tf.layers.rnn({
  cell: lstmCell,
  inputShape: [1, chars.length],
  returnSequences: true,
  goBackwards: false,
  stateful: false,
  unroll: false
});
```

이제 RNN이 생성되었으므로 컴파일해야 합니다. Adam 옵티마이저와 범주형 교차 엔트로피를 손실 함수로 사용할 것입니다.

```javascript
rnn.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

# RNN 교육

이제 RNN이 컴파일되었으므로 훈련을 시작할 수 있습니다. 먼저 훈련 데이터를 만들어야 합니다. 각 문자는 문자에 해당하는 인덱스에 1이 있는 0의 벡터로 표현되는 원-핫 인코딩 문자 배열을 만듭니다.

```javascript
const chars = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];

const oneHotChars = [];

for (let i = 0; i < chars.length; i++) {
  const char = chars[i];
  const oneHotChar = [];

  for (let j = 0; j < chars.length; j++) {
    if (j === i) {
      oneHotChar.push(1.0);
    } else {
      oneHotChar.push(0.0);
    }
  }

  oneHotChars.push(oneHotChar);
}
```

원-핫 인코딩된 문자가 있으므로 학습 데이터를 만들어야 합니다. 각 훈련 예제가 한 쌍의 원-핫 인코딩 문자인 훈련 예제 배열을 만들 것입니다. 쌍의 첫 번째 문자는 입력 문자가 되고 두 번째 문자는 출력 문자가 됩니다.

```javascript
const trainingData = [];

for (let i = 0; i < text.length - 1; i++) {
  const inputChar = oneHotChars[chars.indexOf(text[i])];
  const outputChar = oneHotChars[chars.indexOf(text[i + 1])];

  trainingData.push([inputChar, outputChar]);
}
```

이제 교육 데이터가 있으므로 RNN을 교육할 수 있습니다. 우리는 그것을 10 에포크 동안 훈련시키고 32의 배치 크기를 사용할 것입니다.

```javascript
rnn.fit(trainingData, {
  epochs: 10,
  batchSize: 32
});
```

# 텍스트 생성

이제 RNN이 훈련되었으므로 이를 사용하여 새 텍스트를 생성할 수 있습니다. 문자를 받아서 다음 문자를 반환하는 함수를 만드는 것으로 시작하겠습니다.

```javascript
function nextChar(char) {
  const oneHotChar = oneHotChars[chars.indexOf(char)];
  const output = rnn.predict(tf.tensor2d([oneHotChar], [1, oneHotChar.length]));
  const index = output.argMax(1).dataSync()[0];
  const nextChar = chars[index];

  return nextChar;
}
```

이제 `nextChar` 함수를 사용하여 새 텍스트를 생성할 수 있습니다. 문자 'a'로 시작하여 1000자를 생성합니다.

```javascript
let text = 'a';

for (let i = 0; i < 1000; i++) {
  text += nextChar(text[text.length - 1]);
}

console.log(text);
```

그리고 그게 다야! 이제 문자별로 새 텍스트를 생성할 수 있는 작업 RNN이 있습니다.

# 추가 정보

RNN에 대해 자세히 알아보고 싶다면 다음 리소스를 추천합니다.

- [TensorFlow의 순환 신경망](https://www.tensorflow.org/tutorials/sequences/recurrent)
- [LSTM 네트워크 이해하기](http://colah.github.io/posts/2015-08-Understanding-LSTMs/)
- [TensorFlow로 순환 신경망 구축하기](https://www.oreilly.com/learning/building-a-recurrent-neural-network-with-tensorflow)