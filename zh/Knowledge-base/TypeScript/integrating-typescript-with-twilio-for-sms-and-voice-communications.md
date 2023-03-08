---
title: 将 TypeScript 与 Twilio 集成以进行短信和语音通信
description: 
published: true
date: 2023-02-17T18:07:55.063Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:17:27.612Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Integrating TypeScript with Twilio for SMS and Voice Communications***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-twilio-for-sms-and-voice-communications)
{.links-list}


# 将 TypeScript 与 Twilio 集成以进行短信和语音通信

作为开发人员，您可能会发现自己处于需要向应用程序添加 SMS 或语音功能的情况。例如，您可能需要在您的网站上添加一个“联系我们”表单，以允许用户向您公司的客户服务号码发送 SMS 消息。或者，您可能需要为用户添加从您的 Web 或移动应用程序拨打电话的功能。

Twilio 是一个云通信平台，可让您向应用程序添加语音和 SMS 功能。在本文中，我们将向您展示如何使用 TypeScript 编程语言将 Twilio 与您的 Web 或移动应用程序集成。

## 什么是打字稿？

TypeScript 是由 Microsoft 开发和维护的免费开源编程语言。它是 JavaScript 的超集，这意味着所有 JavaScript 代码都是有效的 TypeScript 代码。

TypeScript 为 JavaScript 添加了一些特性，可以更轻松地开发大型应用程序。例如，TypeScript 支持类型注释，它允许您向变量和函数添加类型信息。这可以帮助您在开发过程的早期发现错误。

##安装打字稿

要安装 TypeScript，您需要在计算机上安装 Node.js 和 npm。 Node.js 是一种 JavaScript 运行时，可让您在浏览器之外运行 JavaScript 代码。 npm 是 Node.js 的包管理器，可让您安装 TypeScript 和其他 JavaScript 库。

安装 Node.js 和 npm 后，您可以使用以下命令安装 TypeScript：

```
npm install -g typescript
```

## 设置 TypeScript 项目

安装 TypeScript 后，您可以通过运行以下命令来设置 TypeScript 项目：

```
tsc --init
```

这将在您的项目目录中创建一个名为“tsconfig.json”的文件。此文件包含项目的 TypeScript 配置。

默认情况下，TypeScript 编译器将生成与最新的 JavaScript 标准 (ES6) 兼容的 JavaScript 代码。如果您需要生成与旧版本的 JavaScript 兼容的代码，您可以在 tsconfig.json 中设置 target 编译器选项。例如，要生成与 ES5 标准兼容的代码，您可以将“target”选项设置为“es5”。

## 编译 TypeScript 代码

设置 TypeScript 项目后，您可以使用以下命令将 TypeScript 代码编译为 JavaScript：

```
tsc
```

这会将项目中的所有 TypeScript 代码编译成 JavaScript。输出的 JavaScript 文件将放在 out 目录中。

您还可以通过运行以下命令来编译特定的 TypeScript 文件：

```
tsc file.ts
```

## 将 TypeScript 与 Twilio 集成

现在我们已经了解了 TypeScript 的基础知识，让我们来看看如何使用 TypeScript 通过 Twilio API 将 SMS 或语音功能添加到您的应用程序。

### 发送短信

要使用 TypeScript 发送 SMS 消息，您需要设置 Twilio 帐户并购买 Twilio 电话号码。拥有 Twilio 帐户和电话号码后，您可以使用以下 TypeScript 代码发送 SMS 消息：

```typescript
import * as twilio from "twilio";

const accountSid = "your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio(accountSid, authToken);

client.messages
  .create({
     body: "Hello, world!",
     from: "your-twilio-phone-number",
     to: "your-phone-number"
   })
  .then(message => console.log(message.sid));
```

在上面的代码中，我们使用 import 关键字导入了 Twilio 库。然后，我们使用我们的帐户凭据设置一个新的“Twilio”客户端。最后，我们使用 `client.messages.create` 方法发送短信。

### 打电话

要使用 TypeScript 拨打电话，您需要设置 Twilio 帐户并购买 Twilio 电话号码。拥有 Twilio 帐户和电话号码后，您可以使用以下 TypeScript 代码拨打电话：

```typescript
import * as twilio from "twilio";

const accountSid = "your-twilio-account-sid";
const authToken = "your-twilio-auth-token";
const client = twilio(accountSid, authToken);

client.calls
  .create({
     url: "your-twiML-url",
     to: "your-phone-number",
     from: "your-twilio-phone-number"
   })
  .then(call => console.log(call.sid));
```

在上面的代码中，我们使用 import 关键字导入了 Twilio 库。然后，我们使用我们的帐户凭据设置一个新的“Twilio”客户端。最后，我们使用 `client.calls.create` 方法拨打电话。

## 结论

在本文中，我们向您展示了如何使用 TypeScript 通过 Twilio API 将 SMS 和语音功能添加到您的 Web 或移动应用程序。我们还介绍了 TypeScript 的基础知识，包括如何安装 TypeScript 以及如何设置 TypeScript 项目。