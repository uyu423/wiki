---
title: 062：使用 TensorFlow.js 和 Node.js 进行实时图像分类
description: 
published: true
date: 2023-02-02T21:36:45.177Z
tags: 
editor: markdown
dateCreated: 2023-02-02T21:36:43.516Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [062: Real-Time Image Classification with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/062-real-time-image-classification-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 进行实时图像分类

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 构建实时图像分类应用程序。

TensorFlow.js 是一个用 JavaScript 创建机器学习模型的强大工具。 Node.js 是一个 JavaScript 运行时，允许您在服务器上运行 JavaScript。

 这两种技术可以一起用于构建强大的实时图像分类应用程序。

## 安装 TensorFlow.js

第一步是安装 TensorFlow.js。您可以使用节点包管理器 (NPM) 执行此操作：

```
npm install @tensorflow/tfjs
```

## 安装 Node.js

如果您尚未安装 Node.js，可以按照 Node.js 网站上的说明进行安装：https://nodejs.org/en/

## 构建模型

现在我们已经安装了 TensorFlow.js 和 Node.js，我们可以开始构建我们的图像分类模型了。

我们将使用 MobileNet 模型。 MobileNet 是一种预训练模型，已在大型图像数据集上进行训练。

要使用 MobileNet 模型，我们首先需要将其加载到 TensorFlow.js 中：

```javascript
const tf = require('@tensorflow/tfjs');

const mobilenet = require('@tensorflow-models/mobilenet');

async function loadModel() {
  const model = await mobilenet.load();
  return model;
}
```

加载模型后，我们可以使用它对图像进行分类。

下面的 classifyImage() 函数将图像作为输入并返回前 5 个预测：

```javascript
async function classifyImage(image) {
  const model = await loadModel();
  const predictions = await model.classify(image);
  return predictions;
}
```

## 服务模型

现在我们已经构建了图像分类模型，我们需要使用 Node.js 为其提供服务。

我们将使用 Express 网络框架。 Express 是一个流行的 Node.js Web 框架。

要安装 Express，请运行以下命令：

```
npm install express
```

安装 Express 后，我们可以创建一个名为 server.js 的文件并添加以下代码：

```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/classify', async (req, res) => {
  const image = req.query.image;
  const predictions = await classifyImage(image);
  res.json(predictions);
});

app.listen(3000, () => console.log('Server listening on port 3000!'));
```

上面的代码执行以下操作：

- 从公共目录提供静态文件
- 创建一个将图像 URL 作为查询参数的端点 (/classify)
- 使用 classifyImage() 函数对图像进行分类
- 以 JSON 形式返回前 5 个预测

## 构建前端

现在我们已经启动并运行了 Node.js 服务器，我们可以开始构建应用程序的前端了。

我们将使用 React。 React 是一个流行的 JavaScript 库，用于构建用户界面。

要安装 React，请运行以下命令：

```
npm install react react-dom
```

安装 React 后，我们可以创建一个名为 App.js 的文件并添加以下代码：

```javascript
import React, { useState, useEffect } from 'react';
import './App.css';

function App() {
  const [image, setImage] = useState(null);
  const [predictions, setPredictions] = useState([]);

  useEffect(() => {
    async function fetchPredictions() {
      const response = await fetch('/classify?image=' + image);
      const predictions = await response.json();
      setPredictions(predictions);
    }
    if (image) {
      fetchPredictions();
    }
  }, [image]);

  const onSelectFile = e => {
    if (e.target.files && e.target.files.length > 0) {
      const reader = new FileReader();
      reader.onload = () => setImage(reader.result);
      reader.readAsDataURL(e.target.files[0]);
    }
  };

  return (
    <div className="App">
      <h1>Real-Time Image Classification</h1>
      <p>
        Select an image to classify:
      </p>
      <input type="file" accept="image/*" onChange={onSelectFile} />
      {predictions.length > 0 && (
        <div className="predictions">
          <h2>Predictions</h2>
          {predictions.map((prediction, i) => (
            <div key={i}>
              <div className="prediction-label">{prediction.className}</div>
              <div className="prediction-confidence">{prediction.probability.toFixed(2)}</div>
            </div>
          ))}
        </div>
      )}
    </div>
  );
}

export default App;
```

上面的代码执行以下操作：

- 呈现一个文件输入字段，允许用户选择图像
- 选择图像后，将图像上传到服务器并获取预测
- 然后将预测显示在页面上

## 运行应用程序

现在我们已经完成了前端和后端代码，我们可以运行应用程序了。

首先，通过运行以下命令启动 Node.js 服务器：

```
node server.js
```

然后，在浏览器中打开以下 URL：http://localhost:3000

您现在应该看到图像分类应用程序已启动并正在运行！