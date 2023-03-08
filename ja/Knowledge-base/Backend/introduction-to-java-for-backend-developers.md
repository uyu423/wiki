---
title: バックエンド開発者のための Java 入門
description: 
published: true
date: 2023-02-17T18:13:02.734Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:58:04.151Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Introduction to Java for Backend Developers***English** version of this document is available*](/en/Knowledge-base/Backend/introduction-to-java-for-backend-developers)
{.links-list}


#バックエンド開発者向けのJavaの紹介

Javaは、バックエンド開発者が強力でスケーラブルなソフトウェアを作成できるようにする多目的言語です。この記事では、バックエンド開発者のためのJava開発の概要について説明します。次のトピックを取り上げます。

- 開発環境設定
- こんにちは、世界！
- 基本構文
- クラスとオブジェクト
- 方法
- 例外処理
- JDBC

##開発環境設定

Javaで開発を開始する前に、開発環境を設定する必要があります。以下が必要です。

- テキストエディタまたはIDE。
- Java開発キット（JDK）。

Eclipse、IntelliJ IDEA、NetBeansなどの多くのテキストエディタとIDEがあります。この記事ではEclipse IDEを使用します。

[Oracle Webサイト]（https://www.oracle.com/java/）からJDKをダウンロードできます。 JREではなくJDKをダウンロードする必要があります。

JDKをダウンロードしたら、JDKの場所を指すように環境変数JAVA_HOMEを設定する必要があります。

## こんにちは、世界！

これで開発環境が設定されたので、最初のJavaプログラムを書いてみましょう。

`HelloWorld.java`という新しいファイルを作成し、次のコードを追加します。

```java
public class HelloWorld {
 
    public static void main(String[] args) {
       System.out.println("Hello, world!");
    }
 
}
```

これでプログラムをコンパイルして実行できます。プログラムをコンパイルするには、コマンドプロンプトまたはターミナルを開き、 `HelloWorld.java`があるディレクトリに移動します。次に、次のコマンドを実行します。

```
javac HelloWorld.java
```

これにより、プログラムのバイトコードを含む「HelloWorld.class」というファイルが生成されます。これで、次のコマンドを入力してプログラムを実行できます。

```
java HelloWorld
```

「Hello、world！」出力を表示する必要があります。

## 基本構文

Javaでは、すべてのプログラムには `main()` メソッドが必要です。 `main()` メソッドはプログラムの実行が始まるところです。

すべてのJavaプログラムはクラスで構成されています。クラスはオブジェクトを作成するためのテンプレートです。オブジェクトはクラスのインスタンスです。 `HelloWorld`の例には、`HelloWorld`クラスとそのクラスのオブジェクトがあります。

Javaは大文字と小文字を区別する言語なので、文字の大文字と小文字が重要です。たとえば、 `HelloWorld`クラスは `helloworld`クラスと同じではありません。

Javaは静的に型指定された言語なので、各変数の型を明示的に宣言する必要があります。たとえば、次のコードはコンパイルされません。

```java
String message;
message="Hello, world!";
```

`message`が`String`であることを明示的に宣言する必要があります。

```java
String message;
message="Hello, world!";
```

## クラスとオブジェクト

前述のように、クラスはオブジェクトを作成するためのテンプレートです。 Javaでは、クラスは単にオブジェクトの青写真であり、オブジェクトはクラスのインスタンスです。

クラスは次の2つで構成されています。

- オブジェクトに含めるデータ（変数）。
- オブジェクトが実行できる動作（メソッド）です。

一例を見てみましょう。

```java
public class Car {
   
   // The data
   private String make;
   private String model;
   private int year;
   
   // The behavior
   public void start() {
      // Start the car
   }
   
   public void stop() {
      // Stop the car
   }
   
   public void drive() {
      // Drive the car
   }
   
}
```

