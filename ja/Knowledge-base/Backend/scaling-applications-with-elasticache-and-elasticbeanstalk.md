---
title: ElastiCache と ElasticBeanstalk を使用したアプリケーションのスケーリング
description: 
published: true
date: 2023-02-17T18:14:23.567Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:23:16.327Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Scaling Applications with ElastiCache and ElasticBeanstalk***English** version of this document is available*](/en/Knowledge-base/Backend/scaling-applications-with-elasticache-and-elasticbeanstalk)
{.links-list}
 

## ElastiCacheとElasticBeanstalkでアプリケーションを拡張する

この記事では、アプリケーションの拡張に役立つ2つのAmazon Web Services（AWS）製品、ElastiCacheとElastic Beanstalkについて説明します。これらの製品のしくみと、アプリケーションを拡張するために使用できる方法について説明します。

ElastiCacheは、クラウド内のインメモリキャッシュを簡単に展開、運用、および拡張できるWebサービスです。 ElastiCacheは、2つのオープンソースキャッシュエンジンであるMemcachedとRedisをサポートしています。

Elastic Beanstalk は、AWS クラウドでウェブアプリケーションを簡単にデプロイおよび管理できるようにするウェブサービスです。 Elastic Beanstalkは、Webアプリケーションをデプロイおよび実行するためのプラットフォームを提供します。容量プロビジョニング、ロードバランシング、拡張、およびアプリケーションの状態監視の詳細を自動的に処理します。

Elastic Beanstalk で ElastiCache を使用する場合は、ElastiCache の垂直方向と水平方向の拡張機能を利用できます。垂直拡張とは、アプリケーションで使用できるメモリ量および/またはCPUの数を増やすことを意味します。水平拡張とは、キャッシュクラスタにさらにノードを追加することを意味します。

ElastiCacheは、キャッシュクラスタにノードを追加して垂直方向に拡張できます。水平方向に拡張するには、ElastiCacheクラスタにノードを追加するだけです。シャーディングを使用して水平に拡張することもできます。シャーディングは、データを複数のノードに分散させる技術です。

Elastic Beanstalkは、環境にWebサーバーを追加して水平方向に拡張できます。 Webサーバーで利用可能なメモリ量および/またはCPUの数を増やして垂直方向に拡張することもできます。

以下は、ElastiCacheとElastic Beanstalkを使用してアプリケーションを拡張するためのヒントです。

– ElastiCache を使用して頻繁にアクセスするデータをキャッシュします。キャッシュはデータベースへの移動回数を減らし、アプリケーションのパフォーマンスを向上させることができます。

- Elastic Beanstalkを使用してWebアプリケーションをデプロイおよび管理します。 Elastic Beanstalkは、Webアプリケーションをデプロイおよび実行するためのプラットフォームを提供します。容量プロビジョニング、ロードバランシング、拡張、およびアプリケーションの状態監視の詳細を自動的に処理します。

- ElastiCache を Elastic Beanstalk と共に使用して、ElastiCache の垂直および水平拡張機能を活用します。垂直拡張とは、アプリケーションで使用できるメモリ量および/またはCPUの数を増やすことを意味します。水平拡張とは、キャッシュクラスタにさらにノードを追加することを意味します。

- シャーディングを使用してElastiCacheを水平方向に拡張します。シャーディングは、データを複数のノードに分散させる技術です。

- Elastic Beanstalk を使用して環境に Web サーバーを追加し、水平方向に拡張します。 Webサーバーで利用可能なメモリ量および/またはCPUの数を増やして垂直方向に拡張することもできます。