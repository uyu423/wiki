---
title: React
description: 
published: true
date: 2023-01-31T13:57:54.477Z
tags: 
editor: markdown
dateCreated: 2023-01-31T13:57:52.918Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [React***English** version of this document is available*](/en/Knowledge-base/Dictionary/react)
{.links-list}


#Overview
Reactはユーザーインターフェースを構築するためのJavaScriptライブラリです。 Facebookと個々の開発者と会社のコミュニティによって維持されます。 Reactは、単一ページまたはモバイルアプリケーション開発の基盤として使用できます。

#History
ReactはFacebookのソフトウェアエンジニアであるJordan Walkeによって作成されました。彼は2011年に「FaxJS」というReactの初期プロトタイプを初めて発売しました。 Reactの最初の公開リリースは2013年5月29日でした。それ以来、Reactはユーザーインターフェースを構築するための最も人気のあるJavaScriptライブラリの1つになりました。

#description
Reactはユーザーインターフェースを構築するためのJavaScriptライブラリです。 Webアプリケーションで利用可能な再利用可能なコンポーネントを作成するために使用されます。 Reactはシンプルで効率的で柔軟に設計されています。宣言的なプログラミングスタイルを使用すると、読みやすく理解しやすくなります。

#特徴
Reactには、Web開発に広く使用されているいくつかの機能があります。これには以下が含まれます。

- **仮想DOM：** Reactは仮想DOMを使用してUIを効率的に更新します。これにより、Reactはページ全体を再レンダリングしなくてもUIを変更できます。

- **JSX:** React は、開発者が JavaScript コードで HTML と同様の構文を作成できるようにする JSX という構文拡張を使用します。

- **React Native：** React Nativeは、開発者がReactを使用してiOSおよびAndroid用の基本アプリを作成できるモバイル開発フレームワークです。

- **Flux：** Fluxは、アプリケーション内のデータフローを管理するのに役立つReact用のアプリケーションアーキテクチャです。

- **サーバー側のレンダリング：** Reactはサーバー側のレンダリングをサポートしているため、開発者はReactコンポーネントをクライアントに送信する前にサーバーからレンダリングできます。

#yes
以下は、アイテムのリストを表示するReactコンポーネントの例です。

```javascript
import React from 'react';

class List extends React.Component {
  render() {
    return(
      <ul>
        {this.props.items.map(item => (
          <li key={item.id}>{item.name}</li>
        ))}
      </ul>
    ）;
  }
}
```

#長所と短所
Reactにはいくつかの利点があります。

- **簡単に学ぶ：** Reactは学び、使いやすく、あらゆる技術レベルの開発者に適しています。

- **パフォーマンス：** Reactの仮想DOMとサーバー側のレンダリングは高速で効率的です。

- **再利用可能なコンポーネント：** Reactコンポーネントは再利用可能なので、複雑なユーザーインターフェイスを簡単に作成できます。

しかし、Reactの使用には、次のようないくつかの欠点もあります。

- **急な学習曲線：** Reactは、ライブラリを初めて使用する開発者が学習するのが難しい場合があります。

- **文書の欠如:** Reactのドキュメントは理解しにくくなる可能性があり、開発者が起動しにくい場合があります。

#議論
ReactはJSX構文を使用しているため、議論の対象となりました。一部の開発者は、JSXが「本物の」プログラミング言語ではなく、Web開発に使用してはならないと主張しています。他の人々は、JSXが複雑なユーザーインターフェースをより簡単に作成できるようにする強力なツールであると主張しました。

#関連技術
Reactはしばしば次のような他の技術と組み合わせて使用されます。

- **Redux：** Reduxは、アプリケーション内のデータフローを管理するのに役立つReact用の状態管理ライブラリです。

- **GraphQL：** GraphQLは、サーバーからデータをより簡単に取得できるAPI用のクエリ言語です。

- **TypeScript:** TypeScript は、React アプリケーションに型安全性を追加する型付き JavaScript 親セットです。

#余談
Reactは、ユーザーインターフェイスを構築するための最も人気のあるJavaScriptライブラリの1つになりました。 Facebook、Airbnb、Netflixなどの多くの大企業で使用されています。 Reactは、InstagramやUberなどの最も人気のあるモバイルアプリを作成するためにも使用されました。

#その他
Reactはオープンソースプロジェクトであり、MITライセンスとして配布されています。つまり、手数料やロイヤリティを支払うことなく、誰でも無料でReactを使用できます。 Reactはまた、大規模な開発者コミュニティで積極的にメンテナンスおよびサポートしています。