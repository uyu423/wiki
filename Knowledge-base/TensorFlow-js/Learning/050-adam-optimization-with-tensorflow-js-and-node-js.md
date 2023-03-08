---
title: 050: TensorFlow.js 및 Node.js를 사용한 Adam 최적화
description: 
published: true
date: 2023-02-02T18:36:28.016Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:36:26.412Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [050: Adam Optimization with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/050-adam-optimization-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 Adam 최적화

이 게시물에서는 TensorFlow.js 및 Node.js와 함께 Adam 최적화 알고리즘을 사용하는 방법을 살펴보겠습니다. Adam은 신경망 훈련에 사용할 수 있는 최적화 알고리즘입니다. Adam은 AdaGrad 및 RMSProp 최적화 알고리즘의 조합입니다.

Adam 최적화는 신경망을 훈련하는 계산적으로 효율적인 방법입니다. Adam은 심층 신경망 훈련에 매우 적합합니다. Adam은 모든 미분 가능한 손실 함수와 함께 사용할 수 있습니다.

## 시작하기

시작하려면 TensorFlow.js 및 Node.js 종속 항목을 설치해야 합니다. 다음 명령을 사용하여 TensorFlow.js 및 Node.js를 설치할 수 있습니다.

```
npm install @tensorflow/tfjs
npm install node
```

## 모델 정의

다음으로 훈련하려는 모델을 정의해야 합니다. 하나의 숨겨진 레이어가 있는 간단한 신경망을 사용합니다. 숨겨진 레이어에는 100개의 뉴런이 있습니다. 다음 코드를 사용하여 모델을 정의할 수 있습니다.

```javascript
const model = tf.sequential();
model.add(tf.layers.dense({units: 100, inputShape: [1], activation: 'relu'}));
model.add(tf.layers.dense({units: 1, activation: 'linear'}));
```

## 모델 컴파일

모델을 정의한 후에는 모델을 컴파일해야 합니다. 모델을 컴파일하면 사용하려는 옵티마이저와 손실 함수를 지정할 수 있습니다. Adam 옵티마이저와 평균 제곱 오류 손실 함수를 사용합니다. 다음 코드를 사용하여 모델을 컴파일할 수 있습니다.

```javascript
model.compile({optimizer: 'adam', loss: 'meanSquaredError'});
```

## 모델 교육

이제 모델을 컴파일했으므로 학습할 수 있습니다. 우리는 10 epoch 동안 모델을 훈련시킬 것입니다. Epoch는 전체 교육 데이터 세트에 대한 하나의 반복입니다. 다음 코드를 사용하여 모델을 훈련할 수 있습니다.

```javascript
model.fit(x, y, {epochs: 10});
```

## 모델 평가

모델이 학습된 후 평가할 수 있습니다. 테스트 데이터 세트에서 모델을 평가합니다. 다음 코드를 사용하여 모델을 평가할 수 있습니다.

```javascript
model.evaluate(xTest, yTest);
```

## 예측하기

마지막으로 훈련된 모델을 사용하여 예측할 수 있습니다. 새로운 데이터 세트에 대한 예측을 할 것입니다. 다음 코드를 사용하여 예측할 수 있습니다.

```javascript
model.predict(xPred);
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js와 함께 Adam 최적화 알고리즘을 사용하는 방법을 살펴보았습니다. Adam은 신경망 훈련에 사용할 수 있는 효율적인 최적화 알고리즘입니다. Adam은 모든 미분 가능한 손실 함수와 함께 사용할 수 있습니다.