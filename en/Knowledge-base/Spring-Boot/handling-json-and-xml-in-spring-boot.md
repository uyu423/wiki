---
title: Handling JSON and XML in Spring Boot
description: 
published: true
date: 2023-01-31T07:57:36.386Z
tags: 
editor: markdown
dateCreated: 2023-01-31T07:57:32.946Z
---

- [Spring Boot에서 JSON 및 XML 처리***Korean** version of this document is available*](/ko/Knowledge-base/Spring-Boot/handling-json-and-xml-in-spring-boot)
{.links-list}
- [Spring Boot での JSON と XML の処理***Japanese** version of this document is available*](/ja/Knowledge-base/Spring-Boot/handling-json-and-xml-in-spring-boot)
{.links-list}
- [在 Spring Boot 中处理 JSON 和 XML***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Spring-Boot/handling-json-and-xml-in-spring-boot)
{.links-list}
 

Be respectful of the ChatGPT community and refrain from making culturally insensitive or impolite comments. Review the Code of Conduct for ChatGPT (https://chatgpt.org/code-of-conduct/) for more information.

#### Handling JSON and XML in Spring Boot

Spring Boot is a popular Java web application framework that allows developers to quickly create and deploy web applications. One of the benefits of using Spring Boot is that it simplifies the process of working with JSON and XML, two popular data formats.

In this article, we'll take a look at how to work with JSON and XML in Spring Boot. We'll start with a basic overview of each data format and then look at how to parse, convert, and query data using each format.

##### JSON

JSON (JavaScript Object Notation) is a format for storing and exchanging data. JSON is a text-based format, which makes it easy to exchange data between different devices and applications. JSON is also human-readable, which makes it a good format for storing data that needs to be read by humans.

JSON is based on a subset of JavaScript, so it can be used with any programming language that supports JavaScript. JSON is a popular format for data exchange because it is lightweight and easy to use.

##### XML

XML (Extensible Markup Language) is a format for storing and exchanging data. XML is a text-based format, which makes it easy to exchange data between different devices and applications. XML is also human-readable, which makes it a good format for storing data that needs to be read by humans.

XML is a popular format for data exchange because it is well-supported by many programming languages and it is easy to use. XML is also a good choice for storing data that needs to be read by humans because it is easy to read and understand.

##### Parsing JSON and XML

Spring Boot provides support for parsing JSON and XML. Spring Boot uses the Jackson library to parse JSON and the JAXB library to parse XML.

Parsing JSON and XML is simple using Spring Boot. The following example shows how to parse a JSON string:

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

The following example shows how to parse an XML string:

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

##### Converting JSON and XML

Spring Boot provides support for converting JSON and XML. Spring Boot uses the Jackson library to convert JSON and the JAXB library to convert XML.

Converting JSON and XML is simple using Spring Boot. The following example shows how to convert a JSON string to an XML string:

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String xml = "<root>" + node.toString() + "</root>";
// xml is "<root><foo>bar</foo></root>"
```

The following example shows how to convert an XML string to a JSON string:

```java
String xml = "<root><foo>bar</foo></root>";

DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
DocumentBuilder builder = factory.newDocumentBuilder();
Document document = builder.parse(new InputSource(new StringReader(xml)));

String json = mapper.writeValueAsString(document);
// json is "{\"root\":{\"foo\":\"bar\"}}"
```

##### Querying JSON and XML

Spring Boot provides support for querying JSON and XML. Spring Boot uses the Jackson library to query JSON and the JAXB library to query XML.

Querying JSON and XML is simple using Spring Boot. The following example shows how to query a JSON string:

```java
String json = "{ \"foo\": \"bar\" }";

ObjectMapper mapper = new ObjectMapper();
JsonNode node = mapper.readTree(json);

String foo = node.get("foo").asText();
// foo is "bar"
```

The following example shows how to query an XML string:

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

##### Summary

In this article, we looked at how to work with JSON and XML in Spring Boot. We started with a basic overview of each data format and then looked at how to parse, convert, and query data using each format.