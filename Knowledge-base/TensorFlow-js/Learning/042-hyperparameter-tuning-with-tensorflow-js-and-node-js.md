---
title: 042: TensorFlow.js 및 Node.js를 사용한 하이퍼파라미터 튜닝
description: 
published: true
date: 2023-02-02T16:44:18.750Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:44:14.175Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [042: Hyperparameter Tuning with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/042-hyperparameter-tuning-with-tensorflow-js-and-node-js)
{.links-list}


# 042: TensorFlow.js 및 Node.js를 사용한 하이퍼파라미터 튜닝

이 게시물에서는 Hyperparameter 튜닝을 위해 TensorFlow.js 및 Node.js를 사용하는 방법을 알아봅니다.

하이퍼파라미터 튜닝은 모델의 하이퍼파라미터에 가장 적합한 값을 선택하여 기계 학습 모델을 최적화하는 프로세스입니다. 하이퍼파라미터 튜닝의 목표는 본 적이 없는 데이터에서 모델의 최상의 성능을 제공하는 하이퍼파라미터 값을 찾는 것입니다.

초매개변수 튜닝에 접근하는 방법에는 몇 가지가 있습니다. 널리 사용되는 방법 중 하나는 가능한 모든 값 조합을 시도하여 하이퍼 매개변수의 최상의 값을 철저하게 검색하는 그리드 검색입니다.

또 다른 인기 있는 방법은 확률 모델을 사용하여 하이퍼파라미터의 최상의 값을 찾는 방법을 안내하는 베이지안 최적화입니다.

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 Bayesian 최적화를 사용하여 간단한 하이퍼파라미터 조정 실험을 구현합니다.

## 전제 조건

시작하기 전에 따라하기 위해 필요한 몇 가지 사항이 있습니다.

- 기계 학습 및 작동 방식에 대한 기본적인 이해
- 텍스트 편집기 또는 IDE
- 컴퓨터에 설치된 Node.js

## 시작하기

새 Node.js 프로젝트를 생성하여 시작하겠습니다. 프로젝트의 새 디렉터리를 만들고 npm으로 초기화합니다.

```
mkdir hyperparameter-tuning
cd hyperparameter-tuning
npm init -y
```

