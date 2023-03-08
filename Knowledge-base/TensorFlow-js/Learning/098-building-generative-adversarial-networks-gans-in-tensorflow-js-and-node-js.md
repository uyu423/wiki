---
title: 098: TensorFlow.js 및 Node.js에서 생성적 적대 신경망(GAN) 구축
description: 
published: true
date: 2023-02-03T06:04:52.614Z
tags: 
editor: markdown
dateCreated: 2023-02-03T06:04:50.998Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [098: Building Generative Adversarial Networks (GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/098-building-generative-adversarial-networks-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 098: TensorFlow.js 및 Node.js에서 생성적 적대 신경망(GAN) 구축

TensorFlow.js 및 Node.js를 사용하여 생성 모델을 구축하려는 개발자는 GAN(Generative Adversarial Network)을 사용하여 이를 수행할 수 있습니다. 이 게시물에서는 TensorFlow.js 및 Node.js에서 GAN을 구축하는 과정을 안내합니다.

## GAN이 무엇인가요?

GAN은 처음부터 새로운 데이터를 생성하는 데 사용되는 일종의 신경망입니다. 네트워크는 생성기와 판별기의 두 부분으로 구성됩니다. Generator는 새로운 데이터를 생성하는 역할을 하고, Discriminator는 데이터가 진짜인지 가짜인지 판단하는 역할을 합니다.

## TensorFlow.js에서 GAN 구축

GAN 구축의 첫 번째 단계는 `gan.js`라는 새 파일을 만드는 것입니다. `tensorflow` 및 `tfjs-node` 모듈을 요구하는 것으로 시작하겠습니다:

```javascript
const tf = require('tensorflow');
const tfNode = require('tfjs-node');
```

다음으로 생성기 및 판별기 모델을 정의합니다.

```javascript
// Generator
const generator = tf.sequential();
generator.add(tf.layers.dense({units: 100, inputShape: [100]}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());
generator.add(tf.layers.dense({units: 784, activation: 'tanh'}));

// Discriminator
const discriminator = tf.sequential();
discriminator.add(tf.layers.dense({units: 784, inputShape: [784]}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

위의 코드에서 우리는 100차원 노이즈 벡터를 받아들이고 784차원 벡터(예: 28x28 이미지)를 출력하는 생성기를 정의했습니다. 우리는 또한 784차원 벡터를 받아들이고 벡터가 진짜인지 가짜인지를 나타내는 단일 값을 출력하는 판별자를 정의했습니다.

다음으로 모델을 컴파일해야 합니다.

```javascript
// Generator
generator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});

// Discriminator
discriminator.compile({
  optimizer: tf.train.adam(0.0001),
  loss: 'binaryCrossentropy'
});
```

위의 코드에서 학습률이 0.0001인 Adam 옵티마이저를 사용하여 모델을 최적화하도록 지정했습니다. 또한 두 모델의 손실 함수가 이진 교차 엔트로피여야 한다고 지정했습니다.

## GAN 교육

이제 모델을 정의하고 컴파일했으므로 GAN 교육을 시작할 수 있습니다. 학습 프로세스는 판별자 학습과 생성자 학습의 두 단계로 구성됩니다.

### 판별기 훈련

GAN 학습의 첫 번째 단계는 판별자를 학습시키는 것입니다. 생성기를 사용하여 가짜 데이터 배치를 생성하고 교육 데이터 세트를 사용하여 실제 데이터 배치를 생성하여 이를 수행합니다. 그런 다음 이 두 데이터 배치에 대해 판별자를 훈련합니다.

```javascript
// Train the discriminator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of fake data
  const noise = tf.randomNormal([batchSize, 100]);
  const fakeData = generator.predict(noise);

  // Generate a batch of real data
  const realData = tf.data.nextBatch(batchSize, [784]);

  // Train the discriminator
  const xs = tf.concat([fakeData, realData], 0);
  const ys = tf.concat([tf.zeros([batchSize, 1]), tf.ones([batchSize, 1])], 0);
  discriminator.fit(xs, ys);
}
```

위의 코드에서 생성기를 사용하여 가짜 데이터 배치를 생성하고 교육 데이터 세트를 사용하여 실제 데이터 배치를 생성했습니다. 그런 다음 이 두 데이터 배치를 연결하고 판별자를 훈련했습니다.

### 생성기 교육

Discriminator가 학습되었으므로 Generator를 학습할 수 있습니다. 노이즈 벡터 배치를 생성하고 생성기를 통해 전달하여 이를 수행합니다. 그런 다음 이러한 노이즈 벡터에 대해 생성기를 훈련합니다.

```javascript
// Train the generator
for (let i = 0; i < 1000; i++) {
  // Generate a batch of noise vectors
  const noise = tf.randomNormal([batchSize, 100]);

  // Train the generator
  const ys = tf.ones([batchSize, 1]);
  generator.fit(noise, ys);
}
```

위의 코드에서 노이즈 벡터 배치를 생성하고 생성기를 통해 전달했습니다. 그런 다음 이러한 잡음 벡터에 대해 생성기를 훈련했습니다.

## 새 데이터 생성

이제 GAN이 학습되었으므로 이를 사용하여 새 데이터를 생성할 수 있습니다. 이를 위해 잡음 벡터 배치를 생성하고 생성기를 통해 전달합니다.

```javascript
// Generate a batch of noise vectors
const noise = tf.randomNormal([batchSize, 100]);

// Generate new data
const generatedData = generator.predict(noise);
```

위의 코드에서 노이즈 벡터 배치를 생성하고 생성기를 통해 전달했습니다. 이것은 어떤 목적으로든 사용할 수 있는 새로운 데이터 배치를 생성했습니다.