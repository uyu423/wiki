---
title: Spring Test: Spring Boot のテスト フレームワーク
description: 
published: true
date: 2023-02-17T18:16:57.029Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:57:36.270Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Spring Test: Testing Framework for Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-test-testing-framework-for-spring-boot)
{.links-list}


#スプリングテスト：スプリングブート用のテストフレームワーク

この記事では、Spring Boot用のSpring Testテストフレームワークについて説明します。フレームワークの簡単な概要から始めて、使用方法のチュートリアルを提供します。次に、フレームワークの高度な機能について説明します。

## 概要

Spring TestはSpring Boot用のテストフレームワークです。 Spring Bootアプリケーションのテストを書くのに役立つように設計されています。 Spring Testは、Spring Bootアプリケーションのテストを書く便利な方法を提供します。また、アプリケーションのテストを簡単に書くためのいくつかの機能を提供します。

##チュートリアル

このチュートリアルでは、Spring Testを使用してSpring Bootアプリケーションのテストを作成する方法を説明します。数値の階乗を計算する単純なアプリケーションの例を使用します。

まず、プロジェクトに次の依存関係を追加する必要があります。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

次に、テストケースを作成する必要があります。 @Test アノテーションを使用してテストケースを表示します。

```java
@Test
public void testFactorial() {
    ...
}
```

テストケースでは、アプリケーションに必要な依存関係を注入する必要があります。 @Autowiredアノテーションを使用してこれを実行できます。

```java
@Autowired
private FactorialService service;
```

これでテストケースを作成できます。テストケースでは、FactorialService クラスの factorial() メソッドを呼び出します。私たちは結果が正しいと主張します。

```java
@Test
public void testFactorial() {
    int result = service.factorial(5);
    assertThat(result, is(120));
}
```

これで、次のコマンドを使用してテストケースを実行できます。

```
$mvn test
```

テストケースが合格すると、次の結果が表示されます。

```
Results:

Tests run: 1, Failures: 0, Errors: 0, Skipped: 0

[INFO]
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ spring-boot-test-example ---
[INFO]
[INFO] ----------------------------------------------- --------
[INFO] T E S T S
[INFO] ----------------------------------------------- --------
[INFO] Running com.example.test.ExampleTest
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.002 sec
[INFO]
[INFO] Results:
[INFO]
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
[INFO]
[INFO] ----------------------------------------------- -------------------------
[INFO]BUILD SUCCESS
[INFO] ----------------------------------------------- -------------------------
[INFO] Total time: 2.142 s
[INFO] Finished at: 2015-05-27T16:33:21+0530
[INFO] Final Memory: 10M/155M
[INFO] ----------------------------------------------- -------------------------
```

## アサーション

Spring Testは、テストケースで利用可能ないくつかのアサーションメソッドを提供します。これらのアサーションメソッドは org.springframework.test.util.AssertionErrors クラスで定義されます。

以下は、最も一般的に使用されるアサーション方法の一部です。

* assertTrue(条件)
* assertFalse(条件)
* assertEquals（予想、実際）
* assertNotEquals（予想、実際）
* assertNull(オブジェクト)
* assertNotNull(オブジェクト)

AssertionErrorsクラスのJavaDocでアサーションメソッドの完全なリストを見つけることができます。

## 例外処理

@Test（expected = Exception.class）アノテーションを使用して、テストケースで予想される例外を処理できます。

たとえば、入力が負の場合に factorial() メソッドが IllegalArgumentException を発生すると予想される場合は、次のテストケースを作成できます。

```java
@Test（expected = IllegalArgumentException.class）
public void testFactorialNegative() {
    service.factorial(-1);
}
```

##Java 8 Lambdaのサポート

Spring TestはJava 8ラムダ式をサポートしています。ラムダ式を使用すると、簡潔で読みやすいテストケースを作成できます。

たとえば、次のテストケースでは、数値リストがソートされていることを確認します。

```java
@Test
public void testSort() {
    List<Integer> numbers = Arrays.asList(5, 4, 3, 2, 1);
    Collections.sort(numbers);
    assertThat(numbers, is(Arrays.asList(1, 2, 3, 4, 5))));
}
```

## 仮定

Assume クラスを使用してアプリケーションの状態を想定できます。仮定が満たされない場合、テストをスキップするために仮定が使用されます。

たとえば、次のテストケースでは、数値が正数であることを確認します。数値が負の場合はテストケースをスキップします。

```java
@Test
public void testPositive() {
    int number = -1;
    Assume.assumeTrue(number > 0);
    assertThat(number, is(greaterThan(0)));
}
```

## テストコンテキスト

TestContextフレームワークは、テストケースで利用可能ないくつかの機能を提供します。これらの機能には以下が含まれます。

*テスト実行リスナー
*テストサポート
*テストイベントの公開
*テストインスタンスの後処理
*テストクラスへの依存性注入

これらの機能を使用して、アプリケーションの洗練されたテストケースを作成できます。

##結論

この記事では、Spring Boot用のSpring Testテストフレームワークについて説明しました。フレームワークを使用してアプリケーションのテストを作成する方法を見てきました。また、フレームワークの高度な機能の一部を見ました。