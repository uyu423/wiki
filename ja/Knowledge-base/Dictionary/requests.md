---
title: Requests
description: 
published: true
date: 2023-02-08T02:18:02.782Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:18:00.935Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}



- [Requests***English** document is available*](/en/Knowledge-base/Dictionary/requests)
{.links-list}


# 概要

Requests は、Python で書かれた人間向けの Apache2 Licensed HTTP ライブラリです。 Requests を使用すると、ユーザーは指定した URL に対して GET、POST、PUT、DELETE などの HTTP 要求を簡単に行うことができます。また、認証、Cookie、およびその他の機能もサポートしています。

# 説明

Requests は、HTTP リクエストを作成するための一般的な Python ライブラリです。開発者が簡単かつ直感的に使用できるように設計されており、HTTP 要求を作成するプロセスをより簡単にすることに重点が置かれています。 Requests は、GET、POST、PUT、DELETE などの幅広い HTTP 要求をサポートしています。また、認証、Cookie、およびその他の機能のサポートも提供します。

Requests は、人気のある urllib3 ライブラリの上に構築されており、HTTP リクエストを作成するための低レベルのインターフェイスを提供します。 Requests は urllib3 を使用して、HTTP リクエストを作成するための高レベル API を提供し、使いやすくしています。

Requests は、リクエストで送信するデータを指定する機能や、リクエストのタイムアウトを指定する機能など、多くの便利な機能も提供します。

# 歴史

Requests は、もともと 2011 年に Kenneth Reitz によって作成されました。最初は GitHub でオープン ソース プロジェクトとしてリリースされ、すぐに開発者の間で人気を博しました。最初のリリース以来、Requests は最も人気のある Python ライブラリの 1 つになり、ダウンロード数は 1,000 万回を超えています。

# 特徴

Requests には、開発者が HTTP リクエストを簡単に作成できるようにするための多くの機能が用意されています。

- Requests は、GET、POST、PUT、および DELETE を含む幅広い HTTP 要求をサポートします。
- Requests は認証をサポートしているため、開発者は Web サービスで簡単に認証できます。
- リクエストは Cookie をサポートしているため、開発者はリクエストで Cookie を簡単に処理できます。
- Requests はデータをサポートしているため、開発者はリクエストで送信するデータを簡単に指定できます。
- リクエストはタイムアウトをサポートし、開発者がリクエストのタイムアウトを指定できるようにします。

# 例

以下は、Requests を使用して Web サービスに GET 要求を行う例です。

パイソン
インポートリクエスト

応答 = requests.get('http://example.com/api/v1/data')

response.status_code == 200 の場合:
    データ = response.json()
    印刷（データ）
```

# 長所と短所

長所：

- 使いやすい: Requests は、HTTP リクエストを作成するためのシンプルで直感的な API を提供します。
- 幅広いリクエスト: Requests は、GET、POST、PUT、DELETE などの幅広い HTTP リクエストをサポートします。
- 認証: リクエストは認証をサポートしているため、Web サービスでの認証が容易になります。
- Cookies: Requests は Cookie をサポートしているため、リクエストでの Cookie の処理が容易になります。
- データ: リクエストはデータをサポートしているため、リクエストで送信するデータを簡単に指定できます。
- タイムアウト: リクエストはタイムアウトをサポートしているため、リクエストのタイムアウトを簡単に指定できます。

短所：

- 非 HTTP リクエストの制限付きサポート: リクエストは HTTP リクエストのみをサポートするため、非 HTTP リクエストの作成には使用できません。
- ストリーミングのサポートなし: Requests はストリーミングをサポートしていないため、データのストリーミングには使用できません。

# 論争

Requests は、HTTP リクエストを作成するための低レベル ライブラリである urllib3 を使用しているため、いくつかの論争の的となっています。一部の開発者は、urllib3 によってもたらされる潜在的なセキュリティ リスクのために、本番環境でリクエストを使用すべきではないと主張しています。

# 関連技術

- urllib3: urllib3 は、HTTP 要求を作成するための低レベルのライブラリです。 Requests は urllib3 の上に構築されています。
- Requests-toolbelt: Requests-toolbelt は、Requests で HTTP リクエストを作成するためのライブラリです。
- Requests-mock: Requests-mock は、HTTP リクエストを Requests でモックするためのライブラリです。

# 余談

Requests は、Python で HTTP リクエストを作成するための一般的なライブラリです。使いやすいように設計されており、HTTP 要求を簡単に作成できるように幅広い機能を提供します。

# その他

Requests はオープン ソース プロジェクトであり、Apache2 ライセンスの下でリリースされています。積極的にメンテナンスされており、開発者によって広く使用されています。