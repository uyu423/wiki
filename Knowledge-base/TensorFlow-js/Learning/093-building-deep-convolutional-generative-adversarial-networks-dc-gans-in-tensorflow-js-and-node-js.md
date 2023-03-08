---
title: 093: TensorFlow.js 및 Node.js에서 DC-GAN(Deep Convolutional Generative Adversarial Networks) 구축
description: 
published: true
date: 2023-02-03T04:44:36.919Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:44:35.185Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [093: Building Deep Convolutional Generative Adversarial Networks (DC-GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/093-building-deep-convolutional-generative-adversarial-networks-dc-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 093: TensorFlow.js 및 Node.js에서 DC-GAN(Deep Convolutional Generative Adversarial Networks) 구축

DC-GAN(Deep Convolutional Generative Adversarial Network)은 학습 데이터 세트에서 새 이미지를 생성하는 데 사용되는 GAN(Generative Adversarial Network) 유형입니다.

GAN은 생성기와 판별기의 두 부분으로 구성된 일종의 신경망입니다. Generator는 훈련 데이터와 유사한 새로운 이미지를 생성하고, Discriminator는 Generator가 생성한 실제 훈련 이미지와 가짜 이미지를 구별하려고 합니다.

DC-GAN은 생성자와 판별자 모두에 깊은 컨벌루션 신경망을 사용하는 GAN 유형입니다.

이 튜토리얼에서는 TensorFlow.js와 Node.js를 사용하여 DC-GAN을 구축할 것입니다. 우리는 손으로 쓴 숫자의 데이터 세트인 MNIST 데이터 세트를 사용할 것입니다.

## 시작하기

먼저 TensorFlow.js와 Node.js를 설치해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
npm install -g @tensorflow/tfjs-node
```

다음으로 MNIST 데이터 세트를 다운로드해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
wget http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
```

또한 다운로드한 파일의 압축을 풀어야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
gunzip *
```

## 데이터 전처리

이제 MNIST 데이터셋이 있으므로 DC-GAN에서 사용할 수 있도록 전처리해야 합니다.

먼저 MNIST 데이터셋의 이미지를 DC-GAN에서 사용할 수 있는 형식으로 변환해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' ./mnist_model.h5 ./tfjs_model
```

이 명령은 MNIST 데이터셋을 DC-GAN에서 사용할 수 있는 형식으로 변환합니다.

다음으로 MNIST 데이터 세트를 훈련 세트와 테스트 세트로 분할해야 합니다. 다음 명령을 사용하여 이를 수행할 수 있습니다.

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' --train_test_split=0.8 ./mnist_model.h5 ./tfjs_model
```

이 명령은 MNIST 데이터 세트를 훈련 세트와 테스트 세트로 분할합니다. 트레이닝 세트는 DC-GAN을 훈련하는 데 사용되고 테스트 세트는 DC-GAN을 평가하는 데 사용됩니다.

## DC-GAN 구축

이제 MNIST 데이터 세트가 있으므로 DC-GAN 구축을 시작할 수 있습니다.

먼저 생성기 네트워크를 만들어야 합니다. 생성기 네트워크는 노이즈 벡터를 입력으로 받아 MNIST 데이터 세트와 유사한 이미지를 생성합니다.

다음 코드를 사용하여 생성기 네트워크를 만들 수 있습니다.

```javascript
const generator = tf.sequential();

generator.add(tf.layers.dense({inputShape: [100], units: 7*7*256}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.reshape({targetShape: [7, 7, 256]}));
generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 128,
    strides: 2,
    padding: 'same',
    useBias: false
}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 64,
    strides: 2,
    padding: 'same',
    useBias: false
}));
generator.add(tf.layers.batchNormalization());
generator.add(tf.layers.leakyReLU());

generator.add(tf.layers.conv2dTranspose({
    kernelSize: 5,
    filters: 1,
    strides: 2,
    padding: 'same',
    useBias: false,
    activation: 'tanh'
}));
```

생성기 네트워크는 노이즈 벡터를 입력으로 받아 MNIST 데이터 세트와 유사한 이미지를 생성합니다.

다음으로 판별자 네트워크를 만들어야 합니다. 판별자 네트워크는 이미지를 입력으로 사용하고 이미지가 진짜인지 가짜인지 나타내는 값을 출력합니다.

다음 코드를 사용하여 판별자 네트워크를 만들 수 있습니다.

```javascript
const discriminator = tf.sequential();

discriminator.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 64,
    strides: 2,
    padding: 'same',
    inputShape: [28, 28, 1]
}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dropout({rate: 0.3}));

discriminator.add(tf.layers.conv2d({
    kernelSize: 5,
    filters: 128,
    strides: 2,
    padding: 'same'
}));
discriminator.add(tf.layers.leakyReLU());
discriminator.add(tf.layers.dropout({rate: 0.3}));

