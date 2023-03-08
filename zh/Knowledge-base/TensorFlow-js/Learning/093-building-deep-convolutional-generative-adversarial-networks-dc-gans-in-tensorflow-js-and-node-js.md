---
title: 093：在 TensorFlow.js 和 Node.js 中构建深度卷积生成对抗网络 (DC-GAN)
description: 
published: true
date: 2023-02-03T04:44:37.093Z
tags: 
editor: markdown
dateCreated: 2023-02-03T04:44:35.186Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [093: Building Deep Convolutional Generative Adversarial Networks (DC-GANs) in TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/093-building-deep-convolutional-generative-adversarial-networks-dc-gans-in-tensorflow-js-and-node-js)
{.links-list}


# 093：在 TensorFlow.js 和 Node.js 中构建深度卷积生成对抗网络 (DC-GAN)

深度卷积生成对抗网络 (DC-GAN) 是一种生成对抗网络 (GAN)，用于从训练数据集生成新图像。

GAN 是一种神经网络，由两部分组成：生成器和鉴别器。生成器创建与训练数据相似的新图像，而鉴别器则试图区分真实的训练图像和生成器生成的假图像。

DC-GAN 是一种 GAN，它对生成器和鉴别器都使用深度卷积神经网络。

在本教程中，我们将使用 TensorFlow.js 和 Node.js 构建 DC-GAN。我们将使用 MNIST 数据集，这是一个手写数字数据集。

## 入门

首先，我们需要安装 TensorFlow.js 和 Node.js。我们可以使用以下命令执行此操作：

```
npm install -g @tensorflow/tfjs-node
```

接下来，我们需要下载 MNIST 数据集。我们可以使用以下命令执行此操作：

```
wget http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz
wget http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz
```

我们还需要解压缩下载的文件。我们可以使用以下命令执行此操作：

```
gunzip *
```

## 预处理数据

现在我们有了 MNIST 数据集，我们需要对其进行预处理，以便它可以被 DC-GAN 使用。

首先，我们需要将 MNIST 数据集中的图像转换为 DC-GAN 可以使用的格式。我们可以使用以下命令执行此操作：

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' ./mnist_model.h5 ./tfjs_model
```

此命令会将 MNIST 数据集转换为 DC-GAN 可以使用的格式。

接下来，我们需要将 MNIST 数据集拆分为训练集和测试集。我们可以使用以下命令执行此操作：

```
tensorflowjs_converter --input_format=tfjs-layers-model --output_format=tfjs-layers-model --output_node_names='input,output' --train_test_split=0.8 ./mnist_model.h5 ./tfjs_model
```

此命令会将 MNIST 数据集拆分为训练集和测试集。训练集将用于训练 DC-GAN，而测试集将用于评估 DC-GAN。

## 构建 DC-GAN

现在我们有了 MNIST 数据集，我们可以开始构建 DC-GAN。

首先，我们需要创建生成器网络。生成器网络将噪声向量作为输入，并生成类似于 MNIST 数据集的图像。

我们可以使用以下代码创建生成器网络：

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

生成器网络将噪声向量作为输入并生成类似于 MNIST 数据集的图像。

接下来，我们需要创建鉴别器网络。鉴别器网络将图像作为输入，并输出一个值来指示图像是真实的还是假的。

我们可以使用以下代码创建鉴别器网络：

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

鉴别器网络将图像作为输入并输出一个值，该值指示图像是真实的还是假的。

## 训练 DC-GAN

现在我们有了生成器和鉴别器网络，我们可以开始训练 DC-GAN。

首先，我们需要定义损失函数。损失函数用于衡量 DC-GAN 的表现。

我们可以使用以下代码定义损失函数：

```javascript
function dLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}

function gLoss(yTrue, yPred) {
    return tf.losses.sigmoidCrossEntropy(yTrue, yPred);
}
```

损失函数用于衡量 DC-GAN 的表现。

接下来，我们需要定义优化器。优化器用于更新生成器和鉴别器网络的权重。

我们可以使用以下代码定义优化器：

```javascript
const dOptimizer = tf.train.RMSPropOptimizer(0.0003);
const gOptimizer = tf.train.RMSPropOptimizer(0.0001);
```

优化器用于更新生成器和鉴别器网络的权重。

现在，我们可以开始训练 DC-GAN。我们将训练 DC-GAN 100 个时期。

我们可以使用以下代码训练 DC-GAN：

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

此代码将训练 DC-GAN 100 个时期。

## 生成新图像

现在 DC-GAN 已经训练完毕，我们可以用它来生成新图像。

首先，我们需要生成一个噪声向量。我们可以使用以下代码来做到这一点：

```javascript
const noise = tf.randomNormal([1, 100]);
```

接下来，我们需要使用生成器网络从噪声向量生成新图像。我们可以使用以下代码来做到这一点：

```javascript
const generatedImage = generator.predict(noise);
```

最后，我们可以使用以下代码可视化生成的图像：

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

此代码将从噪声向量生成新图像。

## 结论

在本教程中，我们了解了如何在 TensorFlow.js 和 Node.js 中构建 DC-GAN。我们还看到了如何使用 DC-GAN 生成新图像。