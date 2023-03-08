---
title: Kotlin と XML: XML データの解析と生成
description: 
published: true
date: 2023-02-17T18:07:40.554Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:05:37.909Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and XML: Parsing and Generating XML Data***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-xml-parsing-and-generating-xml-data)
{.links-list}


# KotlinとXML：XMLデータの解析と生成

Kotlin は Java Virtual Machine で動作する最新のプログラミング言語です。 Kotlinは、オブジェクト指向と機能プログラミングパラダイムの両方の利点を組み合わせた簡潔で安全で相互運用可能な言語として知られています。

XMLは、データの保存と転送に一般的に使用されるマークアップ言語です。 XML は、人間と機械の両方が読み取れるため、データ交換に広く使用されている形式です。

この記事では、KotlinでXMLデータを解析して生成する方法について説明します。最も一般的に使用されているKotlin用のXMLライブラリについて学び、使用方法のいくつかの例を見てみましょう。

## Kotlin用のXMLライブラリ

Kotlinで利用可能な多くのXMLライブラリがあります。このセクションでは、最も人気のあるいくつかを見てみましょう。

### JUnit 5

JUnit 5は、広く使用されているJava用のテストフレームワークです。また、Kotlinをよくサポートしています。 JUnit 5には、XMLデータのテストに使用できる組み込みのコメントセットが付属しています。これらのコメントは次のとおりです。

* @試験
* @名前を表示する
* @タグ
* @障害がある

XMLデータテストにJUnit 5を使用するには、build.gradleファイルに次の依存関係を追加する必要があります。

「groovy
repositories {
    jcenter()
}

dependencies {
    ...
    testImplementation("org.junit.jupiter:junit-jupiter-api:5.3.1")
    testRuntimeOnly("org.junit.jupiter:junit-jupiter-engine:5.3.1")
    ...
}
```

その後、次の簡単なテストを作成できます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // TODO: write test
}
```

上記のテストでは、@Test、@DisplayName、@Tag、および@Disabledアノテーションを使用しています。 @Testアノテーションは、メソッドをテストメソッドとして表示するために使用されます。 @DisplayName アノテーションは、テストのカスタム名を指定するために使用されます。 @Tag アノテーションはテストのタグ付けに使用されます。 @Disabled アノテーションはテストを無効にするために使用されます。

その後、テストメソッドにXML解析コードを書くことができます。たとえば、次のコードを使用してXMLデータを解析できます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XMLデータ
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // TODO: write assertions
}
```

上記のコードでは、DocumentBuilderFactoryクラスを使用して新しいXMLドキュメントビルダーを作成します。次に、parse（）メソッドを使用してXML文字列を解析します。

その後、申し立てを作成できます。たとえば、次のコードを使用して、XML文書に「element1」という名前の要素があることをアサートできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XMLデータ
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // Assert that the XML document has an element with the name "element1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    assertNotNull(element1)
}
```

上記のコードでは、 getElementsByTagName() メソッドを使用して、名前が "element1" の要素を取得します。次に、assertNotNull（）メソッドを使用して、要素がnullでないことを確認します。

また、次のコードを使用して、要素の値が「value1」であることをアサートすることもできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XMLデータ
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // Assert that the element has the value "value1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    val value1 = element1.textContent
    assertEquals("value1", value1)
}
```

上記のコードでは、textContentプロパティを使用して要素の値を取得します。次に assertEquals() メソッドを使用して、値が "value1" と等しいと主張します。

次のコードを使用してXMLデータを生成することもできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Generate XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument()
    val root = xmlDoc.createElement("root")
    val element1 = xmlDoc.createElement("element1")
    element1.textContent = "value1"
    root.appendChild(element1)
    xmlDoc.appendChild(root)

    // TODO: write assertions
}
```

上記のコードでは、createElement（）メソッドを使用して新しい要素を作成します。次に、 textContent プロパティを使用して要素の値を設定します。次に、appendChild（）メソッドを使用して要素をドキュメントに追加します。

その後、申し立てを作成できます。たとえば、次のコードを使用して、XML文書に「element1」という名前の要素があることをアサートできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Generate XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument()
    val root = xmlDoc.createElement("root")
    val element1 = xmlDoc.createElement("element1")
    element1.textContent = "value1"
    root.appendChild(element1)
    xmlDoc.appendChild(root)

    // Assert that the XML document has an element with the name "element1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    assertNotNull(element1)
}
```

上記のコードでは、 getElementsByTagName() メソッドを使用して、名前が "element1" の要素を取得します。次に、assertNotNull（）メソッドを使用して、要素がnullでないことを確認します。

また、次のコードを使用して、要素の値が「value1」であることをアサートすることもできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Generate XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument()
    val root = xmlDoc.createElement("root")
    val element1 = xmlDoc.createElement("element1")
    element1.textContent = "value1"
    root.appendChild(element1)
    xmlDoc.appendChild(root)

    // Assert that the element has the value "value1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    val value1 = element1.textContent
    assertEquals("value1", value1)
}
```

上記のコードでは、textContentプロパティを使用して要素の値を取得します。次に assertEquals() メソッドを使用して、値が "value1" と等しいと主張します。

次のコードを使用してXMLデータを生成することもできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Generate XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument()
    val root = xmlDoc.createElement("root")
    val element1 = xmlDoc.createElement("element1")
    element1.textContent = "value1"
    root.appendChild(element1)
    xmlDoc.appendChild(root)

    // Assert that the XML document has an element with the name "element1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    assertNotNull(element1)
}
```

上記のコードでは、 getElementsByTagName() メソッドを使用して、名前が "element1" の要素を取得します。次に、assertNotNull（）メソッドを使用して、要素がnullでないことを確認します。

また、次のコードを使用して、要素の値が「value1」であることをアサートすることもできます。

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Generate XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument()
    val root = xmlDoc.createElement("root")
    val element1 = xmlDoc.createElement("element1")
    element1.textContent = "value1"
    root.appendChild(element1)
    xmlDoc.appendChild(root)

    // Assert that the element has the value "value1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    val value1 = element1.textContent
    assertEquals("value1", value1)
}
```

上記のコードでは、textContentプロパティを使用して要素の値を取得します。次に assertEquals() メソッドを使用して、値が "value1" と等しいと主張します。