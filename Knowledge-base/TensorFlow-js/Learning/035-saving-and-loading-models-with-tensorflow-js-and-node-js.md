---
title: 035: TensorFlow.js 및 Node.js로 모델 저장 및 로드
description: 
published: true
date: 2023-02-02T15:17:20.463Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:17:18.807Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [035: Saving and Loading Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/035-saving-and-loading-models-with-tensorflow-js-and-node-js)
{.links-list}


## TensorFlow.js 및 Node.js로 모델 저장 및 로드

이 게시물에서는 TensorFlow.js 및 Node.js로 모델을 저장하고 로드하는 방법을 알아봅니다. 다음 주제를 다룹니다.

- TensorFlow.js로 모델 저장
- TensorFlow.js로 모델 로드
- Node.js로 모델 사용

### TensorFlow.js로 모델 저장

첫 번째 단계는 모델을 저장하는 것입니다. `tf.Model.save` 메서드를 사용하여 이 작업을 수행할 수 있습니다. 이 메서드는 두 가지 인수를 사용합니다.

- `경로`: 모델을 저장할 경로입니다.
- `overwrite`: 지정된 경로에서 기존 모델을 덮어쓸지 여부를 나타내는 부울입니다.

다음은 모델을 저장하는 예입니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

model.save('/tmp/model/1/model.json', true);
```

이 예에서는 모델을 `/tmp/model/1` 디렉토리에 저장했습니다. `overwrite` 매개변수는 `true`로 설정되어 있으므로 해당 디렉토리에 모델이 이미 있는 경우 덮어씁니다.

### TensorFlow.js로 모델 로드

이제 모델을 저장했으므로 모델을 로드하는 방법을 알아보겠습니다. `tf.loadModel` 메서드를 사용하여 이 작업을 수행할 수 있습니다. 이 메서드는 하나의 인수를 사용합니다.

- `경로`: 저장된 모델의 경로입니다.

다음은 모델을 로드하는 예입니다.

```javascript
const model = await tf.loadModel('/tmp/model/1/model.json');
```

이 예에서는 `/tmp/model/1` 디렉토리에서 모델을 로드했습니다.

### Node.js로 모델 사용하기

모델을 로드하면 모델을 사용하여 예측할 수 있습니다. 우리는 이것을 `model.predict` 메소드로 할 수 있습니다. 이 메서드는 하나의 인수를 사용합니다.

- `입력`: 예측을 수행할 입력 데이터입니다. 이것은 단일 `tf.Tensor` 또는 `tf.Tensor`의 `Array`일 수 있습니다.

다음은 모델을 사용하여 예측을 수행하는 예입니다.

```javascript
const input = tf.tensor2d([[1.0]]);
const output = model.predict(input);

output.print();
```

이 예제에서는 값이 `[[1.0]]`인 `tf.Tensor`를 만들었습니다. 이 텐서를 예측을 반환하는 `model.predict` 메서드에 전달했습니다. 그런 다음 예측을 콘솔에 인쇄했습니다.