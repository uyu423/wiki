---
title: 092: TensorFlow.js 및 Node.js에서 VAE(Variational Autoencoder) 사용
description: 
published: true
date: 2023-02-03T04:36:31.914Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:36:27.082Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [092: Using Variational Autoencoders (VAEs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/092-using-variational-autoencoders-vaes-in-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js에서 VAE(Variational Autoencoder) 사용

VAE(Variational Autoencoder)는 데이터의 잠재적 표현을 학습하기 위한 강력한 도구입니다. 이 게시물에서는 VAE를 사용하여 TensorFlow.js 및 Node.js에서 MNIST 데이터의 잠재 표현을 학습하는 방법을 살펴보겠습니다.

## VAE란 무엇인가요?

VAE는 데이터의 잠재적 표현을 학습하는 데 사용할 수 있는 확률 모델입니다. VAE는 데이터를 잠재 공간으로 압축하는 방법을 학습한다는 점에서 오토인코더와 유사합니다. 그러나 VAE는 잠재 공간에서 새로운 데이터 샘플을 생성하는 데 사용할 수 있는 확률적 모델입니다.

## VAE는 어떻게 작동하나요?

VAE는 데이터의 잠재적 표현을 학습하여 작동합니다. 잠재 공간은 데이터의 필수 기능을 캡처하는 저차원 공간입니다. 그런 다음 VAE는 이 잠재 공간을 사용하여 새 데이터 샘플을 생성합니다.

## TensorFlow.js에서 VAE를 어떻게 사용하나요?

TensorFlow.js에서 VAE를 사용하려면 먼저 TensorFlow.js 라이브러리를 설치해야 합니다. Node.js 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 MNIST 데이터를 로드해야 합니다. tf.data.Dataset API를 사용하여 이를 수행할 수 있습니다.

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

이제 VAE를 만들어야 합니다. tf.layers.vae() 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

마지막으로 VAE를 교육해야 합니다. fit() 메서드를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## Node.js에서 VAE를 어떻게 사용하나요?

Node.js에서 VAE를 사용하려면 먼저 TensorFlow.js 라이브러리를 설치해야 합니다. Node.js 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

다음으로 MNIST 데이터를 로드해야 합니다. tf.data.Dataset API를 사용하여 이를 수행할 수 있습니다.

```javascript
const mnistData = tf.data.dataset.mnist({
  train: true,
  testData: false
});
```

이제 VAE를 만들어야 합니다. tf.layers.vae() 함수를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
const vae = tf.layers.vae({
  encoder: {
    inputShape: [28, 28, 1],
    latentDimensions: 2
  },
  decoder: {
    outputShape: [28, 28, 1]
  }
});
```

마지막으로 VAE를 교육해야 합니다. fit() 메서드를 사용하여 이 작업을 수행할 수 있습니다.

```javascript
vae.fit(mnistData, {
  epochs: 10
});
```

## 결론

이 게시물에서는 VAE를 사용하여 TensorFlow.js 및 Node.js에서 MNIST 데이터의 잠재 표현을 학습하는 방법을 살펴보았습니다. VAE는 데이터의 잠재적 표현을 학습하기 위한 강력한 도구입니다.