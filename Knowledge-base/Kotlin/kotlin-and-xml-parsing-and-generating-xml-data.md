---
title: Kotlin 및 XML: XML 데이터 파싱 및 생성
description: 
published: true
date: 2023-02-17T18:07:34.486Z
tags: 
editor: markdown
dateCreated: 2023-01-30T16:05:37.877Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and XML: Parsing and Generating XML Data***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-xml-parsing-and-generating-xml-data)
{.links-list}


# Kotlin 및 XML: XML 데이터 파싱 및 생성

Kotlin은 Java Virtual Machine에서 실행되는 최신 프로그래밍 언어입니다. Kotlin은 객체 지향 및 기능적 프로그래밍 패러다임의 장점을 모두 결합한 간결하고 안전하며 상호 운용 가능한 언어로 알려져 있습니다.

XML은 데이터 저장 및 전송에 일반적으로 사용되는 마크업 언어입니다. XML은 사람과 기계가 모두 읽을 수 있으므로 데이터 교환에 널리 사용되는 형식입니다.

이 기사에서는 Kotlin에서 XML 데이터를 구문 분석하고 생성하는 방법을 살펴보겠습니다. 가장 일반적으로 사용되는 Kotlin용 XML 라이브러리에 대해 알아보고 사용 방법에 대한 몇 가지 예를 살펴보겠습니다.

## Kotlin용 XML 라이브러리

Kotlin에서 사용할 수 있는 많은 XML 라이브러리가 있습니다. 이 섹션에서는 가장 인기 있는 몇 가지를 살펴보겠습니다.

### JUnit 5

JUnit 5는 널리 사용되는 Java용 테스트 프레임워크입니다. 또한 Kotlin을 잘 지원합니다. JUnit 5는 XML 데이터를 테스트하는 데 사용할 수 있는 기본 제공 주석 세트와 함께 제공됩니다. 이러한 주석은 다음과 같습니다.

* @시험
* @이름 표시하기
* @태그
* @장애가 있는

XML 데이터 테스트에 JUnit 5를 사용하려면 build.gradle 파일에 다음 종속성을 추가해야 합니다.

```groovy
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

그런 다음 다음과 같은 간단한 테스트를 작성할 수 있습니다.

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // TODO: write test
}
```

위의 테스트에서 @Test, @DisplayName, @Tag 및 @Disabled 주석을 사용하고 있습니다. @Test 어노테이션은 메소드를 테스트 메소드로 표시하는 데 사용됩니다. @DisplayName 주석은 테스트의 사용자 지정 이름을 지정하는 데 사용됩니다. @Tag 주석은 테스트에 대한 태그를 지정하는 데 사용됩니다. @Disabled 주석은 테스트를 비활성화하는 데 사용됩니다.

그런 다음 테스트 메서드에 XML 구문 분석 코드를 작성할 수 있습니다. 예를 들어 다음 코드를 사용하여 XML 데이터를 구문 분석할 수 있습니다.

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // TODO: write assertions
}
```

위의 코드에서는 DocumentBuilderFactory 클래스를 사용하여 새 XML 문서 빌더를 만듭니다. 그런 다음 parse() 메서드를 사용하여 XML 문자열을 구문 분석합니다.

그런 다음 주장을 작성할 수 있습니다. 예를 들어 다음 코드를 사용하여 XML 문서에 "element1"이라는 이름의 요소가 있음을 어설션할 수 있습니다.

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // Assert that the XML document has an element with the name "element1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    assertNotNull(element1)
}
```

위의 코드에서 getElementsByTagName() 메서드를 사용하여 이름이 "element1"인 요소를 가져옵니다. 그런 다음 assertNotNull() 메서드를 사용하여 요소가 null이 아님을 확인합니다.

또한 다음 코드를 사용하여 요소의 값이 "value1"임을 어설션할 수 있습니다.

```kotlin
@Test
@DisplayName("Test XML data")
@Tag("xml")
@Disabled
fun testXmlData() {
    // Parse XML data
    val xmlString = "<?xml version=\"1.0\" encoding=\"UTF-8\"?><root><element1>value1</element1></root>"
    val xmlDoc = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(xmlString)

    // Assert that the element has the value "value1"
    val element1 = xmlDoc.getElementsByTagName("element1").item(0)
    val value1 = element1.textContent
    assertEquals("value1", value1)
}
```

위의 코드에서는 textContent 속성을 사용하여 요소의 값을 가져옵니다. 그런 다음 assertEquals() 메서드를 사용하여 값이 "value1"과 같다고 주장합니다.

다음 코드를 사용하여 XML 데이터를 생성할 수도 있습니다.

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

위의 코드에서는 createElement() 메서드를 사용하여 새 요소를 만듭니다. 그런 다음 textContent 속성을 사용하여 요소의 값을 설정합니다. 그런 다음 appendChild() 메서드를 사용하여 요소를 문서에 추가합니다.

그런 다음 주장을 작성할 수 있습니다. 예를 들어 다음 코드를 사용하여 XML 문서에 "element1"이라는 이름의 요소가 있음을 어설션할 수 있습니다.

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

위의 코드에서 getElementsByTagName() 메서드를 사용하여 이름이 "element1"인 요소를 가져옵니다. 그런 다음 assertNotNull() 메서드를 사용하여 요소가 null이 아님을 확인합니다.

또한 다음 코드를 사용하여 요소의 값이 "value1"임을 어설션할 수 있습니다.

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

위의 코드에서는 textContent 속성을 사용하여 요소의 값을 가져옵니다. 그런 다음 assertEquals() 메서드를 사용하여 값이 "value1"과 같다고 주장합니다.

다음 코드를 사용하여 XML 데이터를 생성할 수도 있습니다.

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

위의 코드에서 getElementsByTagName() 메서드를 사용하여 이름이 "element1"인 요소를 가져옵니다. 그런 다음 assertNotNull() 메서드를 사용하여 요소가 null이 아님을 확인합니다.

또한 다음 코드를 사용하여 요소의 값이 "value1"임을 어설션할 수 있습니다.

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

위의 코드에서는 textContent 속성을 사용하여 요소의 값을 가져옵니다. 그런 다음 assertEquals() 메서드를 사용하여 값이 "value1"과 같다고 주장합니다.