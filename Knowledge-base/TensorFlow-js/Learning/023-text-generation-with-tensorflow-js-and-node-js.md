---
title: 023: TensorFlow.js 및 Node.js를 사용한 텍스트 생성
description: 
published: true
date: 2023-02-02T12:17:20.836Z
tags: 
editor: markdown
dateCreated: 2023-02-02T12:17:19.203Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [023: Text Generation with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/023-text-generation-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js로 텍스트 생성

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 텍스트를 생성하는 방법을 알아봅니다. 텍스트 시퀀스에서 다음 문자를 예측하는 방법을 학습할 수 있는 반복 신경망(RNN) 유형인 char-rnn 모델을 사용할 것입니다.

## char-rnn이 무엇인가요?

char-rnn은 일련의 텍스트에서 다음 문자를 예측하는 방법을 학습할 수 있는 일종의 RNN입니다. 우리가 사용할 char-rnn 모델은 "Character-Aware Neural Language Models"(https://arxiv.org/abs/1508.06615) 문서에 설명된 모델을 기반으로 합니다.

## TensorFlow.js가 무엇인가요?

TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

## Node.js가 무엇인가요?

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다.

## 시작하기

먼저 TensorFlow.js와 Node.js를 설치해야 합니다. 우리는 Node.js 모듈인 TensorFlow.js char-rnn 모델을 사용할 것입니다.

```
npm install @tensorflow/tfjs-node
npm install @tensorflow/tfjs-node-charrnn
```

다음으로 훈련 데이터를 다운로드해야 합니다. 이 예에서는 셰익스피어 작품의 데이터 세트(https://www.kaggle.com/kinguistics/shakespeare-plays)를 사용합니다.

교육 데이터가 있으면 char-rnn 모델 교육을 시작할 수 있습니다. 학습 프로세스를 완료하는 데 몇 분 정도 걸릴 수 있습니다.

```
const tf = require('@tensorflow/tfjs-node');
const charRNN = require('@tensorflow/tfjs-node-charrnn');

const model = charRNN.create(
  'https://storage.googleapis.com/tfjs-models/tfjs/charrnn/data/shakespeare_input.txt',
  {
    rnnType: 'lstm',
    embeddingSize: 128,
    rnnUnits: 128,
    batchSize: 64,
    seqLength: 128,
    temperature: 0.8,
    numEpochs: 20
  });

model.fit().then(() => {
  // The model is trained!
});
```

모델이 훈련되면 이를 사용하여 텍스트를 생성할 수 있습니다.

```
model.generate('The').then((text) => {
  console.log(text);
});
```

## 추가 정보

- TensorFlow.js에 대한 자세한 내용은 TensorFlow.js 문서(https://js.tensorflow.org/)를 참조하세요.
- Node.js에 대한 자세한 내용은 Node.js 설명서(https://nodejs.org/en/docs/)를 참조하세요.