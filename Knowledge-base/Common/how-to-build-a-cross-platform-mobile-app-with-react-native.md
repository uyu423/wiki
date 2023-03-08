---
title: React Native로 크로스 플랫폼 모바일 앱을 구축하는 방법
description: 
published: true
date: 2023-02-07T23:17:33.623Z
tags: 
editor: markdown
dateCreated: 2023-02-07T23:17:27.855Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Build a Cross-Platform Mobile App with React Native***English** document is available*](/en/Knowledge-base/Common/how-to-build-a-cross-platform-mobile-app-with-react-native)
{.links-list}


# React Native로 크로스 플랫폼 모바일 앱을 구축하는 방법

요즘 모바일 앱 개발이 화두입니다. 모바일 앱에 대한 수요는 그 어느 때보다 높으며 시장은 다양한 앱 개발 도구로 포화 상태입니다. React Native는 크로스 플랫폼 모바일 앱을 만드는 데 널리 사용되는 도구입니다.

모바일 앱 개발에 뛰어들고 싶은 웹 개발자라면 React Native를 선택하는 것이 좋습니다. 이 기사에서는 간단한 React Native 앱을 만드는 방법과 iOS 및 Android용으로 빌드하는 방법을 보여줍니다.

## 리액트 네이티브란?

React Native는 Facebook에서 개발한 크로스 플랫폼 모바일 앱 개발 도구입니다. JavaScript 및 React를 사용하여 네이티브 모양의 모바일 앱을 만들 수 있습니다.

React Native 앱은 웹 앱이 아닙니다. 특정 플랫폼(iOS 또는 Android)에서 작동하도록 설계된 실제 기본 앱입니다.

## 개발 환경 설정

앱 개발을 시작하기 전에 개발 환경을 설정해야 합니다.

Mac을 사용하는 경우 iOS 개발용 Xcode와 Android 개발용 Android Studio를 사용할 수 있습니다.

Windows를 사용하는 경우 iOS 및 Android 개발 모두에 Visual Studio를 사용할 수 있습니다.

개발 환경이 설정되면 React Native CLI를 설치해야 합니다.

이렇게 하려면 터미널을 열고 다음 명령을 실행합니다.

```
npm install -g react-native-cli
```

## 새로운 React Native 앱 만들기

이제 React Native CLI를 설치했으므로 이를 사용하여 새로운 React Native 앱을 만들 수 있습니다.

이렇게 하려면 터미널을 열고 다음 명령을 실행합니다.

```
react-native init my-app
```

그러면 현재 디렉토리에 `my-app`이라는 새 디렉토리가 생성됩니다. 이 디렉토리에는 새로운 React Native 앱의 모든 파일이 포함됩니다.

## 앱 실행

이제 새 앱을 만들었으므로 장치에서 실행할 수 있습니다.

이렇게 하려면 터미널을 열고 `my-app` 디렉토리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
react-native run-ios
```

그러면 iOS 시뮬레이터에서 앱이 빌드되고 실행됩니다. Windows를 사용 중이라면 `react-native run-android` 명령을 사용하여 Android 시뮬레이터에서 앱을 실행할 수 있습니다.

## 첫 번째 React Native 컴포넌트 만들기

이제 앱을 실행했으므로 첫 번째 React Native 구성 요소를 만들어 보겠습니다.

텍스트 편집기에서 `index.ios.js`(또는 Windows의 경우 `index.android.js`)를 열고 파일 내용을 다음으로 바꿉니다.

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

이것은 `<Text>` 요소를 렌더링하는 간단한 React 구성 요소입니다.

## 마무리

이 기사에서는 간단한 React Native 앱을 만드는 방법과 iOS 및 Android용으로 빌드하는 방법을 보여주었습니다.

React Native는 크로스 플랫폼 모바일 앱을 만들기 위한 훌륭한 도구입니다. 모바일 앱 개발에 뛰어들고 싶은 웹 개발자라면 React Native를 선택하는 것이 좋습니다.