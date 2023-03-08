---
title: 如何使用 Microsoft Bot Framework 构建聊天机器人
description: 
published: true
date: 2023-02-12T09:17:32.252Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:17:30.474Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Build a Chatbot with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-chatbot-with-microsoft-bot-framework)
{.links-list}


# 如何使用 Microsoft Bot Framework 构建聊天机器人

开发聊天机器人似乎是一项艰巨的任务，但使用 Microsoft Bot Framework 可以轻松有趣！在本文中，我们将介绍开始构建您自己的聊天机器人所需了解的所有内容。

## 什么是聊天机器人？

聊天机器人是一种模拟人类对话的计算机程序。聊天机器人用于各种行业，包括客户服务、营销，甚至医疗保健。

## 为什么要构建聊天机器人？

聊天机器人可以成为改善客户服务或帮助人们查找信息的好方法。它们也可以用于营销，甚至只是为了好玩！

## 构建聊天机器人需要什么？

要构建聊天机器人，您需要一台可以连接互联网的计算机和一个文本编辑器。您还需要一个 Microsoft 帐户。如果您没有，可以免费创建一个。

## 如何构建聊天机器人？

构建聊天机器人的主要方法有两种：使用 Bot Framework 工具或使用 Azure Bot Service。

### 使用 Bot Framework 工具

Bot Framework 工具是开始构建聊天机器人的绝佳方式。它们包含您入门所需的一切，包括 Bot Builder SDK 和 CLI。

首先，为您的聊天机器人项目创建一个新文件夹。然后，在文本编辑器中打开该文件夹并创建一个名为“app.js”的文件。

接下来，您需要安装 Bot Builder SDK。您可以使用 npm 执行此操作：

```
npm install botbuilder
```

安装 SDK 后，您可以将其导入到您的 `app.js` 文件中：

```js
const builder = require('botbuilder');
```

现在您可以开始编码了！

首先，您需要创建一个机器人适配器。这将用于将您的聊天机器人连接到 Microsoft Bot Framework。您可以使用以下代码执行此操作：

```js
const adapter = new builder.BotFrameworkAdapter();
```

接下来，您需要创建一个机器人处理程序。这将用于处理来自用户的传入消息。您可以使用以下代码执行此操作：

```js
const bot = new builder.UniversalBot(adapter);
```

现在您已准备好开始向您的机器人处理程序添加代码！

您需要做的第一件事是定义一个“WelcomeMessage”对话框。此对话框将用于问候用户并开始使用。您可以使用以下代码执行此操作：

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

如您所见，此对话框将向用户发送一条消息，然后启动“GetName”对话框。

`GetName` 对话框将用于获取用户名。您可以使用以下代码执行此操作：

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

如您所见，此对话框将提示用户输入他们的姓名，然后将响应存储在名为“results.response”的变量中。然后它将结束对话并向用户发送一条包含他们姓名的消息。

现在您已准备好测试您的聊天机器人！为此，您需要运行以下命令：

```
node app.js
```

这将启动你的聊天机器人，你现在可以和它交谈了！试着说“你好”或“你叫什么名字？”看看它做了什么。

### 使用 Azure 机器人服务

Azure 机器人服务是构建和部署聊天机器人的绝佳方式。它包含您入门所需的一切，包括 Bot Builder SDK 和 CLI。

首先，为您的聊天机器人项目创建一个新文件夹。然后，在文本编辑器中打开该文件夹并创建一个名为“app.js”的文件。

接下来，您需要安装 Bot Builder SDK。您可以使用 npm 执行此操作：

```
npm install botbuilder
```

安装 SDK 后，您可以将其导入到您的 `app.js` 文件中：

```js
const builder = require('botbuilder');
```

现在您可以开始编码了！

首先，您需要创建一个机器人适配器。这将用于将您的聊天机器人连接到 Microsoft Bot Framework。您可以使用以下代码执行此操作：

```js
const adapter = new builder.BotFrameworkAdapter();
```

接下来，您需要创建一个机器人处理程序。这将用于处理来自用户的传入消息。您可以使用以下代码执行此操作：

```js
const bot = new builder.UniversalBot(adapter);
```

现在您已准备好开始向您的机器人处理程序添加代码！

您需要做的第一件事是定义一个“WelcomeMessage”对话框。此对话框将用于问候用户并开始使用。您可以使用以下代码执行此操作：

```js
bot.dialog('WelcomeMessage', [
    (session) => {
        session.send("Hello! I'm a chatbot.");
        session.beginDialog('GetName');
    },
]);
```

如您所见，此对话框将向用户发送一条消息，然后启动“GetName”对话框。

`GetName` 对话框将用于获取用户名。您可以使用以下代码执行此操作：

```js
bot.dialog('GetName', [
    (session) => {
        builder.Prompts.text(session, "What's your name?");
    },
    (session, results) => {
        session.endDialog(`Hello, ${results.response}!`);
    },
]);
```

如您所见，此对话框将提示用户输入他们的姓名，然后将响应存储在名为“results.response”的变量中。然后它将结束对话并向用户发送一条包含他们姓名的消息。

现在您已准备好测试您的聊天机器人！为此，您需要运行以下命令：

```
node app.js
```

这将启动你的聊天机器人，你现在可以和它交谈了！试着说“你好”或“你叫什么名字？”看看它做了什么。

## 资源

- [微软机器人框架](https://dev.botframework.com/)
- [Azure 机器人服务](https://azure.microsoft.com/en-us/services/bot-service/)
- [机器人生成器 SDK](https://docs.microsoft.com/en-us/javascript/api/botbuilder-core/botbuilder-core-sdk?view=botbuilder-js-stable)