---
title: 在 Spring Boot 中处理 JSON 和 XML
description: 
published: true
date: 2023-01-31T07:57:34.550Z
tags: 
editor: markdown
dateCreated: 2023-01-31T07:57:32.955Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Handling JSON and XML in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/handling-json-and-xml-in-spring-boot)
{.links-list}
 

尊重 ChatGPT 社区，不要发表文化上不敏感或不礼貌的评论。查看 ChatGPT 行为准则 (https://chatgpt.org/code-of-conduct/) 了解更多信息。

# ### 在 Spring Boot 中处理 JSON 和 XML

Spring Boot 是一种流行的 Java Web 应用程序框架，允许开发人员快速创建和部署 Web 应用程序。使用 Spring Boot 的好处之一是它简化了使用 JSON 和 XML 这两种流行数据格式的过程。

在本文中，我们将了解如何在 Spring Boot 中使用 JSON 和 XML。我们将从每种数据格式的基本概述开始，然后研究如何使用每种格式解析、转换和查询数据。

# #### JSON

JSON（JavaScript 对象表示法）是一种用于存储和交换数据的格式。 JSON 是一种基于文本的格式，可以轻松地在不同设备和应用程序之间交换数据。 JSON 也是人类可读的，这使其成为存储需要人类阅读的数据的良好格式。

JSON 基于 JavaScript 的一个子集，因此它可以与任何支持 JavaScript 的编程语言一起使用。 JSON 是一种流行的数据交换格式，因为它轻巧且易于使用。

# #### XML

XML（可扩展标记语言）是一种用于存储和交换数据的格式。 XML 是一种基于文本的格式，可以方便地在不同设备和应用程序之间交换数据。 XML 也是人类可读的，这使其成为存储需要人类阅读的数据的良好格式。

XML 是一种流行的数据交换格式，因为它得到许多编程语言的良好支持并且易于使用。 XML 也是存储需要人类阅读的数据的不错选择，因为它易于阅读和理解。

# #### 解析 JSON 和 XML

Spring Boot 提供了对解析 JSON 和 XML 的支持。 Spring Boot 使用 Jackson 库解析 JSON，使用 JAXB 库解析 XML。

使用 Spring Boot 解析 JSON 和 XML 很简单。以下示例显示了如何解析 JSON 字符串：

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

以下示例显示了如何解析 XML 字符串：

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

Element root = document.getDocumentElement();
Element foo = (Element) root.getElementsByTagName("foo").item(0);

String fooText = foo.getTextContent();
// fooText is "bar"
```

# #### 转换 JSON 和 XML

Spring Boot 提供对转换 JSON 和 XML 的支持。 Spring Boot 使用 Jackson 库转换 JSON，使用 JAXB 库转换 XML。

使用 Spring Boot 转换 JSON 和 XML 很简单。以下示例显示如何将 JSON 字符串转换为 XML 字符串：

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String xml = "<root>" + node.toString() + "</root>";
// xml is "<root><foo>bar</foo></root>"
```

以下示例显示如何将 XML 字符串转换为 JSON 字符串：

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

String json = mapper.writeValueAsString(document);
// json is "{\"root\":{\"foo\":\"bar\"}}"
```

# #### 查询 JSON 和 XML

Spring Boot 提供了对查询 JSON 和 XML 的支持。 Spring Boot 使用 Jackson 库查询 JSON，使用 JAXB 库查询 XML。

使用 Spring Boot 查询 JSON 和 XML 很简单。以下示例显示了如何查询 JSON 字符串：

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

以下示例显示如何查询 XML 字符串：

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

Element root = document.getDocumentElement();
Element foo = (Element) root.getElementsByTagName("foo").item(0);

String fooText = foo.getTextContent();
// fooText is "bar"
```

##### 概括

在本文中，我们了解了如何在 Spring Boot 中使用 JSON 和 XML。我们首先对每种数据格式进行了基本概述，然后研究了如何使用每种格式解析、转换和查询数据。