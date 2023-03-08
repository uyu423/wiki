---
title: React Native를 사용한 모바일 앱 개발
description: 
published: true
date: 2023-02-17T18:09:56.723Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:37:57.719Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Mobile App Development with React Native***English** version of this document is available*](/en/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}


# React Native로 모바일 앱 개발

React Native는 Facebook에서 만든 JavaScript 기반 모바일 앱 개발 프레임워크입니다. 이를 통해 개발자는 사용자 인터페이스 구축을 위한 JavaScript 라이브러리인 React를 사용하여 Android 및 iOS용 기본 모바일 앱을 만들 수 있습니다.

React Native 앱은 일반적으로 JavaScript 및 React로 작성되지만 TypeScript 또는 ClojureScript로도 작성할 수 있습니다. React Native는 React와 동일한 "가상 DOM" 개념을 사용하지만 브라우저를 대상으로 하는 대신 모바일 플랫폼을 대상으로 합니다.

React Native 앱은 네이티브 바이너리로 컴파일되므로 Java 또는 Objective-C로 작성된 앱과 동일한 성능을 가집니다.

## 리액트 네이티브 시작하기

### 전제 조건

React Native로 개발을 시작하려면 먼저 다음을 설치해야 합니다.

* Node.js
* 반응 네이티브 CLI
* Android 또는 iOS용 개발 환경 설정

