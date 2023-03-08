---
title: Spring Boot での JSON と XML の処理
description: 
published: true
date: 2023-01-31T07:57:34.541Z
tags: 
editor: markdown
dateCreated: 2023-01-31T07:57:32.954Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Handling JSON and XML in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/handling-json-and-xml-in-spring-boot)
{.links-list}
 

ChatGPTコミュニティを尊重し、文化的に無感覚または失礼なコメントを控えてください。詳細については、ChatGPT行動規範（https://chatgpt.org/code-of-conduct/）を参照してください。

# ### Spring BootでのJSONとXMLの処理

Spring Bootは、開発者がWebアプリケーションをすばやく作成してデプロイできるようにする人気のあるJava Webアプリケーションフレームワークです。 Spring Bootを使用する利点の1つは、広く使用されている2つのデータ型であるJSONとXMLで作業するプロセスを簡素化することです。

この記事では、Spring BootでJSONとXMLを扱う方法について説明します。各データ型の基本的な概要から始めて、各型を使用してデータを解析、変換、およびクエリする方法を見てみましょう。

# #### JSON

JSON（JavaScript Object Notation）は、データを保存および交換するための形式です。 JSONは、さまざまなデバイスとアプリケーション間でデータを簡単に交換できるテキストベースの形式です。 JSONは、人間が読むことができるため、人間が読む必要があるデータを保存するのに適した形式です。

JSONはJavaScriptのサブセットに基づいているため、JavaScriptをサポートするすべてのプログラミング言語で使用できます。 JSONは軽量で使いやすいため、データ交換に広く使用されている形式です。

# #### XML

XML（Extensible Markup Language）は、データを保存および交換するための形式です。 XMLは、さまざまなデバイスとアプリケーション間でデータを簡単に交換できるテキストベースの形式です。また、XMLは人間が読むことができるので、人間が読む必要があるデータを格納するのに適した形式です。

XML は多くのプログラミング言語でよくサポートされ、使いやすいため、データ交換に広く使用されている形式です。また、XMLは読みやすく理解しやすいため、人間が読む必要があるデータを保存するのにも適しています。

# #### JSONとXMLの解析

Spring BootはJSONとXMLの解析をサポートしています。 Spring BootはJacksonライブラリを使用してJSONを解析し、JAXBライブラリを使用してXMLを解析します。

JSONとXMLの解析はSpring Bootを使って簡単です。次の例は、JSON文字列を解析する方法を示しています。

```java
String json = "{\"foo\": \"bar\"}";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

次の例は、XML 文字列を解析する方法を示しています。

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance（）;
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

Element root = document.getDocumentElement();
Element foo = (Element) root.getElementsByTagName("foo").item(0);

String fooText = foo.getTextContent();
// fooText is "bar"
```

# #### JSONとXMLの変換

Spring BootはJSONとXMLの変換をサポートしています。 Spring BootはJacksonライブラリを使用してJSONを変換し、JAXBライブラリを使用してXMLを変換します。

Spring Bootを使用すると、JSONとXMLを簡単に変換できます。次の例は、JSON文字列をXML文字列に変換する方法を示しています。

```java
String json = "{\"foo\": \"bar\"}";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String xml = "<root>" + node.toString() + "</root>";
// xml is "<root><foo>bar</foo></root>"
```

次の例は、XML文字列をJSON文字列に変換する方法を示しています。

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance（）;
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

String json = mapper.writeValueAsString(document);
// json is "{\"root\":{\"foo\":\"bar\"}}"
```

# #### JSONおよびXMLクエリ

Spring BootはJSONおよびXMLクエリをサポートしています。 Spring BootはJSONを照会するためにJacksonライブラリを使用し、XMLを照会するためにJAXBライブラリを使用します。

JSONおよびXMLクエリはSpring Bootを使用して簡単です。次の例は、JSON文字列を照会する方法を示しています。

```java
String json = "{\"foo\": \"bar\"}";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

次の例は、XML 文字列を照会する方法を示しています。

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance（）;
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

Element root = document.getDocumentElement();
Element foo = (Element) root.getElementsByTagName("foo").item(0);

String fooText = foo.getTextContent();
// fooText is "bar"
```

# #### まとめ

この記事では、Spring BootでJSONとXMLを扱う方法について説明しました。各データ型の基本的な概要から始めて、各型を使用してデータを解析、変換、および照会する方法について説明しました。