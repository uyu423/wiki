---
title: React Native によるモバイルアプリ開発
description: 
published: true
date: 2023-02-17T18:09:58.889Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:37:57.749Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Mobile App Development with React Native***English** version of this document is available*](/en/Knowledge-base/Common/mobile-app-development-with-react-native)
{.links-list}


#React Nativeでモバイルアプリを開発

React Nativeは、Facebookで作成されたJavaScriptベースのモバイルアプリ開発フレームワークです。これにより、開発者はユーザーインターフェイスを構築するためのJavaScriptライブラリであるReactを使用して、AndroidおよびiOS用のネイティブモバイルアプリを作成できます。

React Nativeアプリは通常JavaScriptとReactで書かれていますが、TypeScriptやClojureScriptで書くこともできます。 React NativeはReactと同じ「仮想DOM」という概念を使用していますが、ブラウザを対象とするのではなく、モバイルプラットフォームを対象としています。

React Nativeアプリはネイティブバイナリにコンパイルされるため、JavaまたはObjective-Cで書かれたアプリと同じパフォーマンスを持ちます。

##リアクトネイティブを始める

### 前提条件

React Nativeで開発を開始するには、まず次のものをインストールする必要があります。

* Node.js
*反応ネイティブCLI
* AndroidまたはiOS用の開発環境設定

[React Native ドキュメント] (https://facebook.github.io/react-native/docs/getting-started.html) で、開発環境設定の手順を確認できます。

### こんにちは、世界

開発環境設定が完了したら、React Native CLIを使用して新しいReact Nativeアプリを作成できます。

次のコマンドを実行します。

```
$react-native init myapp
```

これにより、React Nativeアプリの基本構造として「myapp」という新しいディレクトリが作成されます。

アプリが作成されたら、次のコマンドを実行してデバイスまたはシミュレータで実行できます。

```
$react-native run-android
```

またはiOSの場合：

```
$react-native run-ios
```

これにより、React Nativeパッケージャが起動し、アプリがビルドされてからデバイスで実行されます。

###最初のReact Nativeアプリを書く

それでは基本的なアプリがあるので、コードを書いてみましょう。

テキストエディタで `index.android.js`（Android用）または `index.ios.js`（iOS用）ファイルを開きます。以下が表示されます。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  StyleSheet,
  テキスト、
  View
} from 'react-native';

export default class myapp extends Component {
  render() {
    return(
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
    ）;
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
}）;

AppRegistry.registerComponent('myapp', () => myapp);
```

これはReact Nativeで書かれた基本的な「Hello、World」アプリです。ここで何が起こっているのかを分析しましょう。

まず、必要なReactコンポーネントとReact Nativeコンポーネントをインポートします。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  StyleSheet,
  テキスト、
  View
} from 'react-native';
```

次に、Reactの `Component`クラスを拡張する `myapp`コンポーネントを作成します。これがReactコンポーネントの基本構造です。

```javascript
export default class myapp extends Component {
  render() {
}
```

すべてのReactコンポーネントには、React要素を返す `render()` メソッドが必要です。この場合、要素は<Text>要素を含む要素<View>を返します。

```javascript
    return(
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
    ）;
```

「<View>」と「<Text>」要素は、React Nativeアプリの基本的なビルディングブロックです。 `<View>`はレイアウトに使用され、 `<Text>`はテキストレンダリングに使用されます。

最後に、 `StyleSheet`コンポーネントを使用してコンポーネントのスタイルを設定します。

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
}）;
```

StyleSheetは、コンポーネントのスタイルを作成および管理できるコンポーネントです。この場合、これを使用して `myapp` コンポーネント内の `<View>` および `<Text>` 要素のスタイルを指定します。

最後に、`AppRegistry`コンポーネントにコンポーネントを登録します。

```javascript
AppRegistry.registerComponent('myapp', () => myapp);
```

`AppRegistry`はReact Nativeアプリのエントリポイントです。コンポーネントの登録とアプリの実行に使用されます。

最初のReact Nativeアプリを作成したので、他の利用可能なコンポーネントを見てみましょう。

##コンポーネント

React Nativeは、アプリケーションの構築に使用できるさまざまな組み込みコンポーネントを提供しています。

### より

ViewはReact Nativeアプリの基本的なビルディングブロックです。レイアウトに使用され、他のコンポーネントが含まれています。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  View
} from 'react-native';

export default class myapp extends Component {
  render() {
    return(
      <View style={{ flex: 1 }}>
        // other components go here
      </View>
    ）;
  }
}
```

Viewには、レイアウトを制御するために使用できるいくつかの小道具があります。

* `flex`：Viewが占める必要がある親コンポーネントの利用可能なスペースを決定します。デフォルト値は 0 です。
* `flexDirection`：Viewレイアウトの方向を決定します。デフォルトは「列」です。他の可能な値は `row` と `reverse` です。
* `justifyContent`：Viewの子が基本軸に沿って配置される方法を決定します。デフォルトは `flex-start` です。他の可能な値は `center`、`flex-end`、`space-around`、そして`space-between`です。
* `alignItems`：Viewの子が交差軸に沿って配置される方法を決定します。デフォルトは「ストレッチ」です。他の可能な値は `flex-start`、 `center`、および `flex-end`です。

Viewは他のいくつかの小道具もサポートしていますが、最も一般的に使用される小道具です。

###テキスト

テキストはテキストのレンダリングに使用されます。次の小道具をサポートします。

* `style`: Text コンポーネントのスタイルを指定するために使用されます。スタイルオブジェクトは `StyleSheet`コンポーネントと同じ型を使用します。
* `numberOfLines`：レンダリングされるテキスト行の数を制限するために使用されます。デフォルトは「未定義」であり、制限が適用されないことを意味します。

Textは他のいくつかの小道具もサポートしていますが、最も一般的に使用される小道具です。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  Text
} from 'react-native';

