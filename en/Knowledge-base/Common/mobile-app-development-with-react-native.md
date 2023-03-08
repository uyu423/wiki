---
title: Mobile App Development with React Native
description: 
published: true
date: 2023-02-17T18:09:54.974Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:37:57.717Z
---

- [React Native를 사용한 모바일 앱 개발***Korean** version of this document is available*](/ko/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}
- [React Native によるモバイルアプリ開発***Japanese** version of this document is available*](/ja/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}
- [使用 React Native 开发移动应用程序***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}


# Mobile App Development with React Native

React Native is a JavaScript-based mobile app development framework created by Facebook. It allows developers to create native mobile apps for Android and iOS using React, a JavaScript library for building user interfaces.

React Native apps are typically written in JavaScript and React, but they can also be written in TypeScript or ClojureScript. React Native uses the same concept of a "virtual DOM" as React, but instead of targeting the browser, it targets mobile platforms.

React Native apps are compiled to native binaries, so they have the same performance as apps written in Java or Objective-C.

## Getting Started with React Native

### Prerequisites

Before you can begin developing with React Native, you will need to have the following installed:

* Node.js
* The React Native CLI
* A development environment setup for either Android or iOS

You can find instructions for setting up your development environment in the [React Native docs](https://facebook.github.io/react-native/docs/getting-started.html).

### Hello, World

Once you have your development environment setup, you can create a new React Native app using the React Native CLI.

run the following command:

```
$ react-native init myapp
```

This will create a new directory called "myapp" with a basic structure for a React Native app.

Once the app is created, you can run it on your device or simulator by running the following command:

```
$ react-native run-android
```

or, for iOS:

```
$ react-native run-ios
```

This will start the React Native packager, build the app, and then launch it on your device.

### Writing your first React Native app

Now that you have a basic app, let's write some code!

Open the file `index.android.js` (for Android) or `index.ios.js` (for iOS) in your text editor. You should see the following:

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

This is a basic "Hello, World" app written in React Native. Let's break down what's happening here.

First, we import the React and React Native components that we'll need.

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';
```

Then, we create a `myapp` component that extends React's `Component` class. This is the basic structure of a React component.

```javascript
export default class myapp extends Component {
  render() {
}
```

Every React component must have a `render()` method that returns a React element. In this case, we're returning a `<View>` element that contains a `<Text>` element.

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

The `<View>` and `<Text>` elements are the basic building blocks of React Native apps. `<View>` is used for layout, and `<Text>` is used for rendering text.

Finally, we styles for our component using the `StyleSheet` component.

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

StyleSheet is a component that allows you to create and manage styles for your components. In this case, we're using it to style the `<View>` and `<Text>` elements inside our `myapp` component.

Finally, we register our component with the `AppRegistry` component.

```javascript
AppRegistry.registerComponent('myapp', () => myapp);
```

The `AppRegistry` is the entry point for React Native apps. It is used to register components and launch the app.

Now that we've written our first React Native app, let's take a look at some of the other components that are available.

## Components

React Native offers a wide variety of built-in components that can be used to build applications. 

### View

View is the basic building block of React Native apps. It is used for layout and contains other components.

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

View has a few props that can be used to control its layout:

* `flex`: This determines how much of the available space in the parent component the View should take up. The default value is 0.
* `flexDirection`: This determines the direction of the View's layout. The default value is `column`. Other possible values are `row` and `reverse`.
* `justifyContent`: This determines how the children of the View are laid out along the main axis. The default value is `flex-start`. Other possible values are `center`, `flex-end`, `space-around`, and `space-between`.
* `alignItems`: This determines how the children of the View are laid out along the cross axis. The default value is `stretch`. Other possible values are `flex-start`, `center`, and `flex-end`.

View also supports a few other props, but these are the most commonly used ones.

### Text

Text is used for rendering text. It supports the following props:

* `style`: This is used to style the Text component. The style object takes the same format as the `StyleSheet` component.
* `numberOfLines`: This is used to limit the number of lines of text that are rendered. The default value is `undefined`, which means that no limit is applied.

Text also supports a few other props, but these are the most commonly used ones.

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

### Image

Image is used for displaying images. It supports the following props:

* `source`: This is used to specify the image to display. The value can be a number (for a static image), a string (for a network image), or an object (for an image from the file system).
* `style`: This is used to style the Image component. The style object takes the same format as the `StyleSheet` component.

Image also supports a few other props, but these are the most commonly used ones.

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

### TextInput

TextInput is used for getting text input from the user. It supports the following props:

* `value`: This is used to set the initial value of the input.
* `onChangeText`: This is used to set a function that is called every time the text input changes. The function is passed the new value of the text input.
* `style`: This is used to style the TextInput component. The style object takes the same format as the `StyleSheet` component.

TextInput also supports a few other props, but these are the most commonly used ones.

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

TextInput emits the `onChangeText` event every time the text input changes. We've used the `onChangeText` prop to set a function that updates the `text` state property with the new value. We've also used the `value` prop to set the initial value of the input.

### Button

Button is used for getting user input via button press. It supports the following props:

* `onPress`: This is used to set a function that is called when the button is pressed.
* `title`: This is used to set the button's title.
* `style`: This is used to style the Button component. The style object takes the same format as the `StyleSheet` component.

Button also supports a few other props, but these are the most commonly used ones.

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

In this example, we've used the `_onPressButton` function to display an alert when the button is pressed.

## Styling

React Native uses the same concept of "style objects" as React. Style objects are JavaScript objects that contain style properties and values. The style properties and values are the same as CSS properties and values.

Style objects can be created using the `StyleSheet` component.

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

The `StyleSheet.create` method takes a style object and returns a style object that is optimized for performance.

Once a style object has been created, it can be applied to a component using the `style` prop.

```javascript
<Text style={styles.welcome}>
  Hello, world!
</Text>
```

Style objects can also be created inline.

```javascript
<Text style={{ fontSize: 20 }}>
  Hello, world!
</Text>
```

Inline style objects take the same format as `StyleSheet` style objects.

## Platform Specific code

React Native allows you to write platform specific code. Platform specific code is code that is only executed on a specific platform.

React Native provides the `Platform` API for this. The Platform API has a few methods that can be used to detect the platform:

* `Platform.OS`: This returns the name of the platform. The possible values are `ios` and `android`.
* `Platform.Version`: This returns the version of the platform.

You can use the `Platform.select` method to define platform specific components. The `Platform.select` method takes an object that maps keys to React elements. The keys are platform names, and the React elements are the components to render. The `Platform.select` method will render the React element for the current platform.

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

In this example, we've used the `Platform.select` method to render a different `<Text>` element on iOS and Android devices.

Platform specific code can also be defined using the `Platform.isPad` and `Platform.isTVos` methods.

`Platform.isPad` will return `true` on iPads and `false` on