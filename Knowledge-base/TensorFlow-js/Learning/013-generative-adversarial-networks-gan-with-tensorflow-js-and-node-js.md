---
title: 013: TensorFlow.js 및 Node.js를 사용한 GAN(Generative Adversarial Networks)
description: 
published: true
date: 2023-02-02T09:44:15.358Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:44:13.592Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [013: Generative Adversarial Networks (GAN) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/013-generative-adversarial-networks-gan-with-tensorflow-js-and-node-js)
{.links-list}


# TensorFlow.js 및 Node.js를 사용한 생성적 적대 신경망(GAN)

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 GAN(Generative Adversarial Network)을 만드는 방법을 살펴보겠습니다. 우리는 GAN을 사용하여 MNIST 데이터 세트를 기반으로 손으로 쓴 숫자의 새로운 이미지를 생성할 것입니다.

## GAN이란?

GAN은 생성 모델링에 사용되는 일종의 신경망입니다. 생성 모델링은 훈련 데이터와 유사한 새로운 데이터를 생성하는 것이 목표인 기계 학습의 작업입니다.

GAN은 두 개의 신경망인 생성기와 판별기로 구성됩니다. 생성기 네트워크는 노이즈를 입력으로 받아 훈련 데이터와 유사한 이미지를 생성합니다. Discriminator 네트워크는 이미지를 입력으로 사용하여 실제 또는 가짜로 분류하려고 시도합니다.

생성기 및 판별기 네트워크는 제로섬 게임에서 함께 훈련됩니다. 여기서 생성기의 목표는 생성된 이미지가 실제라고 생각하도록 판별기를 속이는 것이며 판별기의 목표는 이미지를 실제 또는 실제 이미지로 올바르게 분류하는 것입니다. 또는 가짜.

## 프로젝트 설정

GAN 교육을 시작하기 전에 프로젝트를 설정해야 합니다. 다음 라이브러리를 사용할 것입니다.

