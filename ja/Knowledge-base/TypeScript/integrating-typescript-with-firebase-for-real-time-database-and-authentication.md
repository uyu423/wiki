---
title: リアルタイム データベースと認証のために TypeScript を Firebase と統合する
description: 
published: true
date: 2023-02-17T18:14:34.972Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:37:39.147Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Integrating TypeScript with Firebase for Real-Time Database and Authentication***English** version of this document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-firebase-for-real-time-database-and-authentication)
{.links-list}

    
    この資料を構成する方法の多くは可能性がありますが、次のセクションはガイドとして機能します。

#はじめに

TypeScriptは、開発者がメンテナンス可能でエラーのないコードを書くことを可能にする強力なプログラミング言語です。 Firebaseは、リアルタイムのデータベースと認証サービスを提供する人気のあるモバイルおよびWebアプリケーション開発プラットフォームです。この記事では、TypeScriptをFirebaseと統合してリアルタイムデータベースと認証システムを作成する方法について説明します。

#タイプスクリプトとは何ですか？

TypeScriptは、開発者がメンテナンス可能でエラーのないコードを記述できるようにするJavaScriptの親セットです。 TypeScriptはJavaScriptでコンパイルされ、既存のJavaScriptコードと簡単に統合できます。 TypeScriptはコンパイル中に型エラーをチェックし、コードにセキュリティ層を追加します。これにより、コードベースにエラーが導入されるのを防ぎ、コードのリファクタリングとデバッグが容易になります。

#ファイアベースとは？

Firebaseは、リアルタイムのデータベースと認証サービスを提供する人気のあるモバイルおよびWebアプリケーション開発プラットフォームです。 Firebaseは使いやすく、小規模なプロジェクトのための無料評価を提供します。 Firebaseのリアルタイムデータベースを使用すると、複数のデバイスでリアルタイムでデータを同期できるため、レスポンシブアプリケーションを簡単に構築できます。 Firebaseの認証サービスを使用すると、アプリケーションにログイン機能と購読機能を簡単に追加できます。

#TypeScriptとFirebaseを統合する方法

このセクションでは、TypeScriptをFirebaseと統合してリアルタイムデータベースと認証システムを作成する方法を説明します。

## Firebaseの設定

Firebaseを使用する前にFirebaseプロジェクトを作成する必要があります。 [Firebaseコンソール]（https://console.firebase.google.com/）に移動し、[プロジェクトの作成]ボタンをクリックします。

プロジェクト名を入力して[プロジェクトの作成]ボタンをクリックします。

プロジェクトが作成されたら、「WebアプリにFirebaseを追加」ボタンをクリックします。

これにより、Firebaseプロジェクトの構成情報を含むモーダルが開きます。後でこの情報が必要なので、クリップボードまたはテキストエディタにコピーしてください。

## Firebase SDKのインストール

次に、Firebase SDKをインストールする必要があります。 npmを使用してこれを行うことができます。ターミナルで次のコマンドを実行してFirebase SDKをインストールします。

```
npm install firebase --save
```

## TypeScriptの設定

TypeScriptはtsconfig.jsonファイルを使用してコンパイラを設定します。 tsconfig.jsonファイルはプロジェクトディレクトリのルートになければなりません。

tsconfig.json ファイルに次のコンテンツを追加します。

```json
{
    "compilerOptions": {
        "target": "es5",
        "module": "commonjs",
        "sourceMap": true
    }
}
```

compilerOptionsセクションで、TypeScriptコンパイラがes5 JavaScriptをターゲットにしてcommonjsモジュール形式を使用するように指定しました。 TypeScriptコードのデバッグに役立つソースマップも有効にしました。

## Firebaseの初期化

Firebase SDKをインストールしてTypeScriptプロジェクトを構成したので、TypeScriptコードでFirebaseを初期化できます。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;
```

firebaseConfig オブジェクトのプレースホルダ値を Firebase プロジェクトの値で置き換えます。

##リアルタイムデータベースの作成

Firebaseのリアルタイムデータベースを使用すると、複数のデバイスでリアルタイムでデータを同期できます。これにより、レスポンシブアプリケーションを簡単に構築できます。

リアルタイムデータベースを作成する前に、データベースへの参照を生成する必要があります。 firebase.database() メソッドを使用してこれを行うことができます。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const database = firebase.database();
```

