---
title: Kotlin 및 JSON: 데이터 파싱 및 직렬화
description: 
published: true
date: 2023-02-01T18:04:48.198Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:04:43.861Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and JSON: Parsing and Serializing Data***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-json-parsing-and-serializing-data)
{.links-list}


Kotlin 및 JSON: 데이터 파싱 및 직렬화
==============================================

Kotlin의 인기가 계속 높아지면서 점점 더 많은 개발자가 JSON 데이터를 구문 분석하고 직렬화할 때 이 언어로 작업할 수 있는 방법을 찾고 있다는 것은 놀라운 일이 아닙니다.

이 기사에서는 이 작업을 수행하는 데 가장 많이 사용되는 몇 가지 방법을 살펴보겠습니다.

Kotlin 표준 라이브러리로 JSON 파싱
------------------------------------------------------------

Kotlin에서 JSON을 파싱하는 첫 번째이자 가장 확실한 방법은 Kotlin 표준 라이브러리의 내장 [JSON 클래스][1]를 사용하는 것입니다.

이 클래스는 JSON 데이터를 읽고 쓰는 것은 물론 JSON 데이터를 Kotlin 객체로 변환하는 것과 같은 일반적인 작업을 수행하기 위한 다양한 메서드를 제공합니다.

JSON 클래스에서 가장 유용한 메소드 중 하나는 JSON 문자열을 Kotlin `JsonObject`로 구문 분석하는 데 사용할 수 있는 `parse()` 메소드입니다.

```kotlin
val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = JSON.parse(jsonString)
```

`JsonObject`가 있으면 해당 클래스의 다양한 메서드를 사용하여 포함된 데이터에 액세스할 수 있습니다. 예를 들어, `get()` 메서드는 특정 키의 값을 검색하는 데 사용할 수 있습니다.

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

JSON 배열을 구문 분석해야 하는 경우 `JsonArray`를 반환하는 `parseArray()` 메서드를 사용할 수 있습니다. 이 클래스는 배열에서 데이터를 검색하는 데 사용할 수 있는 `get()` 및 `size()`와 같은 `JsonObject` 클래스와 유사한 메서드를 제공합니다.

Gson 라이브러리로 JSON 구문 분석
-----------------------------------

Kotlin에서 JSON을 파싱하는 또 다른 인기 있는 방법은 [Gson][2] 라이브러리를 사용하는 것입니다.

Gson은 Java 개체를 JSON 데이터로 변환하는 데 사용할 수 있는 Java 라이브러리입니다. 또한 Kotlin 지원이 뛰어나며 JSON 데이터를 Kotlin 개체로 구문 분석하는 데 사용할 수 있습니다.

Gson을 사용하려면 먼저 프로젝트에 추가해야 합니다. Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가할 수 있습니다.

```groovy
implementation 'com.google.code.gson:gson:2.8.5'
```

Gson이 프로젝트에 추가되면 `Gson` 인스턴스를 생성하고 이를 사용하여 JSON 데이터를 구문 분석할 수 있습니다.

```kotlin
val gson = Gson()

val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = gson.fromJson(jsonString, JsonObject::class.java)
```

보시다시피 `fromJson()` 메서드는 JSON 문자열과 Kotlin 클래스를 매개변수로 사용합니다. `JsonObject` 클래스는 표준 Java `JsonObject` 클래스를 둘러싼 Kotlin 래퍼입니다.

`JsonObject`가 있으면 해당 클래스의 다양한 메서드를 사용하여 포함된 데이터에 액세스할 수 있습니다. 예를 들어, `get()` 메서드는 특정 키의 값을 검색하는 데 사용할 수 있습니다.

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

JSON 배열을 구문 분석해야 하는 경우 `JsonArray` 클래스와 함께 `fromJson()` 메서드를 사용할 수 있습니다. 이 클래스는 배열에서 데이터를 검색하는 데 사용할 수 있는 `get()` 및 `size()`와 같은 `JsonObject` 클래스와 유사한 메서드를 제공합니다.

Jackson 라이브러리로 JSON 구문 분석
--------------------------------------

Kotlin에서 JSON을 파싱하는 또 다른 인기 있는 방법은 [Jackson][3] 라이브러리를 사용하는 것입니다.

