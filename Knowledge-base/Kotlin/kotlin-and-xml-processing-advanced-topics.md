---
title: Kotlin 및 XML 처리: 고급 주제
description: 
published: true
date: 2023-02-17T18:03:37.779Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:32:52.611Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and XML Processing: Advanced Topics***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-xml-processing-advanced-topics)
{.links-list}


# Kotlin 및 XML 처리: 고급 주제

이 기사에서는 Kotlin 및 XML 처리와 관련된 몇 가지 고급 주제를 살펴보겠습니다. Kotlin의 기본 제공 XML 처리 기능을 사용하여 XML 유효성 검사, XML 변환 및 XML 쿼리와 같은 일반적인 작업을 수행하는 방법을 알아봅니다.

## XML 유효성 검사

XML이 올바른 형식이고 필요할 수 있는 모든 스키마를 준수하는지 확인하기 위해 XML을 처리하기 전에 유효성을 검사하는 것이 중요합니다. Kotlin은 XML을 검증하는 다양한 방법을 제공합니다.

먼저 [`javax.xml.validation`](https://docs.oracle.com/javASE/8/docs/api/javax/xml/validation/package-summary.html) API를 사용하여 XML을 검증할 수 있습니다. [XML 스키마](https://www.w3.org/XML/Schema):

```kotlin
import javax.xml.XMLConstants
import javax.xml.validation.SchemaFactory

// Create a SchemaFactory capable of understand WXS schemas
val factory = SchemaFactory.newInstance(XMLConstants.W3C_XML_SCHEMA_NS_URI)

// Load the specified schema
val schema = factory.newSchema(File("schema.xsd"))

// Create a Validator instance, which can be used to validate XML files
val validator = schema.newValidator()

// Validate the XML file
validator.validate(File("file.xml"))
```

또는 [`kotlinx.xml.validation`](https://github.com/Kotlin/kotlinx.xml/tree/master/validation) 라이브러리를 사용하여 [XML 스키마](https:/ /www.w3.org/XML/스키마):

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

## XML 변환

대부분의 경우 XML을 한 형식에서 다른 형식으로 변환해야 합니다. Kotlin은 XML을 변환하는 다양한 방법을 제공합니다.

먼저 [`javax.xml.transform`](https://docs.oracle.com/javase/8/docs/api/javax/xml/transform/package-summary.html) API를 사용하여 XML을 변환할 수 있습니다. :

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

또는 [`kotlinx.xml.transform`](https://github.com/Kotlin/kotlinx.xml/tree/master/transform) 라이브러리를 사용하여 XML을 변환할 수 있습니다.

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

## XML 쿼리

대부분의 경우 특정 정보를 추출하기 위해 XML을 쿼리해야 합니다. Kotlin은 XML을 쿼리하는 다양한 방법을 제공합니다.

먼저 [`javax.xml.xpath`](https://docs.oracle.com/javase/8/docs/api/javax/xml/xpath/package-summary.html) API를 사용하여 XML을 쿼리할 수 있습니다. :

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

또는 [`kotlinx.xml.xpath`](https://github.com/Kotlin/kotlinx.xml/tree/master/xpath) 라이브러리를 사용하여 XML을 쿼리할 수 있습니다.

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

## 결론

이 기사에서는 Kotlin 및 XML 처리와 관련된 몇 가지 고급 주제를 살펴보았습니다. Kotlin의 기본 제공 XML 처리 기능을 사용하여 XML 유효성 검사, XML 변환 및 XML 쿼리와 같은 일반적인 작업을 수행하는 방법을 배웠습니다.