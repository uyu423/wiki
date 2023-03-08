---
title: 074：在云提供商上使用 TensorFlow.js 和 Node.js
description: 
published: true
date: 2023-02-03T00:04:39.602Z
tags: 
editor: markdown
dateCreated: 2023-02-03T00:04:37.988Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [074: Using TensorFlow.js with Node.js on Cloud Providers***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/074-using-tensorflow-js-with-node-js-on-cloud-providers)
{.links-list}


# 在云提供商上使用 TensorFlow.js 和 Node.js

TensorFlow.js 是一个强大的 JavaScript 机器学习工具。它可以在 AWS、Azure 和谷歌云平台等云提供商上的 Node.js 应用程序中使用。

在本文中，我们将介绍如何在云提供商上设置 Node.js 应用程序并使用 TensorFlow.js 训练机器学习模型。我们还将把经过训练的模型部署到云提供商，以便它可以在 Web 应用程序中使用。

## 在云提供商上设置 Node.js 应用程序

首先，我们需要在云提供商上设置一个 Node.js 应用程序。我们将使用 Express Web 框架来设置一个基本的 Web 应用程序。

如果您不熟悉 Express，可以查看[入门指南](http://expressjs.com/en/starter/installing.html)。

安装 Express 后，我们可以使用以下代码创建一个名为 app.js 的文件：

```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Hello, world!');
});

app.listen(3000, () => {
  console.log('Example app listening on port 3000!');
});
```

此代码创建一个基本的 Express 应用程序，该应用程序使用“Hello, world!”响应 HTTP 请求。信息。

接下来，我们需要将 Node.js 应用程序部署到云提供商。我们将在此示例中使用 AWS，但其他提供商的流程类似。

首先，创建一个 AWS 账户并创建一个可以访问 EC2 的新 IAM 用户。有关如何执行此操作的更多信息，请参阅 [AWS 文档](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)。

设置 IAM 用户后，您可以创建新的 EC2 实例。对于此示例，我们将使用 t2.micro 实例。

实例运行后，您可以通过 SSH 连接到它并为我们的 Node.js 应用程序安装依赖项：

```
$ sudo npm install -g express
$ sudo npm install -g ejs
```

接下来，我们需要将我们的 `app.js` 文件复制到 EC2 实例。我们可以使用 scp 命令来做到这一点：

```
$ scp -i <path-to-pem-file> app.js ec2-user@<ec2-instance-ip>:~/
```

一旦文件被复制，我们就可以启动我们的 Node.js 应用程序：

```
$ node app.js
```

我们的 Node.js 应用程序现在正在我们的 EC2 实例上运行！

## 将 TensorFlow.js 与 Node.js 结合使用

现在我们已经启动并运行了 Node.js 应用程序，我们可以开始使用 TensorFlow.js。

首先，我们需要安装 TensorFlow.js Node.js 包：

```
$ npm install @tensorflow/tfjs-node
```

接下来，我们将使用以下代码创建一个名为“train.js”的文件：

```javascript
const tf = require('@tensorflow/tfjs-node');

// Define a model for linear regression.
const model = tf.sequential();
model.add(tf.layers.dense({units: 1, inputShape: [1]}));

// Prepare the model for training: Specify the loss and the optimizer.
model.compile({loss: 'meanSquaredError', optimizer: 'sgd'});

// Generate some synthetic data for training.
const xs = tf.tensor2d([1, 2, 3, 4], [4, 1]);
const ys = tf.tensor2d([1, 3, 5, 7], [4, 1]);

// Train the model using the data.
model.fit(xs, ys, {epochs: 10}).then(() => {
  // Use the model to do inference on a data point the model hasn't seen before:
  model.predict(tf.tensor2d([5], [1, 1])).print();
});
```

此代码使用 TensorFlow.js 定义了一个简单的线性回归模型。然后我们使用一些合成数据训练模型。最后，我们使用该模型对新数据点进行预测。

要运行这段代码，我们可以使用 `node` 命令：

```
$ node train.js
```

## 将 TensorFlow.js 模型部署到云提供商

一旦我们有了经过训练的 TensorFlow.js 模型，我们就可以将它部署到云提供商，以便它可以在 Web 应用程序中使用。

在此示例中，我们将再次使用 AWS，但其他提供商的流程类似。

首先，我们需要创建一个 Amazon S3 存储桶来存储我们的模型文件。有关如何执行此操作的更多信息，请参阅 [AWS 文档](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html)。

接下来，我们需要安装 AWS CLI。有关如何执行此操作的更多信息，请参阅 [AWS 文档](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)。

安装 AWS CLI 后，我们可以使用它将本地模型文件同步到我们的 S3 存储桶：

```
$ aws s3 sync . s3://<s3-bucket-name>
```

我们的 TensorFlow.js 模型现已部署到我们的 S3 存储桶中！