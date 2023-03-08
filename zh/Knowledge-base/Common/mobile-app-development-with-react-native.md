---
title: 使用 React Native 开发移动应用程序
description: 
published: true
date: 2023-02-17T18:10:01.186Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:37:57.754Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Mobile App Development with React Native***English** version of this document is available*](/en/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}


# 使用 React Native 开发移动应用程序

React Native 是 Facebook 创建的基于 JavaScript 的移动应用程序开发框架。它允许开发人员使用 React（一个用于构建用户界面的 JavaScript 库）为 Android 和 iOS 创建原生移动应用程序。

React Native 应用程序通常使用 JavaScript 和 React 编写，但也可以使用 TypeScript 或 ClojureScript 编写。 React Native 使用与 React 相同的“虚拟 DOM”概念，但它不是针对浏览器，而是针对移动平台。

React Native 应用程序被编译为本地二进制文件，因此它们具有与用 Java 或 Objective-C 编写的应用程序相同的性能。

## 开始使用 React Native

###先决条件

在开始使用 React Native 进行开发之前，您需要安装以下内容：

* 节点.js
* React Native CLI
* Android 或 iOS 的开发环境设置

您可以在 [React Native 文档](https://facebook.github.io/react-native/docs/getting-started.html) 中找到设置开发环境的说明。

### 你好世界

设置开发环境后，您可以使用 React Native CLI 创建一个新的 React Native 应用程序。

运行以下命令：

```
$ react-native init myapp
```

这将创建一个名为“myapp”的新目录，其中包含 React Native 应用程序的基本结构。

创建应用程序后，您可以通过运行以下命令在您的设备或模拟器上运行它：

```
$ react-native run-android
```

或者，对于 iOS：

```
$ react-native run-ios
```

这将启动 React Native 打包程序，构建应用程序，然后在您的设备上启动它。

### 编写你的第一个 React Native 应用程序

现在您已经有了一个基本的应用程序，让我们来编写一些代码吧！

在文本编辑器中打开文件“index.android.js”（适用于 Android）或“index.ios.js”（适用于 iOS）。您应该看到以下内容：

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';

export default class myapp extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Double tap R on your keyboard to reload,{'\n'}
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('myapp', () => myapp);
```

这是一个用 React Native 编写的基本“Hello, World”应用程序。让我们分解一下这里发生的事情。

首先，我们导入我们需要的 React 和 React Native 组件。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';
```

然后，我们创建一个扩展 React 的 Component 类的 myapp 组件。这是 React 组件的基本结构。

```javascript
export default class myapp extends Component {
  render() {
}
```

每个 React 组件都必须有一个返回 React 元素的 render() 方法。在这种情况下，我们将返回一个包含“<Text>”元素的“<View>”元素。

```javascript
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.android.js
        </Text>
        <Text style={styles.instructions}>
          Double tap R on your keyboard to reload,{'\n'}
          Shake or press menu button for dev menu
        </Text>
      </View>
    );
```

`<View>` 和 `<Text>` 元素是 React Native 应用程序的基本构建块。 `<View>` 用于布局，`<Text>` 用于渲染文本。

最后，我们使用 `StyleSheet` 组件为我们的组件设置样式。

```javascript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```

StyleSheet 是一个允许您为组件创建和管理样式的组件。在本例中，我们使用它来设置 `myapp` 组件中的 `<View>` 和 `<Text>` 元素的样式。

最后，我们使用 AppRegistry 组件注册我们的组件。

```javascript
AppRegistry.registerComponent('myapp', () => myapp);
```

`AppRegistry` 是 React Native 应用程序的入口点。它用于注册组件和启动应用程序。

现在我们已经编写了第一个 React Native 应用程序，让我们来看看其他一些可用的组件。

## 组件

React Native 提供了多种可用于构建应用程序的内置组件。

### 看法

视图是 React Native 应用程序的基本构建块。它用于布局并包含其他组件。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  View
} from 'react-native';

export default class myapp extends Component {
  render() {
    return (
      <View style={{ flex: 1 }}>
        // other components go here
      </View>
    );
  }
}
```

View 有一些属性可以用来控制它的布局：

* `flex`：这决定了 View 应该占用父组件中多少可用空间。默认值为 0。
* `flexDirection`：这决定了视图布局的方向。默认值为“列”。其他可能的值是“row”和“reverse”。
* `justifyContent`：这决定了 View 的子项如何沿主轴布局。默认值为“flex-start”。其他可能的值是“center”、“flex-end”、“space-around”和“space-between”。
* `alignItems`：这决定了视图的子项如何沿交叉轴布局。默认值为“拉伸”。其他可能的值是“flex-start”、“center”和“flex-end”。

View 还支持其他一些 props，但这些是最常用的。

### 文本

Text 用于渲染文本。它支持以下道具：

* `style`：这用于设置文本组件的样式。样式对象采用与“StyleSheet”组件相同的格式。
* `numberOfLines`：这用于限制呈现的文本行数。默认值为“undefined”，这意味着不应用任何限制。

Text 还支持其他一些属性，但这些是最常用的。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Text
} from 'react-native';

export default class myapp extends Component {
  render() {
    return (
      <Text style={{ fontSize: 20 }}>
        Hello, world!
      </Text>
    );
  }
}
```

