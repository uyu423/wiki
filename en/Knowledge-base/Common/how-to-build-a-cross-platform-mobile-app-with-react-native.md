---
title: How to Build a Cross-Platform Mobile App with React Native
description: 
published: true
date: 2023-02-07T23:17:29.520Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:17:27.863Z
---

- [Cómo crear una aplicación móvil multiplataforma con React Native***Spanish** document is available*](/es/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}
- [如何使用 React Native 构建跨平台移动应用程序***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}
- [React Native로 크로스 플랫폼 모바일 앱을 구축하는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}


# How to Build a Cross-Platform Mobile App with React Native

Mobile app development is a hot topic these days. The demand for mobile apps is higher than ever, and the market is saturated with different app development tools. React Native is a popular tool for creating cross-platform mobile apps.

If you're a web developer who wants to get into mobile app development, React Native is a great choice. In this article, we'll show you how to create a simple React Native app and how to build it for both iOS and Android.

## What is React Native?

React Native is a cross-platform mobile app development tool developed by Facebook. It allows you to create native-looking mobile apps using JavaScript and React.

React Native apps are not web apps. They are real, native apps that are designed to work on a specific platform (iOS or Android).

## Setting up your development environment

Before we can start developing our app, we need to set up our development environment.

If you're on a Mac, you can use Xcode for iOS development and Android Studio for Android development.

If you're on Windows, you can use Visual Studio for both iOS and Android development.

Once you have your development environment set up, you need to install the React Native CLI.

To do this, open up a terminal and run the following command:

```
npm install -g react-native-cli
```

## Creating a new React Native app

Now that we have the React Native CLI installed, we can use it to create a new React Native app.

To do this, open up a terminal and run the following command:

```
react-native init my-app
```

This will create a new directory called `my-app` in your current directory. This directory will contain all the files for your new React Native app.

## Running your app

Now that we have our new app created, we can run it on our device.

To do this, open up a terminal and navigate to the `my-app` directory. Then, run the following command:

```
react-native run-ios
```

This will build and run your app on an iOS simulator. If you're on Windows, you can use the `react-native run-android` command to run your app on an Android simulator.

## Making your first React Native component

Now that we have our app running, let's create our first React Native component.

Open up `index.ios.js` (or `index.android.js` if you're on Windows) in your text editor and replace the contents of the file with the following:

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

This is a simple React component that renders a `<Text>` element.

## Wrapping up

In this article, we've shown you how to create a simple React Native app and how to build it for both iOS and Android.

React Native is a great tool for creating cross-platform mobile apps. If you're a web developer who wants to get into mobile app development, React Native is a great choice.