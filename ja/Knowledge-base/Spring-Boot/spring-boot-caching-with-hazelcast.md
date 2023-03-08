---
title: Hazelcast を使用した Spring Boot キャッシング
description: 
published: true
date: 2023-01-31T22:18:01.270Z
tags: 
editor: markdown
dateCreated: 2023-01-31T22:17:59.604Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Spring Boot Caching with Hazelcast***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-caching-with-hazelcast)
{.links-list}


# Hazelcastを使用したSpring Boot Caching

キャッシュは、すべての高性能アプリケーションの重要なコンポーネントです。応答時間を大幅に改善し、アプリケーションサーバーの負荷を軽減できます。

利用可能な多くのキャッシュソリューションがありますが、最も人気のあるソリューションの1つはHazelcastです。 Hazelcastは、Spring Bootアプリケーションと簡単に統合できるオープンソースの分散キャッシュソリューションです。

この記事では、Spring BootアプリケーションでキャッシュにHazelcastを使用する方法について説明します。簡単な例から始めて、Hazelcastが提供する必要がある高度な機能のいくつかを見てみましょう。

##ヘイズキャスト設定

最初にすべきことは、Hazelcastインスタンスを設定することです。 Hazelcast Spring Boot Starterを使用してこれを行うことができます。

プロジェクトにスターターを追加するには、ビルドファイルに次の依存関係を追加するだけです。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-hazelcast</artifactId>
</dependency>
```

スタータがプロジェクトに追加されると、アプリケーションの実行時に Hazelcast が自動的に設定され起動されます。

## Hazelcastによるキャッシュ

これでHazelcastを起動して実行したので、それをキャッシュに使用する方法を見てみましょう。

簡単な例から始めましょう。ユーザーのリストを返すサービスがあるとします。

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    ）;

    public List<User> getUsers() {
        return users;
    }
}
```

このサービスはRESTコントローラによって呼び出されます。

```java
@RestController
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.getUsers();
    }
}
```

`getUsers`メソッドの結果をキャッシュして、このコントローラのパフォーマンスを向上させることができます。

```java
@RestController
public class UserController {

    private final UserService userService;

    private final HazelcastInstance hazelcastInstance;

    public UserController(UserService userService, HazelcastInstance hazelcastInstance) {
        this.userService = userService;
        this.hazelcastInstance = hazelcastInstance;
    }

    @GetMapping("/users")
    public List<User> getUsers() {
        List<User> users = hazelcastInstance.getList("users");
        if(users == null) {
            users = userService.getUsers();
            hazelcastInstance.setList("users", users);
        }
        return users;
    }
}
```

この例では、 `list`をキャッシュとして使用しています。 Hazelcastは `Map`、`Set`、`Queue`構造もサポートしています。

個々のメソッドの結果をキャッシュすることもできます。

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    ）;

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }
}
```

この場合、キャッシュを明示的に構成する必要はありません。 Spring Bootは自動的にキャッシュマネージャを設定し、`getUsers`メソッドの結果をキャッシュします。

## キャッシュからエントリを削除

エントリがキャッシュされると、明示的に削除されるまでキャッシュに残っていることを覚えておくことが重要です。これにより、基本データが変更されると、古いデータが返される可能性があります。

`@CacheEvict`アノテーションを使用してキャッシュからエントリを削除できます。

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    ）;

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict("users")
    public void evictUsers() {
    }
}
```

この例では、`@CacheEvict`で`evictUsers`メソッドにコメントを追加しました。これにより、メソッドが呼び出されたときに `users`キャッシュがクリアされます。

`@CacheEvict(allEntries = true)` コメントを使用して、すべてのキャッシュからすべてのエントリを削除することもできます。

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    ）;

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CacheEvict(allEntries = true)
    public void evictAll() {
    }
}
```

## キャッシュされたアイテムの更新

`@CachePut`コメントを使ってキャッシュされたエントリを更新することもできます。

```java
@Service
public class UserService {

    private final List<User> users = Arrays.asList(
            new User(1, "John"),
            new User(2, "Jane"),
            new User(3, "Joe")
    ）;

    @Cacheable("users")
    public List<User> getUsers() {
        return users;
    }

    @CachePut("users")
    public List<User> updateUsers() {
        return users;
    }
}
```

この例では、 `updateUsers`メソッドは `@CachePut`としてコメントされています。これにより、メソッドが呼び出されたときに `users`キャッシュが更新されます。

##結論

この記事では、Spring BootアプリケーションでキャッシュにHazelcastを使用する方法について説明しました。 Hazelcastの設定方法とそれをデータキャッシュに使用する方法を見てきました。また、キャッシュからアイテムを削除する方法と、キャッシュされたアイテムを更新する方法についても説明しました。

キャッシュは、すべての高性能アプリケーションの重要なコンポーネントです。 Hazelcastを使用すると、Spring Bootアプリケーションにキャッシュを簡単に追加できます。