### 图片

图像用于显示图像。它支持以下道具：

* `source`: 用于指定要显示的图像。该值可以是数字（对于静态图像）、字符串（对于网络图像）或对象（对于来自文件系统的图像）。
* `style`：这用于设置图像组件的样式。样式对象采用与“StyleSheet”组件相同的格式。

Image 还支持其他一些道具，但这些是最常用的。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Image
} from 'react-native';

export default class myapp extends Component {
  render() {
    return (
      <Image
        source={{ uri: 'https://facebook.github.io/react/img/logo_og.png' }}
        style={{ width: 400, height: 400 }}
      />
    );
  }
}
```

### 文本输入

TextInput 用于获取用户的文本输入。它支持以下道具：

* `value`：用于设置输入的初始值。
* `onChangeText`: 这用于设置每次文本输入更改时调用的函数。该函数被传递给文本输入的新值。
* `style`：这用于设置 TextInput 组件的样式。样式对象采用与“StyleSheet”组件相同的格式。

TextInput 还支持其他一些属性，但这些是最常用的。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  TextInput
} from 'react-native';

export default class myapp extends Component {
  constructor(props) {
    super(props);
    this.state = {
      text: ''
    };
  }
  
  render() {
    return (
      <TextInput
        style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
        onChangeText={(text) => this.setState({ text })}
        value={this.state.text}
      />
    );
  }
}
```

每次文本输入更改时，TextInput 都会发出“onChangeText”事件。我们使用 `onChangeText` 属性来设置一个函数，用新值更新 `text` 状态属性。我们还使用了 `value` 属性来设置输入的初始值。

### 按钮

按钮用于通过按下按钮获取用户输入。它支持以下道具：

* `onPress`：用于设置按下按钮时调用的函数。
* `title`: 用于设置按钮的标题。
* `style`：这用于设置 Button 组件的样式。样式对象采用与“StyleSheet”组件相同的格式。

Button 还支持其他一些道具，但这些是最常用的。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Button
} from 'react-native';

export default class myapp extends Component {
  _onPressButton() {
    alert('You pressed the button!');
  }
  
  render() {
    return (
      <Button
        onPress={this._onPressButton}
        title="Press Me"
      />
    );
  }
}
```

在此示例中，我们使用了 _onPressButton 函数在按下按钮时显示警报。

##造型

React Native 使用与 React 相同的“样式对象”概念。样式对象是包含样式属性和值的 JavaScript 对象。样式属性和值与 CSS 属性和值相同。

可以使用 `StyleSheet` 组件创建样式对象。

```javascript
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});
```

`StyleSheet.create` 方法采用样式对象并返回针对性能优化的样式对象。

创建样式对象后，可以使用 style 属性将其应用于组件。

```javascript
<Text style={styles.welcome}>
  Hello, world!
</Text>
```

样式对象也可以内联创建。

```javascript
<Text style={{ fontSize: 20 }}>
  Hello, world!
</Text>
```

内联样式对象采用与“StyleSheet”样式对象相同的格式。

## 平台特定代码

React Native 允许您编写特定于平台的代码。平台特定代码是仅在特定平台上执行的代码。

React Native 为此提供了 `Platform` API。 Platform API 有一些方法可以用来检测平台：

* `Platform.OS`：返回平台名称。可能的值为“ios”和“android”。
* `Platform.Version`：返回平台的版本。

您可以使用“Platform.select”方法来定义特定于平台的组件。 `Platform.select` 方法接受一个将键映射到 React 元素的对象。键是平台名称，React 元素是要呈现的组件。 `Platform.select` 方法将为当前平台呈现 React 元素。

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  Text,
  View,
  Platform
} from 'react-native';

export default class myapp extends Component {
  render() {
    return (
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <Text>
          Hello, world!
        </Text>
        {Platform.select({
          ios:
            <Text>
              This is an iOS Device.
            </Text>,
          android:
            <Text>
              This is an Android Device.
            </Text>,
        })}
      </View>
    );
  }
}
```

在此示例中，我们使用了 `Platform.select` 方法在 iOS 和 Android 设备上呈现不同的 `<Text>` 元素。

还可以使用“Platform.isPad”和“Platform.isTVos”方法定义平台特定代码。

`Platform.isPad` 将在 iPad 上返回 `true` 而在 iPad 上返回 `false`