discriminator.add(tf.layers.flatten());
discriminator.add(tf.layers.dense({units: 1, activation: 'sigmoid'}));
```

판별자 네트워크는 이미지를 입력으로 사용하고 이미지가 진짜인지 가짜인지 나타내는 값을 출력합니다.

## DC-GAN 교육

생성기 및 판별기 네트워크가 있으므로 이제 DC-GAN 교육을 시작할 수 있습니다.

먼저 손실 함수를 정의해야 합니다. 손실 함수는 DC-GAN이 얼마나 잘 수행되고 있는지 측정하는 데 사용됩니다.

다음 코드를 사용하여 손실 함수를 정의할 수 있습니다.

```javascript
function dLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}

function gLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}
```

손실 함수는 DC-GAN이 얼마나 잘 수행되고 있는지 측정하는 데 사용됩니다.

다음으로 옵티마이저를 정의해야 합니다. 옵티마이저는 생성기 및 판별기 네트워크의 가중치를 업데이트하는 데 사용됩니다.

다음 코드를 사용하여 옵티마이저를 정의할 수 있습니다.

```javascript
const dOptimizer = tf.train.RMSPropOptimizer(0.0003);
const gOptimizer = tf.train.RMSPropOptimizer(0.0001);
```

옵티마이저는 생성기 및 판별기 네트워크의 가중치를 업데이트하는 데 사용됩니다.

이제 DC-GAN 훈련을 시작할 수 있습니다. 우리는 DC-GAN을 100 epoch 동안 학습시킬 것입니다.

다음 코드를 사용하여 DC-GAN을 훈련할 수 있습니다.

```javascript
async function train() {
    for (let i = 0; i < 100; i++) {
        // Train the discriminator
        let dLosses = [];
        for (let j = 0; j < 10; j++) {
            const noise = tf.randomNormal([BATCH_SIZE, 100]);
            const generatedImages = generator.predict(noise);
            const realImages = tf.data.Dataset.fromTensorSlices(images).batch(BATCH_SIZE).take(BATCH_SIZE).toArray();
            const dRealLabels = tf.ones([BATCH_SIZE, 1]);
            const dFakeLabels = tf.zeros([BATCH_SIZE, 1]);
            const dLossReal = dLoss(dRealLabels, discriminator.predict(realImages));
            const dLossFake = dLoss(dFakeLabels, discriminator.predict(generatedImages));
            const dLoss = dLossReal + dLossFake;
            dLosses.push(dLoss);
            dOptimizer.minimize(dLoss);
        }
        const dAvgLoss = tf.mean(dLosses);
        
        // Train the generator
        const noise = tf.randomNormal([BATCH_SIZE, 100]);
        const gLabels = tf.ones([BATCH_SIZE, 1]);
        const gLoss = gLoss(gLabels, discriminator.predict(generator.predict(noise)));
        gOptimizer.minimize(gLoss);
        
        // Log the losses
        if (i % 10 === 0) {
            console.log(`Epoch: ${i}`);
            console.log(`dLoss: ${dLoss.dataSync()[0]}`);
            console.log(`gLoss: ${gLoss.dataSync()[0]}`);
        }
    }
}

train();
```

이 코드는 100 epoch 동안 DC-GAN을 학습시킵니다.

## 새 이미지 생성

이제 DC-GAN이 학습되었으므로 이를 사용하여 새 이미지를 생성할 수 있습니다.

먼저 노이즈 벡터를 생성해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const noise = tf.randomNormal([1, 100]);
```

다음으로 생성기 네트워크를 사용하여 노이즈 벡터에서 새 이미지를 생성해야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```javascript
const generatedImage = generator.predict(noise);
```

마지막으로 다음 코드를 사용하여 생성된 이미지를 시각화할 수 있습니다.

```javascript
const imageTensor = generatedImage.reshape([28, 28]);
const imageData = imageTensor.dataSync();
const canvas = document.createElement('canvas');
canvas.width = 28;
canvas.height = 28;
const ctx = canvas.getContext('2d');
const imageDataArray = Array.from(imageData);
imageDataArray.forEach((value, index) => {
    const i = Math.floor(index / 28);
    const j = index % 28;
    ctx.fillStyle = `rgb(${value}, ${value}, ${value})`;
    ctx.fillRect(j, i, 1, 1);
});
document.body.appendChild(canvas);
```

이 코드는 노이즈 벡터에서 새 이미지를 생성합니다.

## 결론

이 튜토리얼에서는 TensorFlow.js 및 Node.js에서 DC-GAN을 빌드하는 방법을 살펴보았습니다. 또한 DC-GAN을 사용하여 새 이미지를 생성하는 방법도 살펴보았습니다.