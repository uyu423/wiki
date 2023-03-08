---
title: Spring Boot での依存性注入
description: 
published: true
date: 2023-01-31T14:57:25.325Z
tags: 
editor: markdown
dateCreated: 2023-01-31T14:57:23.770Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Dependency Injection in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/dependency-injection-in-spring-boot)
{.links-list}


#スプリングブートからの依存性注入

##はじめに

依存性注入（DI）は、アプリケーションのモジュール性を高めるために最新のプログラミングで広く使用されている技術です。オブジェクトに依存関係を注入することで、これらの依存関係をハードコーディングせずにコードを柔軟かつテストおよび保守しやすくすることができます。

この記事では、Spring FrameworkのコンテキストでDIがどのように機能するか、およびSpringベースのアプリケーションをよりモジュール化してテストしやすくする方法について説明します。

##依存性注入とは？

依存性注入は、オブジェクト自体からオブジェクトの依存関係を分離する技術です。

従来のプログラミングでは、オブジェクトは依存関係をハードコーディングします。つまり、これらの依存関係が変更された場合は、オブジェクトも変更する必要があります。この緊密な組み合わせにより、コードを維持しテストすることは困難です。

DIを使用すると、オブジェクトの依存関係はハードコーディングされず、実行時にオブジェクトに注入されます。これにより、依存関係を使用するオブジェクトを変更せずに依存関係を変更できます。

## SpringでDIはどのように機能しますか？

Springでは、DIは@Autowiredアノテーションを使用して行われます。このコメントは、フィールド、セッターメソッド、コンストラクタで使用できます。フィールドで使用される場合、フィールドは実行時に依存関係とともに注入されます。 setter メソッドで使用する場合、メソッドが呼び出されると、依存関係がメソッドに注入されます。コンストラクタで使用すると、オブジェクトが作成されると、依存関係がオブジェクトに注入されます。

@Autowiredアノテーションは@Configurationアノテーションを持つメソッドでも使用できます。この場合、メソッドが呼び出されるとメソッドに依存関係が注入されます。

## Spring BootでDIを使用する方法

Spring Bootを使用すると、アプリケーションでDIを簡単に使用できます。 Spring BootでDIを使用するには、依存関係を注入するフィールド、setterメソッド、またはコンストラクタに@Autowiredアノテーションを追加するだけです。

たとえば、依存関係を注入する単純なサービスがあるとします。 @Autowiredでフィールドにコメントを付けることでこれを行うことができます。

```java
@Service
public class MyService {
    @Autowired
    private MyDependency myDependency;
}
```

あるいは、セッターメソッドに注釈を付けることもできます。

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

あるいは、コンストラクタに注釈を付けることもできます。

```java
@Service
public class MyService {
    private MyDependency myDependency;
    
    @Autowired
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
}
```

##結論

依存性注入は、アプリケーションのモジュール性を向上させるために使用できる強力な技術です。 Springでは、DIは@Autowiredアノテーションを使用して行われます。

Spring Bootを使用すると、アプリケーションでDIを簡単に使用できます。 Spring BootでDIを使用するには、依存関係を注入するフィールド、setterメソッド、またはコンストラクタに@Autowiredアノテーションを追加するだけです。