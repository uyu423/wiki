---
title: Spring Boot でのキャッシュ戦略
description: 
published: true
date: 2023-01-31T08:07:37.626Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:07:36.076Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Caching Strategies in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/caching-strategies-in-spring-boot)
{.links-list}


# Spring Bootのキャッシュ戦略

Spring Bootは、静的および動的データキャッシュにすぐに利用可能ないくつかの機能を提供します。この記事では、それぞれの長所と短所を含め、Spring Bootで使用される最も人気のあるキャッシュ戦略を紹介します。

# #静的データキャッシュ

キャッシュの最も単純な形式は、頻繁に変更されない静的データをキャッシュすることです。これは@Cacheableアノテーションを使用して行うことができます。たとえば、ユーザーのリストを返すスローサービスがある場合は、次のコードを使用して結果をキャッシュできます。

```java
@Cacheable(value = "users")
public List<User> getAllUsers() {
  // Slow service call
}
```

これにより、サービス呼び出しの結果が "users"キーと共にキャッシュに保存されます。次にサービスを呼び出すと、遅いサービス呼び出しを行うのではなく、キャッシュされた結果が返されます。

# #動的データキャッシュ

動的データキャッシュは少し複雑ですが、データベースやその他のリソースへの負荷を軽減するのに非常に役立ちます。取ることができるいくつかのアプローチがあります。

# ##キャッシュ除外

キャッシュ除外パターンは、データベースまたは他の低速リソースから読み取られたデータをキャッシュするための一般的なアプローチです。基本的なアイデアは、まず要求されたデータのキャッシュを確認することです。データがキャッシュにない場合は、低速なリソースから取得され、キャッシュに保存されます。このパターンは、次のコードを使用して実装できます。

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(String id) {
  // Check cache
  User user = cache.get(id);
  
  // If not in cache, fetch from database
  if(user==null){
    user = database.get(id);
    
    // Store in cache
    cache.put(id, user);
  }
  
  return user;
}
```

まず、特定のIDを持つユーザーのキャッシュを確認します。ユーザーがキャッシュにない場合は、データベースからインポートされ、キャッシュに保存されます。次に同じユーザーが要求されると、キャッシュされたコピーが返されます。

# ##を読む

データキャッシュのもう一つの一般的なパターンは読取りキャッシュである。このパターンはキャッシュ除外パターンと似ていますが、データは常に低速リソースから取得されます。結果はキャッシュに保存され、呼び出し元に返されます。このパターンは、次のコードを使用して実装できます。

```java
@Cacheable(value = "users", key = "#id")
public User getUserById(String id) {
  // Fetch from database
  User user = database.get(id);
  
  // Store in cache
  cache.put(id, user);
  
  return user;
}
```

これにより、データベースからユーザーがインポートされ、結果がキャッシュに保存されます。次に同じユーザーが要求されると、キャッシュされたコピーが返されます。

# #正しいキャッシュ戦略を選択

すべての状況に対して完璧なキャッシュ戦略はありません。正しい戦略は、キャッシュされるデータ、システムの期待される負荷、およびその他の要因によって異なります。

# ##静的データ

頻繁に変更されない静的データの場合、最も簡単な解決策は@Cacheableアノテーションを使用することです。これにより、データがキャッシュに保存され、後続の要求によって返されます。

# ##動的データ

動的データの場合、キャッシュ戦略の選択はいくつかの要因に依存します。データを頻繁に読み込み、システムの負荷が高い場合は、キャッシュ除外または読み取りキャッシュが最良の選択である可能性があります。データの読み取り頻度が低い場合やシステム負荷が低い場合は、キャッシュ除外パターンで十分です。