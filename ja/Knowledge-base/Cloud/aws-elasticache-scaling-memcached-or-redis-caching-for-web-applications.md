---
title: AWS Elasticache: Web アプリケーションの Memcached または Redis キャッシングのスケーリング
description: 
published: true
date: 2023-02-17T18:14:46.059Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:43:20.570Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [AWS Elasticache: Scaling Memcached or Redis Caching for Web Applications***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-elasticache-scaling-memcached-or-redis-caching-for-web-applications)
{.links-list}


#AWS Elasticache：Webアプリケーション用のMemcachedまたはRedisキャッシュ拡張

##はじめに

Elasticacheは、クラウド内のメモリ内キャッシュを簡単に展開、運用、および拡張できるWebサービスです。低速のディスクベースのデータベースに依存するのではなく、迅速に管理されたメモリ内システムから情報を取得してパフォーマンスを向上させます。

Elasticacheは、2つのオープンソースインメモリキャッシュエンジンであるMemcachedとRedisをサポートしています。この記事では、2つのエンジンを簡単に比較し、各エンジンを使用する場合について説明します。 Elasticacheを最大限に活用する方法についてのヒントもいくつかあります。

## メンカシド

Memcachedは単純な高性能キーと値のキャッシュです。外部データソース（データベースまたはAPIなど）にアクセスする必要がある回数を減らすために、データとオブジェクトをRAMにキャッシュして動的データベースベースのWebサイトを高速化するためによく使用されます。

Memcachedは使いやすく配布が簡単です。単純なデータキャッシュが必要なWebアプリケーションに広く使用されている選択肢です。

##レディス

Redisは強力で多様なKey-Valueキャッシュです。文字列、ハッシュ、リスト、セット、ソートされたセットなどのデータ構造をサポートします。したがって、より複雑なデータキャッシュが必要なアプリケーションに適しています。

RedisはMemcachedよりも設定と管理が難しいですが、より多くの機能と柔軟性を提供します。

## Memcachedを使用している場合

Memcachedは、単純なキャッシュを必要とするWebアプリケーションに適した選択です。アプリケーションがキーと値のペアのデータのみをキャッシュする必要がある場合は、Memcachedが適切なソリューションかもしれません。

設定と管理が簡単なシンプルなキャッシュソリューションを探している場合は、Memcachedも良い選択です。

## Redisを使用している場合

Redisは、より複雑なデータ構造をキャッシュする必要があるWebアプリケーションに適しています。アプリケーションがリスト、セット、またはソートされたセットのデータをキャッシュする必要がある場合は、Redisが適切なソリューションかもしれません。

より多くの機能と柔軟性を提供するより強力なキャッシュソリューションを探しているなら、Redisも良い選択です。

## Elasticacheの使い方

Elasticacheを最大限に活用するには、次のヒントを念頭に置いてください。

- 複数のWebアプリケーションに単一のElasticacheクラスタを使用します。これにより、コストを削減し、管理オーバーヘッドを削減できます。

- ElastiCache 自動検出を使用して ElastiCache クラスター展開を簡素化します。 Auto Discoveryを使用すると、アプリケーションをElastiCacheに簡単に接続でき、作成された新しいElastiCacheクラスタを自動的に検出して登録できます。

- MySQL 用 Amazon Relational Database Service (Amazon RDS) と共に Memcached 用 ElastiCache を使用します。 ElastiCacheは、MySQLデータベースを使用するWebアプリケーションのパフォーマンスを大幅に向上させることができます。

- Amazon ElastiSearchでRedis用のElastiCacheを使用します。 ElastiCacheは、ElastiSearchを使用するWebアプリケーションのパフォーマンスを大幅に向上させることができます。

##結論

Elasticacheは、クラウド内のメモリ内キャッシュを簡単に展開、運用、および拡張できるWebサービスです。 MemcachedとRedisという2つのオープンソースインメモリキャッシュエンジンをサポートしています。

Memcachedは単純な高性能キーと値のキャッシュです。外部データソース（データベースまたはAPIなど）にアクセスする必要がある回数を減らすために、データとオブジェクトをRAMにキャッシュして動的データベースベースのWebサイトを高速化するためによく使用されます。

Redisは強力で多様なKey-Valueキャッシュです。文字列、ハッシュ、リスト、セット、ソートされたセットなどのデータ構造をサポートします。したがって、より複雑なデータキャッシュが必要なアプリケーションに適しています。

Elasticacheを最大限に活用するには、複数のWebアプリケーションに単一のElasticacheクラスタを使用し、ElastiCache Auto Discoveryを使用してElastiCacheクラスタの展開を簡素化します。