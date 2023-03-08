---
title: TypeScript と Three.js を使用した拡張現実アプリケーションの構築
description: 
published: true
date: 2023-01-31T17:17:19.034Z
tags: 
editor: markdown
dateCreated: 2023-01-31T17:17:17.453Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Building Augmented Reality Applications with TypeScript and Three.js***English** version of this document is available*](/en/Knowledge-base/TypeScript/building-augmented-reality-applications-with-typescript-and-three-js)
{.links-list}



#TypeScriptとThree.jsで拡張現実アプリケーションを構築する

ARKitとARCoreの発売により、拡張現実（AR）がさらに主流となっています。この新しいSDKにより、開発者はiOSおよびAndroidデバイスで何百万人ものユーザーのためのAR体験を作成できます。

しかし、ARアプリケーションの開発は難しいかもしれません。 SDKは継続的に変更され、開発者が始めるのに役立つリソースはほとんどありません。

この記事では、TypeScriptとThree.jsを使用してWeb用のARアプリケーションを作成する方法について説明します。開発環境の設定、簡単なARシーンの作成、Webサーバーへのアプリケーションのデプロイについて説明します。

##開発環境設定

ARアプリケーションの構築を開始する前に、開発環境を設定する必要があります。

まず、[Node.js]（https://nodejs.org/en/）をインストールする必要があります。 Node.jsは、Webブラウザの外部でJavaScriptコードを実行できるJavaScriptランタイムです。 Node.jsを使用してアプリケーション用のローカルWebサーバーを実行します。

次に、[TypeScript]（https://www.typescriptlang.org/）をインストールする必要があります。 TypeScript は、静的型チェックやその他の機能を追加する JavaScript の親セットです。 TypeScriptを使用してARアプリケーションを作成します。

最後に、[Three.js]（https://threejs.org/）をインストールする必要があります。 Three.jsは3Dグラフィックを作成するためのJavaScriptライブラリです。 Three.jsを使用してARシーンを作成します。

##シンプルなARシーンの作成

これで開発環境が設定されたので、ARシーンを作成できます。

まず、新しいTypeScriptファイルを作成してThree.jsをインポートする必要があります。

```typescript
import * as THREE from 'three';
```

次に、新しいThree.jsシーンを作成する必要があります。

```typescript
const scene = new THREE.Scene();
```

これで、シーンにいくつかのオブジェクトを追加できます。簡単なキューブから始めましょう。

```typescript
const geometry = new THREE.BoxGeometry(1, 1, 1);
const material = new THREE.MeshBasicMaterial({ color: 0xff0000 });
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

最後に、シーンをレンダリングする必要があります。

```typescript
const renderer = new THREE.WebGLRenderer();
renderer.setSize（window.innerWidth、window.innerHeight）;
document.body.appendChild(renderer.domElement);

renderer.render(scene, camera);
```

すべてがうまくいったら、Webブラウザに赤いキューブを表示する必要があります。

## アプリケーションのデプロイ

これでデフォルトのARシーンがあるので、それをWebサーバーに展開する必要があります。

まず、[http-server]（https://www.npmjs.com/package/http-server）Node.jsモジュールをインストールする必要があります。

```
npm install -g http-server
```

次に、TypeScriptコードをJavaScriptにコンパイルする必要があります。

```
tsc main.ts
```

最後に、Webサーバーを起動できます。

```
http-server
```

これで http://localhost:8080 からアプリケーションにアクセスできるようになります。

##結論

この記事では、TypeScriptとThree.jsを使用してWeb用のARアプリケーションを作成する方法について説明しました。これまで、開発環境の設定、簡単なARシーンの作成、Webサーバーへのアプリケーションのデプロイについて説明しました。

AR開発の詳細については、次のリソースを確認してください。

- [ARKit 101](https://www.raywenderlich.com/160517/arkit-101-using-arkit-build-augmented-reality-apps)
- [ARCore 101](https://www.raywenderlich.com/166886/arcore-101-arkit-equivalent-android)
- [A-フレーム](https://aframe.io/)