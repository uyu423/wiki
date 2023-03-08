---
title: Kotlin 및 XML: 데이터 파싱 및 직렬화
description: 
published: true
date: 2023-02-18T01:32:16.610Z
tags: 
editor: markdown
dateCreated: 2023-02-18T01:32:15.272Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and XML: Parsing and Serializing Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-xml-parsing-and-serializing-data)
{.links-list}


# Kotlin 및 XML: 데이터 파싱 및 직렬화

Kotlin은 유형 유추 기능이 있는 정적 유형의 범용 프로그래밍 언어입니다. 구문이 깨끗하고 이해하기 쉽습니다. Kotlin은 기존 Java 코드와 상호 운용이 가능하므로 Android 애플리케이션을 개발하는 데 사용할 수 있습니다.

 XML은 데이터를 저장하는 데 사용되는 마크업 언어입니다. 사람이 읽을 수 있고 기계가 읽을 수 있습니다. XML은 플랫폼 독립적이고 다른 형식으로 쉽게 변환될 수 있기 때문에 데이터 저장에 널리 사용됩니다.

Kotlin과 XML을 함께 사용하여 데이터를 구문 분석하고 직렬화할 수 있습니다. 이 기사에서는 Kotlin을 사용하여 XML 데이터를 구문 분석하고 직렬화하는 방법을 배웁니다.

## Kotlin으로 XML 구문 분석

Kotlin으로 XML을 파싱하는 것은 간단하고 쉽습니다. Kotlin에는 XML 데이터를 쉽게 파싱할 수 있는 XML 처리용 내장 라이브러리가 있습니다.

먼저 XML 처리 라이브러리를 가져와야 합니다.

```kotlin
import kotlin.xml.*
```

그런 다음 'parse' 함수를 사용하여 XML 데이터를 구문 분석할 수 있습니다.

```kotlin
val xmlData = """
<books>
    <book>
        <title>Kotlin in Action</title>
        <author>Dmitry Jemerov</author>
        <year>2017</year>
    </book>
    <book>
        <title>Effective Java</title>
        <author>Joshua Bloch</author>
        <year>2008</year>
    </book>
</books>
""".trimIndent()

val books = xmlData.parseAsXml().books.book

for (book in books) {
    println("Title: ${book.title}")
    println("Author: ${book.author}")
    println("Year: ${book.year}")
    println()
}
```

위의 예에서는 먼저 XML 데이터를 포함하는 문자열을 만듭니다. 그런 다음 'parseAsXml' 함수를 사용하여 XML 데이터를 구문 분석합니다. `parseAsXml` 함수는 `books` 요소를 포함하는 `XmlDocument`를 반환합니다. `books` 요소는 XML 데이터의 각 책에 대한 `book` 요소를 포함합니다.

`for` 루프를 사용하여 `book` 요소를 반복합니다. 각 `book` 요소에 대해 제목, 저자 및 연도를 인쇄합니다.

## Kotlin으로 XML 직렬화

또한 Kotlin을 사용하면 XML 데이터를 쉽게 직렬화할 수 있습니다. `toXmlString` 함수를 사용하여 XML 데이터를 문자열로 변환할 수 있습니다.

```kotlin
val xmlData = books.toXmlString()
```

`toXmlString` 함수는 `XmlDocument`를 가져와 문자열로 변환합니다. 위의 예에서 `toXmlString` 함수를 사용하여 `books` 요소를 문자열로 변환합니다.

## 결론

Kotlin과 XML은 데이터 파싱 및 직렬화를 위한 훌륭한 조합입니다. Kotlin을 사용하면 XML 데이터를 쉽게 구문 분석하고 직렬화할 수 있습니다.