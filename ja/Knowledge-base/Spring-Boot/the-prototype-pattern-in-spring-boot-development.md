---
title: Spring Boot 開発におけるプロトタイプ パターン
description: 
published: true
date: 2023-01-31T15:43:32.938Z
tags: 
editor: markdown
dateCreated: 2023-01-31T15:43:31.382Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [The Prototype Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-prototype-pattern-in-spring-boot-development)
{.links-list}


#Spring Boot開発のプロトタイプパターン

プロトタイプパターンは、オブジェクトを最初から新しくするオーバーヘッドを避けながらオブジェクトを複製できる生成デザインパターンです。 Springでは、Prototypeスコープは一度だけ使用されるBeanを生成するために使用されます。これは、同じ構成で多数のBeanを作成する必要がある場合に便利です。

プロトタイプBeanを作成すると、SpringはリクエストごとにBeanの新しいインスタンスを作成します。これは、データベースで照会する必要があるオブジェクトなど、作成コストが高いBeanに役立ちます。

Prototype スコープを使用するには、空のクラスに @Scope("prototype") アノテーションを追加できます。これは、各リクエストに対してBeanの新しいインスタンスを作成するようにSpringに指示します。

たとえば、データベースを照会する必要があるBeanがあるとします。 @Scope("prototype") アノテーションを使用して、この Bean にアノテーションを付けて、各リクエストに対して新しいインスタンスを作成できます。これにより、各要求に独自のデータベース接続があります。

```java
@Scope("prototype")
@Component
public class MyBean {
   ...
}
```

プロトタイプBeanをシングルトンBeanに注入する必要がある場合は、@Autowiredアノテーションを使用できます。これは、各リクエストに対してプロトタイプBeanの新しいインスタンスを作成するようにSpringに指示します。

```java
@Autowired
MyBean myBean;
```

@Resourceアノテーションを使用して、プロトタイプBeanをシングルトンBeanに注入することもできます。これは、各リクエストに対してプロトタイプBeanの新しいインスタンスを作成するようにSpringに指示します。

```java
@Resource(name="myBean")
MyBean myBean;
```

Prototypeスコープを使用するときは、各要求が一意のBeanインスタンスを取得することを念頭に置くことが重要です。これは、Beanに保存されているすべてのステータスがリクエスト間で共有されるわけではありません。

プロトタイプBean間で状態を共有する必要がある場合は、ThreadLocalクラスを使用できます。このクラスを使用すると、スレッドセーフな方法でデータを保存できます。

```java
@Scope("prototype")
@Component
public class MyBean {
   private ThreadLocal <Integer> count = new ThreadLocal <Integer>（）;

   public void increment() {
      count.set(count.get() + 1);
   }

   public int getCount() {
      return count.get();
   }
}
```

上記の例では、数を格納するためにThreadLocalを使用しています。これにより、各要求が独自の数を取得します。

Prototype の範囲が継承されないことに注意することも重要です。つまり、 @Scope("prototype") アノテーションでアノテーションが付いたビンがあり、それを子ビンに注入すると、子ビンはプロトタイプになりません。

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

上記の例では、ChildBeanはプロトタイプではありません。これは、 @Scope("prototype") アノテーションが継承されないためです。

子Beanをプロトタイプにする必要がある場合は、@Scope（"prototype"）アノテーションでコメントを付けることができます。

```java
@Component
@Scope("prototype")
public class ParentBean {
   ...
}

@Component
@Scope("prototype")
public class ChildBean {
   @Autowired
   private ParentBean parentBean;

   ...
}
```

上記の例では、ChildBeanはプロトタイプになります。これは、 ChildBean クラスに @Scope("prototype") アノテーションが適用されるためです。

プロトタイプパターンは、アプリケーションのパフォーマンスを向上させるために使用できる強力なツールです。正しく使用すると、最初から新しいオブジェクトを作成するオーバーヘッドを回避できます。