---
title: Service-Oriented Architecture
description: 
published: true
date: 2023-01-31T05:43:41.898Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:43:38.575Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Service-Oriented Architecture***English** version of this document is available*](/en/Knowledge-base/Dictionary/service-oriented-architecture)
{.links-list}


#Overview

SOA（Service-Oriented Architecture）は、高度にモジュール化され、スケーラブルでメンテナンスが容易なアプリケーションとサービスを作成するためにソフトウェア開発に使用されるアーキテクチャスタイルです。 SOAP（Simple Object Access Protocol）などのWebサービスプロトコルを介して通信する疎結合サービスに基づいています。このタイプのアーキテクチャは、プラットフォーム、言語、およびハードウェアとは独立した分散ソフトウェアアプリケーションを開発するために使用されます。

#History

SOA（Service-Oriented Architecture）は、2000年代初頭にコンピュータサイエンティストであり、ソフトウェアエンジニアであるDavid Chappellがますます維持するのが難しくなってきた、従来のモノリシックアーキテクチャに代わるものとして初めて提案しました。 Chappellは、ソフトウェア開発のよりモジュール化されたスケーラブルなアプローチでSOAを開発しました。

その後数年間、SOAは推進力を獲得し、多くの組織で広く採用されています。これにより、リソースをより効率的に使用でき、複数のプラットフォームや言語で使用できるサービス開発が可能になりました。

#description

サービス指向アーキテクチャでは、アプリケーションは緩く結合され、独立してデプロイできる小さな、独立したサービスに分けられます。これらのサービスは、SOAP（Simple Object Access Protocol）などのWebサービスプロトコルを介して互いに通信します。これにより、ソフトウェア開発に対するよりモジュール化されたスケーラブルなアプローチが可能になり、アプリケーションをより簡単に保守できます。

サービス指向アーキテクチャのサービスは、しばしばワークフローで実装されるビジネスプロセスに基づいています。その後、このワークフローは、複数のアプリケーションで再利用できる個々のサービスに分類されます。

たとえば、請求書を生成するためのワークフローには、請求書生成サービス、請求書のPDF版を作成するための別のサービス、および顧客に請求書を送信するサービスが含まれます。これらの各サービスは、会計システムやカスタマーサービスシステムなどの他のアプリケーションで使用できます。

#yes

サービス指向アーキテクチャの簡単な例を見てみましょう。

人々がエネルギー料金を節約するのに役立つWebベースのアプリケーションを構築すると想像してください。このアプリケーションは、エネルギープロバイダ、使用量データ、顧客情報など、複数のソースからのデータにアクセスする必要があります。

サービス指向アーキテクチャでは、これらのデータソースごとに別々のサービスを作成できます。例えば、エネルギープロバイダサービスはエネルギー価格に関するデータを提供し、使用量データサービスはエネルギー使用量に関するデータを提供し、顧客情報サービスは顧客人口統計に関するデータを提供する。

その後、これらのサービスをWebアプリケーションに統合し、ユーザーのレポートやその他の情報を生成するために使用できます。これにより、アプリケーションのメンテナンスが容易になり、あるサービスに対する変更が他のサービスに影響を与えないようになります。

#長所と短所

サービス指向アーキテクチャの主な利点は、ソフトウェア開発へのよりモジュール化されたアプローチを可能にすることです。これにより、アプリケーションをより簡単に保守でき、開発者は複数のアプリケーションでコンポーネントを再利用できます。また、サービスを独立してデプロイできるため、アプリケーションをより簡単に拡張できます。

しかし、サービス指向アーキテクチャの使用にはいくつかの潜在的な欠点があります。たとえば、複数のサービスで一貫した状態を維持するのが難しく、サービスが正しく設計されていない場合、サービス間で競合が発生する可能性があります。さらに、サービスには定期的な更新とテストが必要なため、メンテナンスコストが高くなる可能性があります。

#関連リンク

- [サービス指向アーキテクチャ（SOA）とは？ (英語) *Techopedia*](https://www.techopedia.com/definition/28817/service-oriented-architecture-soa)
- [サービス指向アーキテクチャ(英語) *Wikipedia*](https://en.wikipedia.org/wiki/Service-oriented_architecture)
- [サービス指向アーキテクチャ(Français) *Wikipedia*](https://fr.wikipedia.org/wiki/Architecture_orient%C3%A9e_services)
{.links-list}