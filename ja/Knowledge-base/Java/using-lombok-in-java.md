---
title: Java でロンボクを使用する
description: 
published: true
date: 2023-01-31T09:05:37.411Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:05:35.710Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Using Lombok in Java***English** version of this document is available*](/en/Knowledge-base/Java/using-lombok-in-java)
{.links-list}




# Javaでロンボクを使う

Lombokは、Javaで定型句コードを減らすために使用できるライブラリです。 getter、setter、toString、hashCode、および equals メソッドとコンストラクタを自動的に生成するために使用されます。 Lombokはオープンソースであり、MITライセンスの下で利用可能です。

## インストール

LombokはIDEにプラグインとしてインストールするか、プロジェクトのビルドパスに追加できます。

# # # IDEプラグイン

## # # Eclipse

Eclipseに使用できるLombokプラグインがあります。インストールするには、Eclipseを起動し、ヘルプ> Eclipse Marketplaceに移動します。 Lombokを検索してプラグインをインストールします。

## # # IntelliJ IDEA

IntelliJ IDEAに使用できるLombokプラグインがあります。インストールするには、IntelliJ IDEAを起動して[ファイル]> [設定]に移動します。設定ウィンドウでプラグインに移動し、[リポジトリの参照]をクリックします。 Lombokを検索してプラグインをインストールします。

# # # ビルドパス

MavenでビルドするプロジェクトでLombokを使用している場合は、pom.xmlファイルに次の依存関係を追加して、プロジェクトのビルドパスにLombokを追加できます。

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version> 1.16.20 </version>
    <scope>provided</scope>
</dependency>
```

GradleでビルドするプロジェクトでLombokを使用している場合は、build.gradleファイルに次の依存関係を追加して、プロジェクトのビルドパスにLombokを追加できます。

「groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.16.20'
}
```

## 用法

JavaコードでLombokを使用するには、getter、setter、およびコンストラクタを生成するフィールドにコメントを付ける必要があります。たとえば、

```java
import lombok.Data;

@Data
public class Person {
    private String name;
    private int age;
}
```

@Dataアノテーションは、Personクラスのすべてのフィールドに対してgetter、setter、およびコンストラクタを生成します。

フィールドのゲッターとセッターのみを作成したい場合は、@Getterと@Setterアノテーションを使用できます。

```java
import lombok.Getter;
import lombok.Setter;

public class Person {
    @Getter
    @Setter
    private String name;

    private int age;
}
```

クラスのコンストラクタのみを作成したい場合は、@RequiredArgsConstructorアノテーションを使用できます。

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Person {
    private final String name;
    private final int age;
}
```

@RequiredArgsConstructorアノテーションは、最終的にマークされるか、@NonNullアノテーションを持つすべてのフィールドのパラメータを持つコンストラクタを生成します。

クラスの toString メソッドを生成するには、 @ToString アノテーションを使用できます。

```java
import lombok.ToString;

@ToString
public class Person {
    private String name;
    private int age;
}
```

クラスのhashCodeメソッドを生成するには、@HashCodeアノテーションを使用できます。

```java
import lombok.HashCode;

@HashCode
public class Person {
    private String name;
    private int age;
}
```

クラスのequalsメソッドを生成するには、@EqualsAndHashCodeアノテーションを使用できます。

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Person {
    private String name;
    private int age;
}
```

##メリットとデメリット

Lombokは、Javaで定型句コードを減らすのに役立つ非常に便利なツールです。しかし、Lombokの使用にはいくつかの潜在的な欠点があります。

まず、Lombokはソースコードに見えないコードを生成します。これにより、生成されたコードで発生する問題をデバッグするのが困難になる可能性があります。

第二に、Lombokはコードを読みにくくすることができます。たとえば、@Dataアノテーションは、ソースコードを理解するのがより困難になる可能性がある多くのコードを生成します。

第三に、Lombokはコードチェックツールなどの特定のJavaツールを使用するのが難しくなります。これは、Lombok生成コードがソースコードに表示されないためです。

第四に、Lombokはコードを新しいバージョンのJavaに移行するのが難しくなります。これは、Lombok生成コードがコンパイルされたJavaのバージョンによって異なるためです。

最後に、Lombokは広く使用されていません。これは、Lombokで利用可能な文書やサポートが少ないことを意味します。

## 結論

Lombokは、Javaで定型句コードを減らすために使用できるライブラリです。 getter、setter、toString、hashCode、および equals メソッドとコンストラクタを自動的に生成するために使用されます。 Lombokはオープンソースであり、MITライセンスの下で利用可能です。

Lombokは、Javaで定型句コードを減らすのに役立つ非常に便利なツールです。しかし、Lombokの使用にはいくつかの潜在的な欠点があります。まず、Lombokはソースコードに見えないコードを生成します。これにより、生成されたコードで発生する問題をデバッグするのが困難になる可能性があります。第二に、Lombokはコードを読みにくくすることができます。たとえば、@Dataアノテーションは、ソースコードを理解するのがより困難になる可能性がある多くのコードを生成します。第三に、Lombokはコードチェックツールなどの特定のJavaツールを使用するのが難しくなります。これは、Lombok生成コードがソースコードに表示されないためです。第四に、Lombokはコードを新しいバージョンのJavaに移行するのが難しくなります。これは、Lombok生成コードがコンパイルされたJavaのバージョンによって異なるためです。最後に、Lombokは広く使用されていません。これは、Lombokで利用可能な文書やサポートが少ないことを意味します。