export default class myapp extends Component {
  render() {
    return(
      <Text style={{ fontSize: 20 }}>
        Hello, world!
      </Text>
    ）;
  }
}
```

###画像

画像は画像を表示するために使用されます。次の小道具をサポートします。

* `ソース`：表示する画像を指定するために使用されます。値は、数値（静的イメージの場合）、文字列（ネットワークイメージの場合）、またはオブジェクト（ファイルシステムのイメージの場合）です。
* `style`: イメージコンポーネントのスタイルを指定するために使用されます。スタイルオブジェクトは `StyleSheet`コンポーネントと同じ型を使用します。

Imageは他のいくつかの小道具もサポートしていますが、最も一般的に使用される小道具です。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  イメージ
} from 'react-native';

export default class myapp extends Component {
  render() {
    return(
      <画像
        source={{ uri: 'https://facebook.github.io/react/img/logo_og.png' }}
        style={{ width: 400, height: 400 }}
      />
    ）;
  }
}
```

### テキスト入力

TextInputは、ユーザーからテキスト入力を受け取るために使用されます。次の小道具をサポートします。

* `value`：入力の初期値を設定するために使用します。
* `onChangeText`：テキスト入力が変更されるたびに呼び出される関数を設定するために使用されます。関数にテキスト入力の新しい値が渡されます。
* `style`: TextInput コンポーネントのスタイルを指定するために使用されます。スタイルオブジェクトは `StyleSheet`コンポーネントと同じ型を使用します。

TextInputは他のいくつかの小道具もサポートしますが、最も一般的に使用される小道具です。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  TextInput
} from 'react-native';

export default class myapp extends Component {
  コンストラクタ(props) {
    super（props）;
    this.state = {
      text： ''
    };
  }
  
  render() {
    return(
      <TextInput
        style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
        onChangeText={(text) => this.setState({ text })}
        value={this.state.text}
      />
    ）;
  }
}
```

TextInputは、テキスト入力が変更されるたびに `onChangeText`イベントをエクスポートします。 `onChangeText`小道具を使って`text`ステータスプロパティを新しい値に更新する関数を設定しました。また、`value`小道具を使って入力の初期値を設定しました。

###ボタン

ボタンは、ボタンを押してユーザー入力を受け取るために使用されます。次の小道具をサポートします。

* `onPress`：ボタンを押したときに呼び出される機能を設定します。
* `タイトル`：ボタンのタイトルを設定するために使用します。
* `style`: Button コンポーネントのスタイルを指定するために使用されます。スタイルオブジェクトは `StyleSheet`コンポーネントと同じ型を使用します。

Buttonは他のいくつかの小道具もサポートしていますが、最も一般的に使用される小道具です。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  ボタン
} from 'react-native';

export default class myapp extends Component {
  _onPressButton() {
    alert('You pressed the button!');
  }
  
  render() {
    return(
      <ボタン
        onPress={this._onPressButton}
        title="Press Me"
      />
    ）;
  }
}
```

この例では、`_onPressButton`関数を使用してボタンを押したときに警告を表示しました。

## スタイリング

React Nativeは、Reactと同じ「スタイルオブジェクト」の概念を使用します。スタイルオブジェクトは、スタイルプロパティと値を含むJavaScriptオブジェクトです。スタイル属性と値はCSS属性と値と同じです。

スタイルオブジェクトは `StyleSheet`コンポーネントを使って作成できます。

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
}）;
```

`StyleSheet.create`メソッドはスタイルオブジェクトを取得し、パフォーマンスに最適化されたスタイルオブジェクトを返します。

スタイルオブジェクトが作成されたら、 `style`小道具を使用してコンポーネントに適用できます。

```javascript
<Text style={styles.welcome}>
  Hello, world!
</Text>
```

スタイルオブジェクトをインライン化することもできます。

```javascript
<Text style={{ fontSize: 20 }}>
  Hello, world!
</Text>
```

インラインスタイルオブジェクトは `StyleSheet`スタイルオブジェクトと同じ型を使用します。

## プラットフォーム固有のコード

React Nativeを使用すると、プラットフォーム固有のコードを書くことができます。プラットフォーム固有のコードは、特定のプラットフォームでのみ実行されるコードです。

React Nativeはこれに `Platform` APIを提供します。プラットフォームAPIには、プラットフォームを検出するために使用できるいくつかの方法があります。

* `Platform.OS`: プラットフォーム名を返します。可能な値は `ios` と `android` です。
* `Platform.Version`: プラットフォームのバージョンを返します。

`Platform.select`メソッドを使用してプラットフォーム固有のコンポーネントを定義できます。 `Platform.select`メソッドは、キーをReact要素にマッピングするオブジェクトを使用します。キーはプラットフォーム名で、React要素はレンダリングするコンポーネントです。 `Platform.select`メソッドは現在のプラットフォームのReact要素をレンダリングします。

```javascript
import React、{Component} from 'react';
import {
  AppRegistry,
  テキスト、
  View,
  Platform
} from 'react-native';

export default class myapp extends Component {
  render() {
    return(
      <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
        <Text>
          Hello, world!
        </Text>
        {Platform.select({
          ios:
            <Text>
              This is an iOS Device.
            </Text>、
          android:
            <Text>
              This is an Android Device.
            </Text>、
        })}
      </View>
    ）;
  }
}
```

この例では、`Platform.select`メソッドを使用してiOSとAndroidデバイスで異なる `<Text>`要素をレンダリングしました。

プラットフォーム固有のコードは、`Platform.isPad`と`Platform.isTVos`メソッドを使って定義することもできます。

`Platform.isPad`はiPadでは`true`を返し、iPadでは`false`を返します。