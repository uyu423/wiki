---
title: REST
description: 
published: true
date: 2023-02-17T18:09:23.792Z
tags: 
editor: markdown
dateCreated: 2023-01-30T17:17:31.226Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [REST***English** version of this document is available*](/en/Knowledge-base/Dictionary/rest)
{.links-list}


#Overview

REST（Representational State Transfer）は、Webサービスなどの分散システムを設計するためのアーキテクチャスタイルです。クライアント - サーバーアーキテクチャとステートレスストレージ通信の原則に基づいています。

#History

RESTは、2000年にRoy Fieldingが博士論文の一部として最初に提案しました。彼は、RPCやSOAPなどの既存のアーキテクチャが過度に複雑で、Webがどのように機能するかを反映していないと主張しました。

#description

RESTは、クライアントとサーバーが同じインターフェースを使用して通信できるという考えに基づいています。このインタフェースは、Web上のコンピュータ間でデータを交換するために使用されるプロトコルである**HTTP**の原則に基づいています。 **無状態**として設計され、クライアントからの各要求は独立したトランザクションとして処理され、サーバーは要求間でクライアントに関する情報を保持しません。

RESTアーキテクチャの主なコンポーネントは、**リソース**、**表現**、および**作業**です。リソースは、ユーザーや本などのシステムの基本要素です。表現は、HTML文書やJSONオブジェクトなど、クライアントとサーバー間で交換されるデータです。アクションは、リソースの作成、更新、削除など、リソースで実行できるアクションです。

RESTは**ハイパーメディア**の概念に依存しています。これは、サーバーが応答内の他の関連リソースへのリンクを提供できるという考えです。たとえば、書籍リクエストへの回答には、著者のプロフィールページへのリンクが含まれる場合があります。これにより、クライアントは追加の要求なしで追加情報にアクセスできます。

#余談

RESTはまた、**キャッシュ**を使用できるようにすることで、クライアントとサーバー間で転送する必要があるデータ量を減らしてシステムのパフォーマンスを向上させることができます。

RESTは、**バージョン管理**の概念をサポートしているため、既存のクライアントを損傷することなく新しいバージョンのAPIをリリースできます。これは、URLにバージョン情報を含め、同時に複数のバージョンのAPIをサポートすることによって達成されます。

#関連リンク
- [RESTful Webサービス*O'Reilly Media*](https://www.oreilly.com/library/view/restful-web-services/9780596155860/)
- [REST API チュートリアル*REST API チュートリアル*](https://restapitutorial.com/)
- [REST*Google開発者紹介*]（https://developers.google.com/drive/api/v3/about-rest）
{.links-list}