この例では、3つのデータ（ `make`、 `model`、 `year`）と3つのメソッド（ `start（）`、`stop（）`、およびdrive（）`）です。これら3つのメソッドは `Car`オブジェクトの動作を定義します。

クラスのオブジェクトを生成するには `new` キーワードを使用します。

```java
Car myCar = new Car();
```

オブジェクトを作成したら、ドット表記を使用してオブジェクトのデータとメソッドにアクセスできます。

```java
myCar.make = "Honda";
myCar.model = "Civic";
myCar.year = 2006;

myCar.start();
myCar.drive();
myCar.stop();
```

上記の例では、 `myCar`オブジェクトのデータフィールドを設定してからメソッドを呼び出します。

##メソッド

前のセクションで示したように、メソッドはオブジェクトが実行できる動作です。メソッドには次のコンポーネントがあります。

- 可視性修飾子（「public」、「private」など）
- 戻り値の型（ `void`、 `int`、 `String`など）
- メソッド名
- メソッドパラメータ（括弧で囲む）
- メソッド本文（中括弧で囲む）

例を見てみましょう。

```java
public void drive() {
   // Drive the car
}
```

この例では、メソッドは `public`なので、他のクラスで見ることができます。戻り値の型は `void` であり、メソッドが値を返さないことを意味します。メソッド名は `drive()` です。メソッドはパラメータを使用しないため、括弧は空です。メソッド本文は中かっこで囲みます。

パラメータを使用するメソッドを作成することもできます。

```java
public void drive(int distance) {
   // Drive the car for the specified distance
}
```

そして、値を返すメソッドを作成できます。

```java
public int getDistance() {
   // Calculate and return the distance driven
}
```

## 例外処理

例外処理は、プログラムの実行中に発生するエラーを処理するためのメカニズムです。 Javaでは、エラーは「例外」というオブジェクトで表されます。 2 種類の例外があります。

- 確認された例外：コンパイラが確認する例外です。確認された例外は処理または宣言する必要があります。
- 未確認の例外：コンパイラによって確認されていない例外。未確認の例外は処理または宣言する必要はありません。

確認された例外の例を見てみましょう。

```java
try{
   // This code may throw an exception
} catch(Exception e) {
   // Handle the exception
} finally {
   // This code will always be executed
}
```

上記の例には、例外を発生させる可能性のあるコードを含む `try` ブロックがあります。例外が発生したときに実行される `catch` ブロックがあります。そして、例外が発生したかどうかに関係なく実行される `finally` ブロックがあります。

## JDBC

JDBC（Java Database Connectivity）は、Javaプログラムがデータベースと対話できるようにするJava APIです。 JDBCは、データベースの実装に関係なく、データベースにアクセスするための標準APIを提供します。

JDBCを使用するには、プログラムに `java.sql`パッケージを含める必要があります。

```java
import java.sql.*;
```

`java.sql`パッケージをインポートすると、`DriverManager`クラスを使用してデータベースに接続できます。

```java
Connection conn=DriverManager
   .getConnection("jdbc:mysql://localhost:3306/testdb", "root", "password");
```

上記の例では、ユーザー名 'root'とパスワード 'password'を使用してURL 'jdbc:mysql://localhost:3306/testdb'でMySQLデータベースに接続しています。

データベースに接続したら、 `Statement`と `PreparedStatement`インタフェースを使用してSQL文を実行できます。

`Statement` インタフェースは、パラメータを使用しない SQL 文を実行するために使用できます。

```java
Statement stmt = conn.createStatement();
stmt.executeUpdate("INSERT INTO table1 (column1, column2) VALUES('value1', 'value2')");
```

`PreparedStatement`インタフェースは、パラメータを使用するSQL文を実行するために使用できます。

```java
PreparedStatement pstmt = conn.prepareStatement("INSERT INTO table1 (column1, column2) VALUES(?, ?)");
pstmt.setString(1, "value1");
pstmt.setString(2, "value2");
pstmt.executeUpdate();
```

最後に完了したら、接続を閉じる必要があります。

```java
conn.close();
```

##結論

この記事では、バックエンド開発者のためのJava開発の概要を提供しました。私たちは次のトピックを扱いました。

- 開発環境設定
- こんにちは、世界！
- 基本構文
- クラスとオブジェクト
- 方法
- 例外処理
- JDBC