Jackson은 Java 객체와 JSON 데이터 간에 변환하는 데 사용할 수 있는 Java 라이브러리입니다. 또한 Kotlin 지원이 뛰어나며 JSON 데이터를 Kotlin 개체로 구문 분석하는 데 사용할 수 있습니다.

Jackson을 사용하려면 먼저 프로젝트에 추가해야 합니다. Gradle을 사용하는 경우 `build.gradle` 파일에 다음 종속성을 추가할 수 있습니다.

```groovy
implementation 'com.fasterxml.jackson.core:jackson-databind:2.9.8'
```

프로젝트에 Jackson이 추가되면 `ObjectMapper` 인스턴스를 생성하고 이를 사용하여 JSON 데이터를 구문 분석할 수 있습니다.

```kotlin
val objectMapper = ObjectMapper()

val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = objectMapper.readValue(jsonString, JsonNode::class.java)
```

보시다시피 `readValue()` 메서드는 JSON 문자열과 Kotlin 클래스를 매개변수로 사용합니다. `JsonNode` 클래스는 표준 Java `JsonNode` 클래스를 둘러싼 Kotlin 래퍼입니다.

`JsonNode`가 있으면 해당 클래스의 다양한 메서드를 사용하여 포함된 데이터에 액세스할 수 있습니다. 예를 들어, `get()` 메서드는 특정 키의 값을 검색하는 데 사용할 수 있습니다.

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

JSON 배열을 구문 분석해야 하는 경우 `JsonNode` 클래스와 함께 `readValue()` 메서드를 사용할 수 있습니다. 이 클래스는 배열에서 데이터를 검색하는 데 사용할 수 있는 `get()` 및 `size()`와 같은 `JsonObject` 클래스와 유사한 메서드를 제공합니다.

Kotlin 표준 라이브러리로 JSON 직렬화
--------------------------------------------------

Kotlin 표준 라이브러리는 또한 JSON 데이터를 직렬화하기 위한 다양한 방법을 제공합니다.

가장 일반적으로 사용되는 방법은 `JsonObject`를 JSON 문자열로 직렬화하는 데 사용할 수 있는 `stringify()` 방법입니다.

```kotlin
val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = JSON.stringify(jsonObject)
```

JSON 배열을 직렬화해야 하는 경우 `JsonArray`와 함께 `stringify()` 메서드를 사용할 수 있습니다.

Gson 라이브러리로 JSON 직렬화
--------------------------------------

Gson 라이브러리를 사용하여 JSON 데이터를 직렬화할 수도 있습니다.

이렇게 하려면 먼저 `Gson` 인스턴스를 만든 다음 해당 인스턴스에서 `toJson()` 메서드를 호출하여 직렬화하려는 개체를 전달해야 합니다.

```kotlin
val gson = Gson()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = gson.toJson(jsonObject)
```

JSON 배열을 직렬화해야 하는 경우 `JsonArray`와 함께 `toJson()` 메서드를 사용할 수 있습니다.

Jackson 라이브러리로 JSON 직렬화
------------------------------------------

Jackson 라이브러리를 사용하여 JSON 데이터를 직렬화할 수도 있습니다.

이렇게 하려면 먼저 `ObjectMapper` 인스턴스를 만든 다음 해당 인스턴스에서 `writeValueAsString()` 메서드를 호출하여 직렬화하려는 개체를 전달해야 합니다.

```kotlin
val objectMapper = ObjectMapper()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = objectMapper.writeValueAsString(jsonObject)
```

JSON 배열을 직렬화해야 하는 경우 `JsonArray`와 함께 `writeValueAsString()` 메서드를 사용할 수 있습니다.

결론
----------

이 기사에서는 Kotlin에서 JSON 데이터를 구문 분석하고 직렬화하는 가장 인기 있는 몇 가지 방법을 살펴보았습니다.

Kotlin 표준 라이브러리의 내장 JSON 클래스를 사용하는 방법과 Gson 및 Jackson 라이브러리를 사용하는 방법을 살펴보았습니다.

선택하는 방법은 궁극적으로 개인 취향에 따라 다릅니다.

[1]: https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-json/
[2]: https://github.com/google/gson
[3]: https://github.com/FasterXML/jackson