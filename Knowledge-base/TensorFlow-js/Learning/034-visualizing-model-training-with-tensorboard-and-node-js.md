---
title: 034: TensorBoard 및 Node.js로 모델 교육 시각화하기
description: 
published: true
date: 2023-02-02T15:04:26.622Z
tags: 
editor: markdown
dateCreated: 2023-02-02T15:04:25.007Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [034: Visualizing Model Training with TensorBoard and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/034-visualizing-model-training-with-tensorboard-and-node-js)
{.links-list}


---

# 034: TensorBoard 및 Node.js로 모델 교육 시각화하기

TensorBoard는 Google에서 개발한 기계 학습용 시각화 도구 키트입니다. 모델 디버깅 및 최적화에 도움이 될 수 있는 기계 학습 모델의 교육 프로세스를 시각화할 수 있습니다.

이번 포스트에서는 TensorBoard를 Node.js와 함께 사용하는 방법에 대해 알아보겠습니다. TensorBoard를 설치하고 기본 기계 학습 모델을 설정하는 것으로 시작하겠습니다. 그런 다음 TensorBoard를 사용하여 모델의 학습 프로세스를 시각화하는 방법을 배웁니다.

## 텐서보드 설치하기

TensorBoard는 Python 패키지로 제공됩니다. pip 패키지 관리자를 사용하여 설치할 수 있습니다.

```
pip install tensorboard
```

## 기본 기계 학습 모델 설정

TensorFlow.js를 사용하여 기본 기계 학습 모델을 설정합니다. TensorFlow.js는 브라우저에서 기계 학습 모델을 교육하고 배포하기 위한 JavaScript 라이브러리입니다.

먼저 TensorFlow.js를 설치해야 합니다.

```
npm install @tensorflow/tfjs
```

다음으로 간단한 선형 회귀 모델을 설정합니다. tf.sequential() API를 사용하여 모델을 생성합니다.

```javascript
const model = tf.sequential();
```

그런 다음 모델에 하나의 조밀한 레이어를 추가합니다. 조밀한 계층은 완전히 연결된 계층입니다. 즉, 해당 계층의 모든 뉴런이 이전 계층의 모든 뉴런에 연결되어 있습니다.

```javascript
model.add(tf.layers.dense({units: 1, inputShape: [1]}));
```

마지막으로 모델을 컴파일합니다. 모델을 컴파일할 때 옵티마이저와 손실 함수를 지정해야 합니다. 옵티마이저는 훈련 중에 모델의 가중치를 업데이트하는 데 사용됩니다. 손실 함수는 모델이 얼마나 잘 수행되고 있는지 측정하는 데 사용됩니다. 우리는 tf.train.sgd() 옵티마이저와 tf.losses.meanSquaredError() 손실 함수를 사용할 것입니다:

```javascript
model.compile({optimizer: tf.train.sgd(0.001), loss: tf.losses.meanSquaredError});
```

## TensorBoard로 훈련 과정 시각화하기

이제 기계 학습 모델이 설정되었으므로 TensorBoard를 사용하여 교육 프로세스를 시각화할 수 있습니다.

먼저 TensorBoard 콜백을 만들어야 합니다. 콜백은 각 훈련 에포크가 끝날 때 호출되는 함수입니다. tf.tensorBoard() 함수를 사용하여 콜백을 만들 수 있습니다.

```javascript
const tensorBoardCallback = tf.tensorBoard('logdir');
```

다음으로 모델을 교육합니다. tf.fit() 함수를 사용하여 모델을 훈련할 것입니다. 학습 데이터, 학습 에포크 수 및 생성한 TensorBoard 콜백을 지정해야 합니다.

```javascript
model.fit(x, y, {epochs: 100, callbacks: [tensorBoardCallback]});
```

교육이 완료되면 TensorBoard 서버를 시작할 수 있습니다. tensorboard 명령을 사용하여 이를 수행할 수 있습니다. TensorBoard 콜백을 만들 때 지정한 로그 디렉터리를 지정해야 합니다.

```
tensorboard --logdir logdir
```

그러면 TensorBoard 서버가 시작되고 웹 브라우저가 열립니다. 그런 다음 "그래프" 탭으로 이동하여 교육 프로세스의 시각화를 볼 수 있습니다.

![텐서보드 그래프 탭](https://i.imgur.com/rm3kTGi.png)

트레이닝 에포크가 진행됨에 따라 손실이 감소하는 것을 볼 수 있습니다.

## 결론

이 게시물에서는 TensorBoard를 사용하여 기계 학습 모델의 교육 프로세스를 시각화하는 방법을 배웠습니다. TensorBoard를 설치하고 기본 기계 학습 모델을 설정했습니다. 그런 다음 TensorBoard를 사용하여 모델의 학습 프로세스를 시각화했습니다.