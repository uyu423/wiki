---
title: 021: TensorFlow.js 및 Node.js를 사용한 NER(Named Entity Recognition)
description: 
published: true
date: 2023-02-02T11:43:40.729Z
tags: 
editor: markdown
dateCreated: 2023-02-02T11:43:39.129Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [021: Named Entity Recognition (NER) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/021-named-entity-recognition-ner-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 NER(Named Entity Recognition)

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 JavaScript에서 명명된 엔터티 인식(NER)을 수행하는 방법을 살펴보겠습니다. NER는 자연어 처리(NLP)에서 사람, 장소, 조직 등과 같은 텍스트의 명명된 엔터티를 식별하고 분류하는 작업입니다.

CoNLL 2003 NER 데이터 세트에서 훈련된 사전 훈련된 모델을 사용할 것입니다. 모델은 상단에 CRF(Conditional Random Field) 레이어가 있는 BiLSTM(Bidirectional Long Short-Term Memory) 모델입니다.

## 전제 조건

이 게시물을 따르려면 다음이 필요합니다.

- Node.js(버전 8 이상)
- 텍스트 편집기 또는 IDE

## 시작하기

먼저 새 Node.js 프로젝트를 생성해 보겠습니다. 우리는 Express 웹 프레임워크를 사용할 것이므로 이것도 설치해야 합니다.

```
npm init
npm install --save express
```

다음으로 TensorFlow.js NER 모델을 설치해야 합니다. 다음 명령으로 그렇게 할 수 있습니다.

```
npm install @tensorflow-models/ner
```

이제 코딩을 시작할 준비가 되었습니다!

## 모델 불러오기

가장 먼저 해야 할 일은 모델을 로드하는 것입니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();
}

main();
```

위의 코드에서 먼저 TensorFlow.js와 NER 모델을 가져왔습니다. 그런 다음 모델을 로드하고 변수에 저장할 비동기 함수를 만들었습니다.

## 명명된 엔터티 예측

이제 모델을 로드했으므로 이를 사용하여 텍스트에서 명명된 엔터티를 예측할 수 있습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  console.log(results);
}

main();
```

위의 코드에서 명명된 엔터티를 예측하려는 텍스트 문자열을 추가했습니다. 그런 다음 모델의 'predict' 메서드를 사용하여 결과를 얻었습니다.

결과는 개체의 배열이며 각 개체는 명명된 엔터티를 나타냅니다. 각 개체에는 입력 텍스트에서 명명된 엔터티의 시작 및 끝 인덱스를 나타내는 `start` 및 `end` 속성과 예측에 대한 모델의 신뢰도를 나타내는 `score` 속성이 있습니다.

## 결과 시각화

예측 결과를 시각화하는 것이 도움이 될 수 있습니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const model = require('@tensorflow-models/ner');

async function main() {
  const ner = await model.load();

  const text = 'John Smith is a software engineer at Google.';

  const results = await ner.predict(text);

  for (const result of results) {
    console.log(
        `${text.substring(result.start, result.end)} (${result.score})`);
  }
}

main();
```

위의 코드에서 각 명명된 엔터티와 해당 예측에 대한 모델의 신뢰도 점수를 출력하는 루프를 추가했습니다.

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 JavaScript에서 명명된 엔터티 인식을 수행하는 방법을 살펴보았습니다. 또한 예측 결과를 시각화하는 방법도 살펴보았습니다.

NER 또는 TensorFlow.js에 대해 자세히 알아보려면 다음 리소스를 참조하세요.

- [TensorFlow를 사용한 명명된 엔터티 인식(블로그 게시물)](https://blog.tensorflow.org/2018/12/named-entity-recognition-ner-tensorflow.html)
- [TensorFlow.js NER 모델](https://js.tensorflow.org/tutorials/tensorflow-for-js- nerds.html)
- [CoNLL 2003 NER 데이터셋](https://www.clips.uantwerpen.be/conll2003/ner/)