[React Native 문서](https://facebook.github.io/react-native/docs/getting-started.html)에서 개발 환경 설정에 대한 지침을 찾을 수 있습니다.

### 안녕하세요, 세계

개발 환경 설정이 완료되면 React Native CLI를 사용하여 새로운 React Native 앱을 만들 수 있습니다.

다음 명령을 실행합니다.

```
$ react-native init myapp
```

이렇게 하면 React Native 앱의 기본 구조로 "myapp"이라는 새 디렉토리가 생성됩니다.

앱이 생성되면 다음 명령을 실행하여 장치 또는 시뮬레이터에서 실행할 수 있습니다.

```
$ react-native run-android
```

또는 iOS의 경우:

```
$ react-native run-ios
```

이렇게 하면 React Native 패키저가 시작되고 앱이 빌드된 다음 기기에서 실행됩니다.

### 첫 번째 React Native 앱 작성

이제 기본 앱이 있으므로 코드를 작성해 보겠습니다.

텍스트 편집기에서 `index.android.js`(Android용) 또는 `index.ios.js`(iOS용) 파일을 엽니다. 다음이 표시되어야 합니다.

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

이것은 React Native로 작성된 기본 "Hello, World" 앱입니다. 여기서 무슨 일이 일어나고 있는지 분석해 봅시다.

먼저 필요한 React 및 React Native 구성 요소를 가져옵니다.

```javascript
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View
} from 'react-native';
```

그런 다음 React의 `Component` 클래스를 확장하는 `myapp` 컴포넌트를 만듭니다. 이것이 React 컴포넌트의 기본 구조입니다.

```javascript
export default class myapp extends Component {
  render() {
}
```

모든 React 구성 요소에는 React 요소를 반환하는 `render()` 메서드가 있어야 합니다. 이 경우 `<Text>` 요소를 포함하는 `<View>` 요소를 반환합니다.

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

`<View>` 및 `<Text>` 요소는 React Native 앱의 기본 빌딩 블록입니다. `<View>`는 레이아웃에 사용되고 `<Text>`는 텍스트 렌더링에 사용됩니다.

마지막으로 `StyleSheet` 구성 요소를 사용하여 구성 요소의 스타일을 지정합니다.

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

StyleSheet는 구성 요소의 스타일을 만들고 관리할 수 있는 구성 요소입니다. 이 경우에는 이를 사용하여 `myapp` 구성 요소 내의 `<View>` 및 `<Text>` 요소의 스타일을 지정합니다.

마지막으로 `AppRegistry` 컴포넌트에 컴포넌트를 등록합니다.

```javascript
AppRegistry.registerComponent('myapp', () => myapp);
```

`AppRegistry`는 React Native 앱의 진입점입니다. 구성 요소를 등록하고 앱을 실행하는 데 사용됩니다.

이제 첫 번째 React Native 앱을 작성했으므로 사용 가능한 다른 구성 요소를 살펴보겠습니다.

## 구성 요소

React Native는 애플리케이션을 구축하는 데 사용할 수 있는 다양한 내장 구성 요소를 제공합니다.

### 보다

View는 React Native 앱의 기본 빌딩 블록입니다. 레이아웃에 사용되며 다른 구성 요소를 포함합니다.

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

View에는 레이아웃을 제어하는 데 사용할 수 있는 몇 가지 소품이 있습니다.

* `flex`: View가 차지해야 하는 부모 구성 요소의 사용 가능한 공간을 결정합니다. 기본값은 0입니다.
* `flexDirection`: View 레이아웃의 방향을 결정합니다. 기본값은 '열'입니다. 다른 가능한 값은 `row` 및 `reverse`입니다.
* `justifyContent`: View의 자식이 기본 축을 따라 배치되는 방식을 결정합니다. 기본값은 `flex-start`입니다. 다른 가능한 값은 `center`, `flex-end`, `space-around` 및 `space-between`입니다.
* `alignItems`: View의 자식이 교차 축을 따라 배치되는 방식을 결정합니다. 기본값은 `스트레치`입니다. 다른 가능한 값은 `flex-start`, `center` 및 `flex-end`입니다.

View는 몇 가지 다른 소품도 지원하지만 가장 일반적으로 사용되는 소품입니다.

### 텍스트

텍스트는 텍스트 렌더링에 사용됩니다. 다음 소품을 지원합니다.

* `style`: Text 컴포넌트의 스타일을 지정하는 데 사용됩니다. 스타일 개체는 `StyleSheet` 구성 요소와 동일한 형식을 사용합니다.
* `numberOfLines`: 렌더링되는 텍스트 줄 수를 제한하는 데 사용됩니다. 기본값은 '정의되지 않음'이며 제한이 적용되지 않음을 의미합니다.

Text는 몇 가지 다른 소품도 지원하지만 가장 일반적으로 사용되는 소품입니다.

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

### 이미지

이미지는 이미지를 표시하는 데 사용됩니다. 다음 소품을 지원합니다.

* `소스`: 표시할 이미지를 지정하는 데 사용됩니다. 값은 숫자(정적 이미지의 경우), 문자열(네트워크 이미지의 경우) 또는 객체(파일 시스템의 이미지의 경우)일 수 있습니다.
* `style`: 이미지 구성 요소의 스타일을 지정하는 데 사용됩니다. 스타일 개체는 `StyleSheet` 구성 요소와 동일한 형식을 사용합니다.

Image는 몇 가지 다른 소품도 지원하지만 가장 일반적으로 사용되는 소품입니다.

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

### 텍스트 입력

TextInput은 사용자로부터 텍스트 입력을 받는 데 사용됩니다. 다음 소품을 지원합니다.

* `value`: 입력의 초기값을 설정하는데 사용합니다.
* `onChangeText`: 텍스트 입력이 변경될 때마다 호출되는 함수를 설정하는데 활용합니다. 함수에 텍스트 입력의 새 값이 전달됩니다.
* `style`: TextInput 구성 요소의 스타일을 지정하는 데 사용됩니다. 스타일 개체는 `StyleSheet` 구성 요소와 동일한 형식을 사용합니다.

TextInput은 몇 가지 다른 소품도 지원하지만 가장 일반적으로 사용되는 소품입니다.

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

TextInput은 텍스트 입력이 변경될 때마다 `onChangeText` 이벤트를 내보냅니다. `onChangeText` 소품을 사용하여 `text` 상태 속성을 새 값으로 업데이트하는 함수를 설정했습니다. 또한 `value` 소품을 사용하여 입력의 초기 값을 설정했습니다.

### 버튼

버튼은 버튼 누름을 통해 사용자 입력을 받는 데 사용됩니다. 다음 소품을 지원합니다.

* `onPress`: 버튼을 눌렀을 때 호출되는 기능을 설정합니다.
* `제목`: 버튼의 제목을 설정하는데 사용합니다.
* `style`: Button 컴포넌트의 스타일을 지정하는 데 사용됩니다. 스타일 개체는 `StyleSheet` 구성 요소와 동일한 형식을 사용합니다.

Button은 몇 가지 다른 소품도 지원하지만 가장 일반적으로 사용되는 소품입니다.

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

이 예제에서는 `_onPressButton` 함수를 사용하여 버튼을 눌렀을 때 경고를 표시했습니다.

## 스타일링

React Native는 React와 동일한 "스타일 객체" 개념을 사용합니다. 스타일 개체는 스타일 속성과 값을 포함하는 JavaScript 개체입니다. 스타일 속성 및 값은 CSS 속성 및 값과 동일합니다.

스타일 개체는 `StyleSheet` 구성 요소를 사용하여 만들 수 있습니다.

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

`StyleSheet.create` 메서드는 스타일 개체를 가져와서 성능에 최적화된 스타일 개체를 반환합니다.

스타일 객체가 생성되면 `style` 소품을 사용하여 구성 요소에 적용할 수 있습니다.

```javascript
<Text style={styles.welcome}>
  Hello, world!
</Text>
```

스타일 개체를 인라인으로 만들 수도 있습니다.

```javascript
<Text style={{ fontSize: 20 }}>
  Hello, world!
</Text>
```

인라인 스타일 개체는 `StyleSheet` 스타일 개체와 동일한 형식을 사용합니다.

## 플랫폼별 코드

React Native를 사용하면 플랫폼별 코드를 작성할 수 있습니다. 플랫폼 특정 코드는 특정 플랫폼에서만 실행되는 코드입니다.

React Native는 이를 위한 `Platform` API를 제공합니다. 플랫폼 API에는 플랫폼을 감지하는 데 사용할 수 있는 몇 가지 방법이 있습니다.

* `Platform.OS`: 플랫폼 이름을 반환합니다. 가능한 값은 `ios` 및 `android`입니다.
* `Platform.Version`: 플랫폼 버전을 반환합니다.

`Platform.select` 메서드를 사용하여 플랫폼별 구성 요소를 정의할 수 있습니다. `Platform.select` 메서드는 키를 React 요소에 매핑하는 객체를 사용합니다. 키는 플랫폼 이름이고 React 요소는 렌더링할 구성 요소입니다. `Platform.select` 메서드는 현재 플랫폼에 대한 React 요소를 렌더링합니다.

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

이 예제에서는 `Platform.select` 메서드를 사용하여 iOS 및 Android 장치에서 다른 `<Text>` 요소를 렌더링했습니다.

플랫폼별 코드는 `Platform.isPad` 및 `Platform.isTVos` 메서드를 사용하여 정의할 수도 있습니다.

`Platform.isPad`는 iPad에서 `true`를 반환하고 iPad에서 `false`를 반환합니다.