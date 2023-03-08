---
title: 096: TensorFlow.js 및 Node.js에서 게이트 반복 단위(GRU) 빌드
description: 
published: true
date: 2023-02-03T05:38:01.336Z
tags: 
editor: markdown
dateCreated: 2023-02-03T05:37:59.459Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [096: Building Gated Recurrent Units (GRUs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/096-building-gated-recurrent-units-grus-in-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js의 GRU

## GRU가 무엇인가요?

GRU(Gated Recurrent Unit)는 순차 데이터에서 장기 종속성을 더 잘 캡처하도록 설계된 순환 신경망(RNN) 유형입니다. 기존 RNN과 달리 GRU에는 숨겨진 상태로 들어오고 나가는 정보의 흐름을 제어하는 두 개의 게이트가 있습니다. 업데이트 게이트는 새로운 정보를 얼마만큼 받아들일 것인지를 결정하는 반면, 리셋 게이트는 얼마나 많은 이전 정보를 잊을 것인지를 결정합니다.

## TensorFlow.js에서 GRU 구축

TensorFlow.js는 브라우저와 Node.js에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다. 이 자습서에서는 TensorFlow.js에서 GRU를 빌드하고 이를 사용하여 시퀀스의 다음 단어를 예측하는 방법을 살펴봅니다.

### TensorFlow.js 설치하기

브라우저에서 이 튜토리얼을 실행하는 경우 다음 스크립트 태그를 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
<script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@latest"></script>
```

Node.js에서 이 튜토리얼을 실행하는 경우 다음 명령을 사용하여 TensorFlow.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
```

### 데이터 로드

이 자습서에서는 Amazon 제품 리뷰 데이터 세트를 사용합니다. 데이터 세트에는 각 리뷰에 대한 별점과 함께 다양한 제품에 대한 리뷰가 포함되어 있습니다.

먼저 데이터 세트를 TensorFlow.js에 로드해야 합니다. `tf.data.csv` 함수를 사용하여 이를 수행할 수 있습니다.

```
const dataset = tf.data.csv('https://storage.googleapis.com/tfjs-datasets/amazon_reviews_multilingual_CSV_V2/reviews.csv', {
  columnConfigs: {
    review_body: {
      isLabel: true
    },
    review_title: {
      isLabel: true
    },
    star_rating: {
      isLabel: true
    }
  }
});
```

### 데이터 전처리

모델을 교육하기 전에 데이터를 사전 처리해야 합니다. 다음 전처리 단계를 수행해야 합니다.

- 리뷰를 문장으로 토큰화합니다.
- 문장을 단어로 토큰화합니다.
- 단어를 정수로 변환합니다.

`tf.tokenize` 및 `tf.tensorize` 함수를 사용하여 각각 리뷰를 토큰화하고 정수로 변환할 수 있습니다.

```
const sentences = dataset.map(({review_body, review_title}) => tf.tokenize(review_body + ' ' + review_title));

const words = sentences.map(sentence => tf.tensor1d(sentence, 'int32'));
```

### 모델 구축

이제 모델을 만들 준비가 되었습니다. 이 튜토리얼에서는 GRU를 사용할 것입니다. 모델의 첫 번째 레이어는 '임베딩' 레이어입니다. 이 레이어는 단어를 가져와 특정 크기의 벡터로 변환합니다. `inputDim` 및 `outputDim` 매개변수를 사용하여 벡터의 크기를 지정할 수 있습니다. 값이 0인 단어(즉, 패딩)를 무시하도록 레이어에 지시하는 `maskZero` 매개변수도 지정해야 합니다.

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

모델의 다음 계층은 GRU 계층입니다. 이 레이어는 'Embedding' 레이어의 벡터 출력을 가져와 시퀀스의 정보를 캡처하는 단일 벡터로 변환합니다. `units` 매개변수를 사용하여 숨겨진 상태의 크기를 지정할 수 있습니다.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

모델의 마지막 레이어는 'Dense' 레이어입니다. 이 레이어는 GRU 레이어의 벡터 출력을 가져와 어휘의 단어에 대한 확률 분포로 변환합니다. `units` 매개변수를 사용하여 레이어의 단위 수를 지정할 수 있습니다. 또한 `activation` 및 `kernelInitializer` 매개변수를 지정해야 합니다. `activation` 매개변수는 사용할 활성화 함수를 지정하는 반면 `kernelInitializer` 매개변수는 레이어의 가중치에 대한 이니셜라이저를 지정합니다.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### 모델 컴파일

모델을 훈련하기 전에 모델을 컴파일해야 합니다. 모델을 컴파일할 때 다음 매개변수를 지정해야 합니다.

- 사용할 옵티마이저. 이 튜토리얼에서는 `adam` 옵티마이저를 사용할 것입니다.
- 사용할 손실 함수. 이 튜토리얼에서는 `categoricalCrossentropy` 손실 함수를 사용할 것입니다.
- 추적할 메트릭입니다. 이 자습서에서는 '정확도' 메트릭을 추적할 것입니다.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### 모델 교육

이제 모델을 교육할 준비가 되었습니다. 우리는 `model.fit` 방법을 사용하여 이것을 할 수 있습니다. 모델을 교육할 때 다음 매개변수를 지정해야 합니다.

- 훈련 데이터. 이것은 `tf.data.Dataset` 객체여야 합니다.
- 학습할 에포크 수입니다. 우리는 이 튜토리얼을 위해 10 에포크 동안 훈련할 것입니다.
- 사용할 배치 크기. 이 자습서에서는 배치 크기 32를 사용합니다.

`validationData` 매개변수를 지정할 수도 있습니다. 유효성 검사 데이터를 포함하는 `tf.data.Dataset` 개체여야 합니다. `validationData` 매개변수를 지정하면 모델은 각 에포크가 끝날 때 검증 데이터에 대해 평가됩니다.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### 예측하기

훈련된 모델을 사용하여 새로운 데이터를 예측할 수 있습니다. 예측을 하기 전에 새 데이터를 토큰화하고 정수로 변환해야 합니다. 이를 위해 `tf.tokenize` 및 `tf.tensorize` 함수를 사용할 수 있습니다:

```
const newSentences = tf.tokenize('this is a new sentence');
const newWords = tf.tensor1d(newSentences, 'int32');
```

그런 다음 `model.predict` 메서드를 사용하여 새 데이터에 대한 예측을 할 수 있습니다.

```
model.predict(newWords).print();
```

## Node.js에서 GRU 구축

이 섹션에서는 Node.js에서 GRU를 빌드하는 방법을 살펴보겠습니다. 이전 섹션에서와 동일한 Amazon 제품 리뷰 데이터 세트를 사용합니다.

### 종속성 설치

코딩을 시작하기 전에 다음 종속 항목을 설치해야 합니다.

- `@tensorflow/tfjs-node`: TensorFlow.js Node.js 바인딩입니다.
- `csv-parser`: Node.js용 CSV 파서입니다.
- `tokenizer`: Node.js용 자연어 처리 라이브러리입니다.

다음 명령을 사용하여 이러한 종속성을 설치할 수 있습니다.

```
npm install @tensorflow/tfjs-node csv-parser tokenizer
```

### 데이터 로드

데이터 세트를 메모리에 로드하는 것으로 시작하겠습니다. `csv-parser` 라이브러리를 사용하여 이를 수행할 수 있습니다.

```
const parser = csvParser();

parser.on('data', (data) => {
  // do something with the data
});

parser.on('end', () => {
  // do something when the parsing is finished
});

fs.createReadStream('reviews.csv').pipe(parser);
```

### 데이터 전처리

모델을 교육하기 전에 데이터를 사전 처리해야 합니다. 다음 전처리 단계를 수행해야 합니다.

- 리뷰를 문장으로 토큰화합니다.
- 문장을 단어로 토큰화합니다.
- 단어를 정수로 변환합니다.

리뷰를 문장과 단어로 토큰화하기 위해 `tokenizer` 라이브러리를 사용할 수 있습니다. 그런 다음 `tf.tensor1d` 함수를 사용하여 단어를 정수로 변환할 수 있습니다.

```
const sentences = reviews.map((review) => tokenizer.sentences(review));

const words = sentences.map((sentence) => tf.tensor1d(sentence.map((word) => tokenizer.words(word))));
```

### 모델 구축

이제 모델을 만들 준비가 되었습니다. 이 튜토리얼에서는 GRU를 사용할 것입니다. 모델의 첫 번째 레이어는 '임베딩' 레이어입니다. 이 레이어는 단어를 가져와 특정 크기의 벡터로 변환합니다. `inputDim` 및 `outputDim` 매개변수를 사용하여 벡터의 크기를 지정할 수 있습니다. 값이 0인 단어(즉, 패딩)를 무시하도록 레이어에 지시하는 `maskZero` 매개변수도 지정해야 합니다.

```
const model = tf.sequential();
model.add(tf.layers.embedding({
  inputDim: 10000,
  outputDim: 64,
  maskZero: true
}));
```

모델의 다음 계층은 GRU 계층입니다. 이 레이어는 'Embedding' 레이어의 벡터 출력을 가져와 시퀀스의 정보를 캡처하는 단일 벡터로 변환합니다. `units` 매개변수를 사용하여 숨겨진 상태의 크기를 지정할 수 있습니다.

```
model.add(tf.layers.gru({
  units: 64,
  returnSequences: true,
  recurrentInitializer: 'glorotUniform'
}));
```

모델의 마지막 레이어는 'Dense' 레이어입니다. 이 레이어는 GRU 레이어의 벡터 출력을 가져와 어휘의 단어에 대한 확률 분포로 변환합니다. `units` 매개변수를 사용하여 레이어의 단위 수를 지정할 수 있습니다. 또한 `activation` 및 `kernelInitializer` 매개변수를 지정해야 합니다. `activation` 매개변수는 사용할 활성화 함수를 지정하는 반면 `kernelInitializer` 매개변수는 레이어의 가중치에 대한 이니셜라이저를 지정합니다.

```
model.add(tf.layers.dense({
  units: 10000,
  activation: 'softmax',
  kernelInitializer: 'glorotUniform'
}));
```

### 모델 컴파일

모델을 훈련하기 전에 모델을 컴파일해야 합니다. 모델을 컴파일할 때 다음 매개변수를 지정해야 합니다.

- 사용할 옵티마이저. 이 튜토리얼에서는 `adam` 옵티마이저를 사용할 것입니다.
- 사용할 손실 함수. 이 튜토리얼에서는 `categoricalCrossentropy` 손실 함수를 사용할 것입니다.
- 추적할 메트릭입니다. 이 자습서에서는 '정확도' 메트릭을 추적할 것입니다.

```
model.compile({
  optimizer: 'adam',
  loss: 'categoricalCrossentropy',
  metrics: ['accuracy']
});
```

### 모델 교육

이제 모델을 교육할 준비가 되었습니다. 우리는 `model.fit` 방법을 사용하여 이것을 할 수 있습니다. 모델을 교육할 때 다음 매개변수를 지정해야 합니다.

- 훈련 데이터. 이것은 `tf.data.Dataset` 객체여야 합니다.
- 학습할 에포크 수입니다. 우리는 이 튜토리얼을 위해 10 에포크 동안 훈련할 것입니다.
- 사용할 배치 크기. 이 자습서에서는 배치 크기 32를 사용합니다.

`validationData` 매개변수를 지정할 수도 있습니다. 유효성 검사 데이터를 포함하는 `tf.data.Dataset` 개체여야 합니다. `validationData` 매개변수를 지정하면 모델은 각 에포크가 끝날 때 검증 데이터에 대해 평가됩니다.

```
model.fit(words, {
  epochs: 10,
  batchSize: 32,
  validationData: words
});
```

### 예측하기

훈련된 모델을 사용하여 새로운 데이터를 예측할 수 있습니다. 예측을 하기 전에 새 데이터를 토큰화하고 정수로 변환해야 합니다. 이를 위해 `tokenizer` 및 `tf.tensor1d` 라이브러리를 사용할 수 있습니다.

```
const newSentences = tokenizer.sentences('this is a new sentence');
const newWords = tf.tensor1d(newSentences.map((sentence) => tokenizer.words(sentence)));
```

그런 다음 `model.predict` 메서드를 사용하여 새 데이터에 대한 예측을 할 수 있습니다.

```
model.predict(newWords).print();
```

## 자원

- [Gated recurrent units](https://en.wikipedia.org/wiki/Gated_recurrent_unit)
- [TensorFlow.js](https://js.tensorflow.org/)
- [Node.js용 TensorFlow.js](https://js.tensorflow.org/api/latest/# tensorflowjs_node)
- [csv-파서](https://www.npmjs.com/package/csv-parser)
- [토큰나이저](https://www.npmjs.com/package/tokenizer)