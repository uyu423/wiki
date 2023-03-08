---
title: 使用 Microsoft Bot Framework 开发聊天机器人
description: 
published: true
date: 2023-02-12T19:18:22.601Z
tags: 
editor: markdown
dateCreated: 2023-02-12T19:18:20.743Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Developing Chatbots with Microsoft Bot Framework***English** document is available*](/en/Knowledge-base/Common/developing-chatbots-with-microsoft-bot-framework)
{.links-list}


# 使用 Microsoft Bot Framework 开发聊天机器人

随着越来越多的企业寻求自动化客户交互的方法，开发聊天机器人已成为 IT 行业的热门话题。 Microsoft Bot Framework 是构建聊天机器人的领先平台之一，它提供了一组易于使用的工具和服务，允许开发人员创建能够以自然方式与用户交互的机器人。

在本文中，我们将了解如何使用 Microsoft Bot Framework 开发聊天机器人。我们将从查看框架的不同组件以及它们如何协同工作开始。然后我们将深入研究一些代码示例，向您展示如何开始构建您自己的聊天机器人。

## 什么是 Microsoft Bot 框架？

Microsoft Bot Framework 是一组工具和服务，可帮助开发人员为各种平台构建聊天机器人，包括 Facebook Messenger、Skype、Slack 等。该框架包括一个 Bot Builder SDK，它提供了一组用于构建机器人的 API，以及一组用于管理机器人对话的工具和服务。

Bot Builder SDK 允许开发人员创建可以理解自然语言的机器人。该 SDK 包括一组用于构建机器人的工具，包括对话系统、一组自然语言处理工具和一组用于管理机器人对话的工具。

该 SDK 还包括一组 API，用于将机器人与各种服务集成，包括 Facebook Messenger、Skype、Slack 等。

## Microsoft Bot 框架的工作原理

Microsoft Bot Framework 的工作原理是允许开发人员创建能够理解自然语言的机器人。该框架包括一组用于构建机器人的工具，包括对话系统、一组自然语言处理工具和一组用于管理机器人对话的工具。

该框架还包括一组 API，用于将机器人与各种服务集成，包括 Facebook Messenger、Skype、Slack 等。

## 开始使用 Microsoft Bot 框架

现在我们已经了解了 Microsoft Bot Framework 是什么以及它是如何工作的，让我们从一些代码示例开始吧。

您需要做的第一件事是创建一个新的 Microsoft Bot Framework 项目。您可以使用 Microsoft Bot Framework Yeoman 生成器执行此操作。

要安装生成器，您需要在计算机上安装 Node.js 和 Yeoman。要安装 Node.js，请前往 Node.js 网站并下载适用于您的操作系统的安装程序。

安装 Node.js 后，您可以使用以下命令安装 Yeoman 生成器：

```
npm install -g yo generator-botframework
```

安装生成器后，您可以使用以下命令创建一个新项目：

```
yo botframework
```

系统将提示您输入有关项目的一些详细信息，包括名称、描述和版本。

生成项目后，您需要安装依赖项。为此，请转到项目目录并运行以下命令：

```
npm install
```

安装依赖项后，您就可以开始开发聊天机器人了。

## 开发你的聊天机器人

Microsoft Bot Framework 附带一组工具和服务，可以轻松开发聊天机器人。在本节中，我们将了解如何使用框架的不同组件来开发聊天机器人。

### 机器人生成器 SDK

Bot Builder SDK 是一组工具，可让您构建能够理解自然语言的机器人。该 SDK 包括一个对话系统、一组自然语言处理工具和一组用于管理机器人对话的工具。

要开始使用 SDK，您需要在项目的根目录中创建一个新文件。该文件应命名为“bot.js”。

在 `bot.js` 文件中，您需要需要 `botbuilder` 模块并创建一个新的 `BotBuilder` 实例。

```javascript
var builder = require('botbuilder');

var bot = new builder.BotBuilder();
```

### 对话系统

对话系统是 Bot Builder SDK 的核心。它允许您定义用户和聊天机器人之间的对话流程。

对话系统基于对话的概念。对话是用户和聊天机器人之间的对话单元。对话框可以嵌套，这意味着一个对话框可以包含其他对话框。

要创建对话框，您需要在项目的“/dialogs”目录中创建一个新文件。该文件应命名为“{dialog_name}.js”。

在 `{dialog_name}.js` 文件中，您需要需要 `botbuilder` 模块并创建一个新的 `Dialog` 实例。

```javascript
var builder = require('botbuilder');

var dialog = new builder.Dialog();
```

拥有“Dialog”实例后，您可以通过将对话添加到“stack”属性来定义对话流。

