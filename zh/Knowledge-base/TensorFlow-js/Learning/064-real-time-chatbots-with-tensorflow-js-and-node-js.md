---
title: 064：使用 TensorFlow.js 和 Node.js 的实时聊天机器人
description: 
published: true
date: 2023-02-02T22:04:38.052Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:04:36.502Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [064: Real-Time Chatbots with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/064-real-time-chatbots-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的实时聊天机器人

在本文中，我们将研究如何使用 TensorFlow.js 和 Node.js 创建实时聊天机器人。我们将使用预先训练的模型来构建我们的聊天机器人，并将其部署在无服务器平台上，以便它可以处理多个并发用户。

## 什么是聊天机器人？

聊天机器人是一种模拟人类对话的计算机程序。聊天机器人用于各种环境，包括客户服务、营销和娱乐。

## 为什么使用 TensorFlow.js？

TensorFlow.js 是一个用于训练和部署机器学习模型的 JavaScript 库。它是开源和跨平台的，可以在浏览器或 Node.js 环境中使用。

## 什么是 Node.js？

Node.js 是一个 JavaScript 运行时环境，使您能够在浏览器之外运行 JavaScript 代码。 Node.js 用于开发服务器端应用程序。

## 先决条件

这篇文章假设您对 JavaScript 和 Node.js 有基本的了解。如果您不熟悉这些技术，您可能需要查看以下资源：

- [JavaScript 教程](https://www.w3schools.com/js/)
- [Node.js 教程](https://nodejs.org/en/docs/guides/getting-started-guide/)

## 入门

### 1.新建一个Node.js项目

让我们从创建一个新的 Node.js 项目开始。我们将使用 [Express](https://expressjs.com/) 网络框架，因此请务必安装它：

```
npm init
npm install express --save
```

### 2.训练你的模型

接下来，我们需要训练一个可供我们的聊天机器人使用的机器学习模型。在这篇博文中，我们将使用来自 [TensorFlow.js Model Zoo](https://js.tensorflow.org/tutorials/training-chatbot.html) 的预训练模型。

您可以训练自己的模型或使用预训练模型。如果您想训练自己的模型，则需要提供对话数据的数据集。 TensorFlow.js Model Zoo 提供了几个不同的数据集供您使用。

选择数据集后，您可以使用 [TensorFlow.js Model Maker](https://js.tensorflow.org/tutorials/model-maker.html) 来训练您的模型。

### 3.部署你的模型

现在我们有了一个经过训练的模型，我们需要部署它，以便我们的聊天机器人可以使用它。为此，我们将使用 [TensorFlow.js 模型服务器](https://js.tensorflow.org/tutorials/serving-models.html)。

TensorFlow.js 模型服务器是一个可以部署在任何平台上的 Node.js 应用程序。它使您能够为 TensorFlow.js 模型提供服务，并提供用于推理的 REST API。

### 4. 实现你的聊天机器人

现在我们的模型已经部署好了，我们可以开始实施我们的聊天机器人了。我们将使用 [Botkit](https://botkit.ai/) 库来执行此操作。

Botkit 是一个 Node.js 库，可以轻松地为 Slack、Facebook Messenger 和其他聊天平台创建机器人。

首先，我们需要安装 Botkit：

```
npm install botkit --save
```

然后，我们可以创建一个名为 `chatbot.js` 的文件并添加以下代码：

```javascript
const Botkit = require('botkit');

const controller = Botkit.slackbot({
  debug: false,
});

controller.spawn({
  token: process.env.SLACK_BOT_TOKEN,
}).startRTM();

controller.hears('hello', ['direct_message', 'direct_mention', 'mention'], (bot, message) => {
  bot.reply(message, 'Hi there!');
});
```

此代码创建一个响应“hello”命令的 Slack 机器人。

### 5.部署你的聊天机器人

现在我们的聊天机器人已经实现，我们需要部署它。为此，我们将使用 [Now](https://zeit.co/now)。

Now 是一个无服务器平台，可以轻松部署 Node.js 应用程序。它负责基础架构，因此您可以专注于您的代码。

首先，我们需要创建一个 Now 帐户并安装 Now CLI：

```
npm install -g now
```

然后，我们可以使用以下命令部署我们的聊天机器人：

```
now --env SLACK_BOT_TOKEN=your-bot-token
```

这将部署我们的聊天机器人并为我们提供可用于访问它的 URL。

## 结论

在本文中，我们了解了如何使用 TensorFlow.js 和 Node.js 创建实时聊天机器人。我们已经训练了一个机器学习模型并将其部署在无服务器平台上。我们还使用 Botkit 库实现了一个聊天机器人。