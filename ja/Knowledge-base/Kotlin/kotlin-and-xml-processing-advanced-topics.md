---
title: Kotlin と XML 処理: 高度なトピック
description: 
published: true
date: 2023-02-17T18:03:35.791Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:32:52.611Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and XML Processing: Advanced Topics***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-xml-processing-advanced-topics)
{.links-list}


# KotlinとXML処理：高度なトピック

この記事では、KotlinとXMLの処理に関するいくつかの高度なトピックについて説明します。 Kotlinの組み込みXML処理機能を使用して、XML検証、XML変換、XMLクエリなどの一般的なタスクを実行する方法を学びます。

## XML検証

XMLが正しい形式であり、必要なすべてのスキーマに準拠していることを確認するには、XMLを処理する前に検証することが重要です。 KotlinはXMLを検証するさまざまな方法を提供しています。

まず、[`javax.xml.validation`]（https://docs.oracle.com/javASE/8/docs/api/javax/xml/validation/package-summary.html）APIを使用してXMLを検証できますあります。 [XML スキーマ] (https://www.w3.org/XML/Schema):

```kotlin
import javax.xml.XMLConstants
import javax.xml.validation.SchemaFactory

// Create a SchemaFactory capable of understand WXS スキーマ
val factory = SchemaFactory.newInstance(XMLConstants.W3C_XML_SCHEMA_NS_URI)

// Load the specified schema
val schema = factory.newSchema(File("schema.xsd"))

// Create a Validator instance, which can be used to validate XML files
val validator = schema.newValidator()

// Validate the XML file
validator.validate(File("file.xml"))
```

または [`kotlinx.xml.validation`] (https://github.com/Kotlin/kotlinx.xml/tree/master/validation) ライブラリを使用した [XML スキーマ] (https://www.w3.org/ XML/スキーマ):

```kotlin
import kotlinx.xml.validation.Schema
import kotlinx.xml.validation.XmlValidator

// Load the specified schema
val schema = Schema.fromResource("schema.xsd")

// Create a validator
val validator = XmlValidator(schema)

// Validate the XML file
validator.validate(File("file.xml"))
```

## XML変換

ほとんどの場合、XMLをある形式から別の形式に変換する必要があります。 KotlinはXMLを変換するさまざまな方法を提供しています。

まず、[`javax.xml.transform`]（https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/package-summary.html）APIを使用してXMLを変換できますあります。 :

```kotlin
import javax.xml.transform.*
import javax.xml.transform.stream.StreamResult

// Create a TransformerFactory
val factory = TransformerFactory.newInstance()

// Use the factory to create a Transformer that will perform the transformation
val transformer = factory.newTransformer()

// Set the transformation parameters
transformer.setOutputProperty(OutputKeys.INDENT, "yes")
transformer.setOutputProperty("{http://xml.apache.org/xslt}indent-amount", "2")

// Transform the XML
transformer.transform(
    StreamSource(File("input.xml")),
    StreamResult(File("output.xml"))
)
```

あるいは、[`kotlinx.xml.transform`]（https://github.com/Kotlin/kotlinx.xml/tree/master/transform）ライブラリを使用してXMLを変換することもできます。

```kotlin
import kotlinx.xml.transform.*

// Transform the XML
transformXml("input.xml") {
    declareDefaultNamespace("http://example.com/ns")
    indent(2)
    forEachElement("//*") {
        println(it.name)
    }
}.write("output.xml")
```

## XMLクエリ

ほとんどの場合、特定の情報を抽出するためにXMLを照会する必要があります。 KotlinはXMLを照会するさまざまな方法を提供します。

まず、[ `javax.xml.xpath`]（https://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/package-summary.html）APIを使用してXMLをクエリできますあります。 :

```kotlin
import javax.xml.xpath.*

// Create an XPathFactory
val factory = XPathFactory.newInstance()

// Use the XPathFactory to create an XPath object
val xpath = factory.newXpath()

// Compile an XPath expression
val expr = xpath.compile("//*[local-name()='root' and namespace-uri()='http://example.com/ns']")

// Evaluate the XPath expression in the context of the specified XML file
val node = expr.evaluate(File("file.xml"), XPathConstants.NODE)

// Print the result
println(node)
```

あるいは、[`kotlinx.xml.xpath`]（https://github.com/Kotlin/kotlinx.xml/tree/master/xpath）ライブラリを使用してXMLを照会することもできます。

```kotlin
import kotlinx.xml.xpath.*

// Load the XML file
val xml = File("file.xml").readText()

// Parse the XML
val document = xml.parseXml()

// Evaluate the XPath expression
val node = document.evaluate("//*[local-name()='root' and namespace-uri()='http://example.com/ns']")

// Print the result
println(node)
```

##結論

この記事では、KotlinとXMLの処理に関するいくつかの高度なトピックについて説明しました。 Kotlinの組み込みXML処理機能を使用して、XML検証、XML変換、XMLクエリなどの一般的なタスクを実行する方法を学びました。