```javascript
dialog.stack(
    // First dialog in the stack
    function (session, args, next) {
        // Do something here
    },
    // Second dialog in the stack
    function (session, args, next) {
        // Do something here
    }
);
```

您还可以使用 addDialog 方法将对话框添加到 stack 属性。

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
});
```

`addDialog` 方法接受一个 `onSelector` 函数，它允许您指定何时执行对话框。 `onSelector` 函数应该在对话框应该执行时返回 `true`，在不应该执行时返回 `false`。

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
});
```

`addDialog` 方法还接受一个 `onReject` 函数，它允许您指定如果对话框未执行应该发生什么。 `onReject` 函数应返回一个 `Promise`，该 Promise 解析为应传递给堆栈中下一个对话框的值。

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return false when the dialog should not be executed
    return false;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

`addDialog` 方法还接受一个 `onPost` 函数，它允许您指定对话框执行后应该发生什么。 `onPost` 函数应返回一个 `Promise`，该 Promise 解析为应传递给堆栈中下一个对话框的值。

```javascript
dialog.addDialog(function (session, args, next) {
    // Do something here
}, function (session, args) {
    // Return true when the dialog should be executed
    return true;
}, function (session, args) {
    // Return a Promise that resolves with the value that should be passed to the next dialog
    return Promise.resolve('some-value');
});
```

### 自然语言处理工具

Bot Builder SDK 包括一组用于处理自然语言的工具。这些工具可用于了解用户的意图、从用户的输入中提取实体等。

自然语言处理工具基于“LuisRecognizer”和“QnAMakerRecognizer”类。

要使用自然语言处理工具，您需要在项目的“/recognizers”目录中创建一个新文件。该文件应命名为“{recognizer_name}.js”。

在“{recognizer_name}.js”文件中，您需要需要“botbuilder”模块并创建一个新的“LuisRecognizer”或“QnAMakerRecognizer”实例。

```javascript
var builder = require('botbuilder');

var recognizer = new builder.LuisRecognizer();
```

一旦您拥有 `LuisRecognizer` 或 `QnAMakerRecognizer` 实例，您就可以使用 `recognize` 方法来处理用户的输入。

```javascript
recognizer.recognize('What is your name?', function (err, result) {
    // Handle the result here
});
```

`recognize` 方法接受一个 `callback` 函数，该函数使用识别结果调用。 `callback` 函数传递了两个参数：`err` 和 `result`。

`err` 参数是一个错误对象，如果在识别过程中发生错误，则传递该对象。

`result` 参数是一个包含识别结果的对象。该对象具有以下属性：

- `intent`：被识别的意图的名称。
- `score`：介于 0 和 1 之间的置信度分数。
- `entities`：包含从用户输入中提取的实体的对象。

### 管理机器人对话的工具

Bot Builder SDK 包括一组用于管理机器人对话的工具。这些工具可用于向用户发送消息、结束对话等。

要使用管理机器人对话的工具，您需要需要“botbuilder”模块并创建一个新的“ConversationBot”实例。

```javascript
var builder = require('botbuilder');

var bot = new builder.ConversationBot();
```

有了“ConversationBot”实例后，您可以使用“message”方法向用户发送消息。

```javascript
bot.message('Hello, world!');
```

`message` 方法接受一个 `text` 参数，这是应该发送给用户的消息，以及一个 `callback` 函数，它在消息发送后被调用。

您还可以使用 `endConversation` 方法结束对话。

```javascript
bot.endConversation();
```

`endConversation` 方法不接受任何参数。

## 部署你的聊天机器人

开发完聊天机器人后，您需要将其部署到服务器，以便用户使用。

Microsoft Bot Framework 附带了一组用于部署聊天机器人的工具和服务。该框架包括一个 Bot Connector 服务，它允许您将聊天机器人连接到各种聊天平台，包括 Facebook Messenger、Skype、Slack 等。

要部署聊天机器人，您首先需要在项目的根目录中创建一个新文件。该文件应命名为“.env”。

在 .env 文件中，您需要添加以下环境变量：

- `PORT`：您的聊天机器人将运行的端口。
- `MICROSOFT_APP_ID`：您的 Microsoft App ID。
- `MICROSOFT_APP_PASSWORD`：您的 Microsoft 应用程序密码。

将环境变量添加到 .env 文件后，您可以使用以下命令启动聊天机器人：

```
npm start
```

您的聊天机器人现在将在 `PORT` 环境变量中指定的端口上运行。

## 结论

在本文中，我们了解了如何使用 Microsoft Bot Framework 开发聊天机器人。我们已经研究了框架的不同组件以及它们如何协同工作。我们还看到了一些关于如何开始构建您自己的聊天机器人的代码示例。