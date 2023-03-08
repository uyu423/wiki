---
title: 058：测试 TensorFlow.js 和 Node.js 应用程序
description: 
published: true
date: 2023-02-02T20:36:35.201Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:36:33.575Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [058: Testing TensorFlow.js and Node.js Applications***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/058-testing-tensorflow-js-and-node-js-applications)
{.links-list}


# 058：测试 TensorFlow.js 和 Node.js 应用程序

## 介绍

在本文中，我们将介绍如何测试 TensorFlow.js 和 Node.js 应用程序。我们将介绍不同类型的测试、如何设置测试环境以及如何运行测试。

## 测试类型

有两种主要的测试类型：单元测试和端到端测试。

单元测试用于测试单独的代码片段，例如函数或类。它们通常由编写代码的开发人员编写。

端到端测试用于从头到尾测试整个应用程序。它们通常由独立的测试人员团队编写。

## 设置测试环境

在开始编写测试之前，您需要设置一个测试环境。

有许多不同的方法可以做到这一点，但我们将介绍最常见的方法：使用测试框架。

测试框架是一种软件，它提供了一组用于编写和运行测试的工具。最流行的 JavaScript 测试框架是 Jest。

要使用 Jest，您需要先安装它。您可以使用命令行或 npm 等包管理器来执行此操作：

```
npm install --save-dev jest
```

安装 Jest 后，您需要创建一个配置文件。这个文件告诉 Jest 如何运行你的测试。

最简单的方法是在项目的根目录中创建一个名为 jest.config.js 的文件：

```js
module.exports = {
  // your config here
};
```

您还可以使用 JSON 文件或 XML 文件。

有了配置文件后，您需要告诉 Jest 您的测试位于何处。您可以通过设置“testMatch”属性来做到这一点：

```js
module.exports = {
  testMatch: ['**/__tests__/**/*.js?(x)']
};
```

这告诉 Jest 查找 __tests__ 目录中以 .js 或 .jsx 结尾的所有文件。

## 编写测试

现在您已经设置了测试环境，您可以开始编写测试。

测试是用 JavaScript 编写的。它们通常放在 __tests__ 目录中，但您可以将它们放在任何您想要的位置。

测试由两部分组成：“测试用例”和“预期结果”。

测试用例是运行被测代码的一段代码。例如，如果您正在测试一个将两个数字相加的函数，您的测试用例可能如下所示：

```js
// test case
const result = add(1, 2);

// expected outcome
expect(result).toBe(3);
```

“预期结果”是您期望代码执行的操作。在本例中，我们期望结果为 3。

如果被测代码没有产生预期的结果，则测试将失败。

## 运行测试

编写测试后，您可以使用命令行或 npm 等包管理器运行它们：

```
npm test
```

这将运行项目中的所有测试。

您还可以通过传递测试或组的名称来运行特定测试或一组测试：

```
npm test my-test
```

```
npm test my-test-group
```

## 结论

在本文中，我们介绍了如何测试 TensorFlow.js 和 Node.js 应用程序。我们介绍了不同类型的测试、如何设置测试环境以及如何编写和运行测试。