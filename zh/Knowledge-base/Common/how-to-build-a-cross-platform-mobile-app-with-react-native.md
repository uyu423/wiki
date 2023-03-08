---
title: 如何使用 React Native 构建跨平台移动应用程序
description: 
published: true
date: 2023-02-07T23:17:33.623Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:17:27.854Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Build a Cross-Platform Mobile App with React Native***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}


# 如何使用 React Native 构建跨平台移动应用程序

移动应用程序开发是当今的热门话题。对移动应用程序的需求比以往任何时候都高，市场上充斥着不同的应用程序开发工具。 React Native 是一种用于创建跨平台移动应用程序的流行工具。

如果您是一名想要进入移动应用程序开发的 Web 开发人员，那么 React Native 是一个不错的选择。在本文中，我们将向您展示如何创建一个简单的 React Native 应用程序以及如何为 iOS 和 Android 构建它。

## 什么是 React Native？

React Native 是 Facebook 开发的跨平台移动应用程序开发工具。它允许您使用 JavaScript 和 React 创建具有原生外观的移动应用程序。

React Native 应用程序不是网络应用程序。它们是专为在特定平台（iOS 或 Android）上运行而设计的真实原生应用程序。

## 设置你的开发环境

在我们开始开发我们的应用程序之前，我们需要设置我们的开发环境。

如果您使用的是 Mac，则可以使用 Xcode 进行 iOS 开发，使用 Android Studio 进行 Android 开发。

如果您使用的是 Windows，则可以使用 Visual Studio 进行 iOS 和 Android 开发。

设置好开发环境后，您需要安装 React Native CLI。

为此，请打开终端并运行以下命令：

```
npm install -g react-native-cli
```

## 创建一个新的 React Native 应用程序

现在我们已经安装了 React Native CLI，我们可以使用它来创建一个新的 React Native 应用程序。

为此，请打开终端并运行以下命令：

```
react-native init my-app
```

这将在您的当前目录中创建一个名为“my-app”的新目录。该目录将包含新 React Native 应用程序的所有文件。

## 运行你的应用

现在我们已经创建了新的应用程序，我们可以在我们的设备上运行它。

为此，请打开一个终端并导航到“my-app”目录。然后，运行以下命令：

```
react-native run-ios
```

这将在 iOS 模拟器上构建和运行您的应用程序。如果您使用的是 Windows，则可以使用“react-native run-android”命令在 Android 模拟器上运行您的应用程序。

## 制作你的第一个 React Native 组件

现在我们已经运行了我们的应用程序，让我们创建我们的第一个 React Native 组件。

在文本编辑器中打开“index.ios.js”（如果您使用的是 Windows，则打开“index.android.js”）并将文件内容替换为以下内容：

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Text,
  View
} from 'react-native';

export default class my-app extends Component {
  render() {
    return (
      <View>
        <Text>Hello, world!</Text>
      </View>
    );
  }
}

AppRegistry.registerComponent('my-app', () => my-app);
```

这是一个简单的 React 组件，它呈现一个 `<Text>` 元素。

## 包起来

在本文中，我们向您展示了如何创建一个简单的 React Native 应用程序以及如何为 iOS 和 Android 构建它。

React Native 是创建跨平台移动应用程序的绝佳工具。如果您是一名想要进入移动应用程序开发的 Web 开发人员，那么 React Native 是一个不错的选择。