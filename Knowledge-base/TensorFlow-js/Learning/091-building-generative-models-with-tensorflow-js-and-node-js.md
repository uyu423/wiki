---
title: 091: TensorFlow.js 및 Node.js로 생성 모델 구축
description: 
published: true
date: 2023-02-03T04:17:28.503Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:17:26.931Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [091: Building Generative Models with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/091-building-generative-models-with-tensorflow-js-and-node-js)
{.links-list}


# 091: TensorFlow.js 및 Node.js로 생성 모델 구축

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 생성 모델을 빌드하는 방법을 살펴보겠습니다. 생성 모델은 새로운 데이터를 생성하는 방법을 배우기 위한 강력한 도구이며 TensorFlow.js는 JavaScript에서 딥 러닝을 시작하는 좋은 방법입니다.

## 생성 모델이란 무엇입니까?

생성 모델은 새로운 데이터를 생성하는 방법을 학습할 수 있는 일종의 기계 학습 모델입니다. 예를 들어 생성 모델은 새로운 얼굴 이미지 또는 새로운 텍스트 조각을 생성하는 방법을 학습할 수 있습니다.

다양한 유형의 생성 모델이 있지만 가장 인기 있는 유형 중 하나는 GAN(Generative Adversarial Network)입니다. GAN은 생성기와 판별기의 두 부분으로 구성된 일종의 신경망입니다.

Generator는 새로운 데이터를 생성하도록 훈련되고 Discriminator는 실제 데이터와 생성된 데이터를 구별하도록 훈련됩니다. 두 네트워크는 서로 경쟁하며, 훈련을 함에 따라 Generator는 Discriminator를 속이는 데 점점 더 능숙해집니다.

## TensorFlow.js로 생성 모델 구축

생성 모델이 무엇인지 살펴보았으니 이제 TensorFlow.js로 생성 모델을 구축하는 방법을 살펴보겠습니다.

TensorFlow.js를 사용하여 생성 모델을 빌드하는 두 가지 방법이 있습니다. 상위 수준 계층 API를 사용하거나 하위 수준 API를 사용할 수 있습니다.

TensorFlow.js를 이제 막 시작했다면 상위 수준 레이어 API를 사용하는 것이 좋습니다. 레이어 API를 사용하면 단 몇 줄의 코드만으로 모델을 쉽게 구축할 수 있으며 기존 TensorFlow.js 코드와 함께 사용하기 쉽습니다.

레이어 API를 사용하려면 먼저 TensorFlow.js를 설치해야 합니다. npm을 사용하여 이 작업을 수행할 수 있습니다.

```
npm install @tensorflow/tfjs
```

TensorFlow.js가 설치되면 Node.js 프로그램으로 가져올 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs');
```

TensorFlow.js를 설치했으므로 TensorFlow.js를 사용하여 생성 모델을 빌드하는 방법을 살펴보겠습니다.

간단한 생성기 네트워크를 구축하는 것으로 시작하겠습니다. 생성기 네트워크는 노이즈 벡터를 받아 해당 노이즈에서 이미지를 생성합니다.

먼저 노이즈 벡터를 받아 생성기 네트워크를 반환하는 함수를 만들어야 합니다. 레이어 API를 사용하여 생성기 네트워크를 구축합니다.

```javascript
function createGenerator(noise_size) {
  const generator = tf.sequential();

  // First, we'll build a fully connected layer that takes in our noise vector
  // and generates an image from that noise.
  generator.add(tf.layers.dense({
    inputShape: [noise_size],
    units: 7 * 7 * 256,
    useBias: false,
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  // Next, we'll add a batch normalization layer.
  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  // Then, we'll add a Leaky ReLU activation layer.
  generator.add(tf.layers.leakyReLU(0.2));

  // Next, we'll reshape our vector into a 7x7x256 image.
  generator.add(tf.layers.reshape({
    targetShape: [7, 7, 256]
  }));

  // We'll then add a series of convolutional layers.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 256,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 128,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 })
  }));

  generator.add(tf.layers.batchNormalization({
    epsilon: 1e-5,
    momentum: 0.9
  }));

  generator.add(tf.layers.leakyReLU(0.2));

  // Finally, we'll add a convolutional layer that outputs a 28x28x1 image.
  generator.add(tf.layers.conv2dTranspose({
    kernelSize: [3, 3],
    filters: 1,
    strides: [2, 2],
    padding: 'same',
    kernelInitializer: tf.initializers.truncatedNormal({ stddev: 0.02 }),
    activation: 'tanh'
  }));

  // We'll return the generator model.
  return generator;
}
```

이제 생성기 네트워크가 있으므로 이를 사용하여 이미지를 생성하는 방법을 살펴보겠습니다.

먼저 노이즈 벡터를 만들어야 합니다. 무작위 정규 분포를 가진 Tensor를 생성하여 이를 수행할 수 있습니다.

```javascript
const noise = tf.randomNormal([1, 100]);
```

다음으로 생성기 네트워크를 만듭니다.

```javascript
const generator = createGenerator(100);
```

이제 생성기 네트워크가 있으므로 노이즈 벡터에서 이미지를 생성하는 데 사용할 수 있습니다.

```javascript
const generated_image = generator.predict(noise);
```

생성된 이미지는 28x28x1 Tensor입니다. JavaScript 배열로 변환하고 plotly.js 라이브러리를 사용하여 플롯할 수 있습니다.

```javascript
const image_array = generated_image.reshape([28, 28]).arraySync();

const data = [
  {
    z: image_array,
    type: 'heatmap'
  }
];

Plotly.newPlot('generated-image', data);
```

위의 코드를 실행하여 이미지를 생성할 수 있습니다. 다음과 같은 내용이 표시되어야 합니다.

![생성된 이미지](generated-image.png)

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 생성 모델을 빌드하는 방법을 살펴보았습니다. 생성 모델은 새로운 데이터를 생성하는 방법을 배우기 위한 강력한 도구이며 TensorFlow.js는 JavaScript에서 딥 러닝을 시작하는 좋은 방법입니다.