다음으로 프로젝트에 필요한 종속 항목을 설치합니다. [ BayesOptimization ](https://www.npmjs.com/package/bayesopt) 및 [ TensorFlow.js ](https://www.npmjs.com/package/@tensorflow/tfjs) 패키지가 필요합니다.

```
npm install --save bayesopt @tensorflow/tfjs
```

종속성이 설치되었으므로 이제 프로젝트 파일을 만들 수 있습니다. 프로젝트 디렉터리에 `index.js`라는 파일을 만들고 다음 코드를 추가합니다.

```javascript
const tf = require('@tensorflow/tfjs');
const BayesOptimization = require('bayesopt');

// TODO: implement our hyperparameter tuning experiment
```

설치한 종속성을 요구하는 것으로 시작하겠습니다. 또한 하이퍼파라미터 조정 실험을 구현해야 하는 위치를 상기시키기 위해 TODO 주석을 생성합니다.

## 초매개변수 조정 실험 구현

이제 프로젝트가 설정되었으므로 하이퍼파라미터 튜닝 실험을 구현할 수 있습니다.

최적화하려는 매개변수를 정의하는 것으로 시작하겠습니다. 이 실험에서는 간단한 선형 회귀 모델의 학습률과 배치 크기를 최적화합니다. 또한 각 매개변수에 대해 검색하려는 값의 범위를 정의합니다.

```javascript
const params = {
  learningRate: {
    type: 'float',
    min: 0.0001,
    max: 0.1
  },
  batchSize: {
    type: 'int',
    min: 1,
    max: 100
  }
};
```

다음으로 목적 함수를 정의합니다. 이것이 우리가 최적화할 기능입니다. 이 경우 검증 세트에서 가장 낮은 오류를 발생시키는 하이퍼파라미터의 값을 찾으려고 합니다.

```javascript
const objective = (params, done) => {
  // TODO: implement our objective function
};
```

잠시 후에 목적 함수를 구현할 것입니다. 지금은 정의만 하면 됩니다.

매개변수와 목적 함수가 정의되었으므로 이제 베이지안 최적화 개체를 만들 수 있습니다.

```javascript
const bo = new BayesOptimization(params, objective);
```

이제 목적 함수 최적화를 시작할 수 있습니다. 20회 반복 최적화를 실행하고 기본 수집 기능을 사용합니다(개선 예상).

```javascript
bo.optimize(20, (err, result) => {
  if (err) {
    console.error(err);
  } else {
    console.log(result);
  }
});
```

이제 목적 함수를 구현할 수 있습니다. 먼저 [ Boston 주택 데이터 세트 ](https://archive.ics.uci.edu/ml/datasets/Housing)를 로드하고 훈련 및 검증 세트로 분할합니다.

```javascript
const loadData = () =>
  tf.data.csv('https://archive.ics.uci.edu/ml/machine-learning-databases/housing/housing.data', {
    columnConfigs: {
      medv: {
        isLabel: true
      }
    }
  });

const splitData = (data) =>
  data.shuffle().splitBatch(0.2);
```

다음으로 선형 회귀 모델을 정의합니다.

```javascript
const createModel = () =>
  tf.sequential({
    layers: [
      tf.layers.dense({ inputShape: [13], units: 1 })
    ]
  });
```

이제 목적 함수를 구현할 수 있습니다. `params` 개체에서 하이퍼파라미터 값을 가져오는 것으로 시작하겠습니다.

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;
  // TODO: implement our objective function
};
```

다음으로 데이터를 로드하고 훈련 세트와 검증 세트로 분할합니다.

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      // TODO: implement our objective function
    });
};
```

이제 모델을 생성하고 최적화 중인 하이퍼파라미터로 컴파일할 수 있습니다.

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });
      // TODO: implement our objective function
    });
};
```

마지막으로 모델을 훈련하고 검증 세트에서 평가할 수 있습니다. 유효성 검사 세트에서 평균 제곱 오차를 계산하고 이를 목적 함수의 값으로 반환합니다.

```javascript
const objective = (params, done) => {
  const learningRate = params.learningRate;
  const batchSize = params.batchSize;

  loadData()
    .then(splitData)
    .then(([train, val]) => {
      const model = createModel();
      model.compile({
        loss: 'meanSquaredError',
        optimizer: tf.train.sgd(learningRate)
      });

      model.fit(train, {
        epochs: 10,
        batchSize: batchSize,
        validationData: val,
        callbacks: {
          onEpochEnd: (epoch, logs) => {
            console.log(`Epoch ${epoch}: loss = ${logs.loss}`);
          }
        }
      })
        .then(() => {
          const valLoss = model.evaluate(val);
          console.log(`Validation loss: ${valLoss}`);
          done(null, valLoss);
        });
    });
};
```

그게 다야! 이제 TensorFlow.js 및 Node.js를 사용하여 간단한 하이퍼파라미터 조정 실험을 구현했습니다.

## 결론

이번 포스트에서는 하이퍼파라미터 튜닝을 위해 TensorFlow.js와 Node.js를 사용하는 방법에 대해 알아보았습니다. 베이지안 최적화를 사용하여 간단한 하이퍼파라미터 조정 실험을 구현했습니다.

하이퍼파라미터 튜닝에는 이 게시물에서 다룬 것보다 훨씬 더 많은 것이 있습니다. 더 자세히 알아보려면 다음 리소스를 확인하는 것이 좋습니다.

- [머신러닝에서의 하이퍼파라미터 최적화](https://towardsdatascience.com/hyperparameter-optimization-in-machine-learning-part-1-of-4-cca2b1c265a2)
- [초매개변수 조정에 대한 베이지안 접근법](https://towardsdatascience.com/a-bayesian-approach-to-hyperparameter-tuning-part-1-of-3-c8f8e527e97b)
- [TensorFlow를 사용한 하이퍼파라미터 튜닝](https://medium.com/tensorflow/hyperparameter-tuning-with-tensorflow-part-1-fae4f2bae5e1)