次に、デバイス間で同期するデータオブジェクトを作成する必要があります。データオブジェクトに message プロパティを追加し、その値を「Hello, world!」に設定します。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const database = firebase.database();

const data = {
    message: "Hello, world!"
};
```

これで、データオブジェクトをデータベースに追加する必要があります。 set() メソッドを使用してこれを行うことができます。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const database = firebase.database();

const data = {
    message: "Hello, world!"
};

database.ref().set(data);
```

これで、データはリアルタイムデータベースに保持されます。 「データ」タブに移動して、Firebaseコンソールでデータを表示できます。

データベースからデータを読み取るには、on（）メソッドを使用できます。 on() メソッドは、イベント型とコールバック関数を引数として使用します。イベントタイプは、「value」、「child_added」、「child_changed」、「child_removed」、「child_moved」のいずれかです。コールバック関数は、イベントタイプがトリガーされるたびに呼び出されます。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const database = firebase.database();

const data = {
    message: "Hello, world!"
};

database.ref().set(data);

database.ref().on("value", (snapshot) => {
    console.log(snapshot.val());
}）;
```

データが更新されるたびにコールバック関数が呼び出され、データがコンソールに書き込まれます。

## 認証の追加

Firebaseの認証サービスを使用すると、アプリケーションにログイン機能と購読機能を簡単に追加できます。 Firebaseは、Google、Facebook、Twitterなど、多くの有名なIDベンダーをサポートしています。このセクションでは、TypeScriptアプリケーションにGoogleログインを追加する方法について説明します。

まず、FirebaseプロジェクトでGoogleログインプロバイダを有効にする必要があります。これを行うには、Firebaseコンソールに移動して[ログイン方法]タブをクリックします。

次に、「Google」ログインプロバイダをクリックして有効にします。

これで、Googleログインプロバイダを使用するようにTypeScriptプロジェクトを設定する必要があります。プロバイダIDをfirebase.auth.GoogleAuthProvider（）メソッドに渡すだけです。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();
```

これでログインプロバイダを設定したので、HTMLファイルにログインボタンを追加できます。

src/index.html ファイルに次のコードを追加します。

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>TypeScript with Firebase</title>
</head>

<body>
    <button id="sign-in">Sign in with Google</button>
</body>

</html>
```

次に、ログインボタンにイベントリスナーを追加する必要があります。ボタンをクリックすると、Googleアカウントでログインします。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup（provider）;
}）;
```

ログインボタンをクリックすると、Googleアカウントでログインするように求められます。

ログインすると、firebase.auth().currentUser プロパティを使用してユーザー情報にアクセスできます。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup（provider）;
}）;

auth.onAuthStateChanged((user) => {
    if(user){
        console.log(user.displayName);
    }
}）;
```

Google アカウントでログインすると、名前がコンソールに記録されます。

## ログアウトする

このセクションでは、アプリケーションにログアウトボタンを追加する方法について説明します。

まず、HTMLファイルにログアウトボタンを追加する必要があります。

src/index.html ファイルに次のコードを追加します。

```html
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>TypeScript with Firebase</title>
</head>

<body>
    <button id="sign-in">Sign in with Google</button>
    <button id="sign-out">Sign out</button>
</body>

</html>
```

次に、ログアウトボタンにイベントリスナーを追加する必要があります。ボタンをクリックすると、Googleアカウントからログアウトします。

src/index.ts ファイルに次のコードを追加します。

```typescript
import firebase from "firebase";

const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_AUTH_DOMAIN",
    databaseURL: "YOUR_DATABASE_URL",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "",
    messagingSenderId: "YOUR_MESSAGING_SENDER_ID"
};

firebase.initializeApp（firebaseConfig）;

const auth = firebase.auth();

const provider = new firebase.auth.GoogleAuthProvider();

const signInButton = document.getElementById("sign-in");

signInButton.addEventListener("click", () => {
    auth.signInWithPopup（provider）;
}）;

const signOutButton = document.getElementById("sign-out");

signOutButton.addEventListener("click", () => {
    auth.signOut();
}）;

auth.onAuthStateChanged((user) => {
    if(user){
        console.log(user.displayName);
    }
}）;
```

[ログアウト]ボタンをクリックすると、Googleアカウントからログアウトされます。

#結論

この記事では、TypeScriptをFirebaseと統合してリアルタイムデータベースと認証システムを作成する方法について説明しました。この記事が役立つことを願っています。ご質問がございましたら、下記にコメントを残してください。