- [TensorFlow.js](https://js.tensorflow.org/)
- [노드 가져오기](https://www.npmjs.com/package/node-fetch)
- [@tensorflow/tfjs-node](https://www.npmjs.com/package/@tensorflow/tfjs-node)

npm을 사용하여 다음 라이브러리를 설치할 수 있습니다.

```
npm install tensorflowjs node-fetch @tensorflow/tfjs-node
```

## MNIST 데이터셋 로드

우리는 GAN에 MNIST 데이터 세트를 사용할 것입니다. MNIST 데이터 세트는 각각 28x28 그레이스케일 이미지로 표현되는 손으로 쓴 숫자 모음입니다.

node-fetch 라이브러리를 사용하여 TensorFlow.js Datasets 저장소에서 MNIST 데이터세트를 로드할 수 있습니다.

```javascript
const tf = require('@tensorflow/tfjs-node');
const fetch = require('node-fetch');

// Load the MNIST dataset from the TensorFlow.js Datasets repository.
const mnistDataset = await tf.data.web('https://storage.googleapis.com/tfjs-datasets/mnist.json');
```

## MNIST 데이터셋 전처리

MNIST 데이터 세트를 로드한 후에는 GAN 교육에 사용할 수 있도록 사전 처리해야 합니다.

먼저 28x28 그레이스케일 이미지를 32x32 RGB 이미지로 변환합니다. 또한 픽셀 값을 [-1, 1] 범위에 있도록 정규화합니다.

```javascript
// Convert the 28x28 grayscale images into 32x32 RGB images.
const mnistImages = mnistDataset.images.map(image => tf.image.resizeBilinear(image, [32, 32]));

// Normalize the pixel values to be in the range [-1, 1].
const mnistImages = mnistImages.map(image => image.toFloat().div(tf.scalar(255)).sub(tf.scalar(1)));
```

## 제너레이터 네트워크 생성

이제 MNIST 데이터셋을 사전 처리했으므로 GAN 생성을 시작할 수 있습니다.

먼저 제너레이터 네트워크를 생성합니다. 생성기 네트워크는 노이즈 벡터를 입력으로 사용하고 훈련 데이터와 유사한 이미지를 생성합니다.

100차원의 노이즈 벡터를 사용합니다. tf.layers.dense 레이어를 사용하여 노이즈 벡터를 32x32x3 크기의 이미지에 매핑합니다.

```javascript
// Create the generator network.
const generator = tf.sequential();

// Map the noise vector to an image with 32x32x3 dimensions.
generator.add(tf.layers.dense({inputShape: [100], units: 32 * 32 * 3}));
generator.add(tf.layers.reshape({targetShape: [32, 32, 3]}));
```

## 판별자 네트워크 만들기

다음으로 판별자 네트워크를 만듭니다. Discriminator 네트워크는 이미지를 입력으로 사용하여 실제 또는 가짜로 분류하려고 시도합니다.

tf.layers.conv2d 레이어를 사용하여 판별자를 위한 컨볼루션 신경망을 생성합니다. 또한 tf.layers.leakyReLU 계층을 사용하여 네트워크에 비선형성을 추가합니다.

```javascript
// Create the discriminator network.
const discriminator = tf.sequential();

// Add a convolutional layer.
discriminator.add(tf.layers.conv2d({inputShape: [32, 32, 3], filters: 16, kernelSize: 3, strides: 2, padding: 'same'}));

// Add a Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add another convolutional layer.
discriminator.add(tf.layers.conv2d({filters: 32, kernelSize: 3, strides: 2, padding: 'same'}));

// Add another Leaky ReLU layer.
discriminator.add(tf.layers.leakyReLU());

// Add a flatten layer.
discriminator.add(tf.layers.flatten());

// Add a fully connected layer.
discriminator.add(tf.layers.dense({units: 1}));

// Add a sigmoid activation layer.
discriminator.add(tf.layers.activation({activation: 'sigmoid'}));
```

## GAN 교육

이제 생성기 및 판별기 네트워크를 만들었으므로 GAN을 훈련할 수 있습니다.

먼저 생성자와 판별자 네트워크를 결합하는 GAN 모델을 만듭니다.

다음으로 tf.train.adamOptimizer 옵티마이저를 사용하여 GAN 모델을 컴파일합니다.

마지막으로 tf.train.ganTrain() 메서드를 사용하여 GAN 모델을 훈련합니다.

```javascript
// Create a GAN model that combines the generator and discriminator.
const gan = tf.sequential();

// Add the generator to the GAN.
gan.add(generator);

// Freeze the generator.
generator.trainable = false;

// Add the discriminator to the GAN.
gan.add(discriminator);

// Compile the GAN using the Adam optimizer.
gan.compile({loss: 'binaryCrossentropy', optimizer: tf.train.adamOptimizer()});

// Train the GAN.
for (let i = 0; i < 100; i++) {
  // Get a batch of real images.
  const realImages = mnistImages.slice(i * 10, (i + 1) * 10);

  // Generate a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);

  // Create a batch of labels for the real and fake images.
  const realLabels = tf.ones([10, 1]);
  const fakeLabels = tf.zeros([10, 1]);

  // Train the discriminator on the real and fake images.
  const loss = await gan.fit([realImages, fakeImages], [realLabels, fakeLabels], {
    epochs: 1,
    batchSize: 10
  });

  // Generate and show a batch of fake images.
  const noise = tf.randomNormal([10, 100]);
  const fakeImages = generator.predict(noise);
  fakeImages.forEach((image, i) => {
    const canvas = document.createElement('canvas');
    canvas.width = 28;
    canvas.height = 28;
    const ctx = canvas.getContext('2d');
    const imageData = new ImageData(28, 28);
    const data = image.dataSync();
    for (let j = 0; j < 28 * 28; j++) {
      const k = j * 4;
      const imgIdx = j;
      imageData.data[k + 0] = (data[imgIdx + 0] + 1) * 127;
      imageData.data[k + 1] = (data[imgIdx + 1] + 1) * 127;
      imageData.data[k + 2] = (data[imgIdx + 2] + 1) * 127;
      imageData.data[k + 3] = 255;
    }
    ctx.putImageData(imageData, 0, 0);
    document.body.appendChild(canvas);
  });
}
```

## 새 이미지 생성

GAN이 학습되면 이를 사용하여 새 이미지를 생성할 수 있습니다.

먼저 100차원의 노이즈 벡터를 생성합니다.

다음으로 생성기 네트워크를 사용하여 노이즈 벡터에서 이미지를 생성합니다.

마지막으로 생성된 이미지를 화면에 표시합니다.

```javascript
// Generate a noise vector with 100 dimensions.
const noise = tf.randomNormal([1, 100]);

// Use the generator to generate an image from the noise vector.
const generatedImage = generator.predict(noise);

// Show the generated image.
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageData = new ImageData(28, 28);
const data = generatedImage.dataSync();
for (let i = 0; i < 28 * 28; i++) {
  const j = i * 4;
  const imgIdx = i;
  imageData.data[j + 0] = (data[imgIdx + 0] + 1) * 127;
  imageData.data[j + 1] = (data[imgIdx + 1] + 1) * 127;
  imageData.data[j + 2] = (data[imgIdx + 2] + 1) * 127;
  imageData.data[j + 3] = 255;
}
ctx.putImageData(imageData, 0, 0);
document.body.appendChild(canvas);
```

## 결론

이 게시물에서는 TensorFlow.js 및 Node.js를 사용하여 GAN을 생성하는 방법을 살펴보았습니다. 또한 GAN을 사용하여 손으로 쓴 숫자의 새 이미지를 생성하는 방법도 살펴보았습니다.

GAN에 대해 자세히 알아보려면 다음 리소스를 추천합니다.

- [Generative Adversarial Networks](https://arxiv.org/abs/1406.2661) (연구 논문)
- [자바스크립트를 이용한 딥러닝](https://www.manning.com/livevideo/deep-learning-with-javascript)(동영상 강좌)
- [TensorFlow의 Generative Adversarial Networks](https://www.tensorflow.org/tutorials/generative/gan)(튜토리얼)