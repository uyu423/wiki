---
title: Kotlin 및 JSON: JSON 데이터 처리 및 생성
description: 
published: true
date: 2023-02-18T08:33:08.039Z
tags: 
editor: markdown
dateCreated: 2023-02-18T08:33:01.043Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and JSON: Processing and Generating JSON Data***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-json-processing-and-generating-json-data)
{.links-list}


# Kotlin과 JSON: JSON 데이터 처리 및 생성

JSON(JavaScript Object Notation)은 구조화된 데이터를 나타내는 데 사용되는 널리 사용되는 데이터 형식입니다. Kotlin은 Java와 상호 운용되도록 설계된 최신 프로그래밍 언어입니다. 이 기사에서는 Kotlin을 사용하여 JSON 데이터로 작업하는 방법을 살펴보겠습니다.

먼저 Kotlin에서 JSON 데이터를 처리하는 다양한 방법을 살펴보겠습니다. 그런 다음 JSON 데이터를 생성하는 방법을 살펴보겠습니다. Kotlin에서 JSON 데이터로 작업하기 위한 몇 가지 팁을 살펴보며 마무리하겠습니다.

## JSON 데이터 처리

Kotlin에서 JSON 데이터를 처리하는 몇 가지 방법이 있습니다. 표준 라이브러리를 사용하거나 Kotlinx.Serialization을 사용하거나 Gson과 같은 타사 라이브러리를 사용할 수 있습니다.

### 표준 라이브러리 사용

Kotlin 표준 라이브러리는 JSON 데이터를 처리하기 위한 일련의 함수를 제공합니다. 이러한 함수는 `kotlin.io.json` 패키지에 있습니다.

표준 라이브러리를 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
```

그런 다음 `json` 함수를 사용하여 JSON 데이터를 구문 분석할 수 있습니다.

```kotlin
val jsonData = """
{
    "name": "john",
    "age": 30
}
""".trimIndent()

val data = json.parseJson(jsonData)
```

`data` 변수는 이제 `JsonObject`입니다. `get` 함수를 사용하여 `JsonObject`의 데이터에 액세스할 수 있습니다.

```kotlin
val name = data.get("name") // "john"
val age = data.get("age") // 30
```

또한 `getValue` 함수를 사용하여 데이터를 특정 유형으로 가져올 수 있습니다.

```kotlin
val name = data.getValue<String>("name") // "john"
val age = data.getValue<Int>("age") // 30
```

존재하지 않는 값을 얻으려고 하면 `null` 값을 얻게 됩니다.

```kotlin
val address = data.getValue<String>("address") // null
```

이를 방지하기 위해 `optValue` 함수를 사용할 수 있습니다. 이 함수는 요청된 값이 존재하지 않는 경우 기본값을 반환합니다.

```kotlin
val address = data.optValue<String>("address") // ""
```

또한 `jsonArray` 함수를 사용하여 JSON 배열을 구문 분석할 수 있습니다.

```kotlin
val jsonData = """
[
    {
        "name": "john",
        "age": 30
    },
    {
        "name": "jane",
        "age": 20
    }
]
""".trimIndent()

val data = json.parseJson(jsonData)
```

`data` 변수는 이제 `JsonArray`입니다. `get` 함수를 사용하여 `JsonArray`의 데이터를 가져올 수 있습니다.

```kotlin
val firstPerson = data.get(0) // { "name": "john", "age": 30 }
val secondPerson = data.get(1) // { "name": "jane", "age": 20 }
```

또한 `getValue` 함수를 사용하여 데이터를 특정 유형으로 가져올 수 있습니다.

```kotlin
val firstPerson = data.getValue<JsonObject>(0) // { "name": "john", "age": 30 }
val secondPerson = data.getValue<JsonObject>(1) // { "name": "jane", "age": 20 }
```

존재하지 않는 값을 얻으려고 하면 `null` 값을 얻게 됩니다.

```kotlin
val thirdPerson = data.getValue<JsonObject>(2) // null
```

### Kotlinx.Serialization 사용

Kotlinx.Serialization은 JSON 데이터 직렬화 및 역직렬화를 지원하는 라이브러리입니다. Kotlinx.Serialization을 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'org.jetbrains.kotlinx:kotlinx-serialization-runtime:0.12.0'
```

그런 다음 `@Serializable` 주석을 사용하여 데이터 클래스에 주석을 달 수 있습니다.

```kotlin
@Serializable
data class Person(val name: String, val age: Int)
```

그런 다음 `Json` 클래스를 사용하여 데이터 클래스를 직렬화 및 역직렬화할 수 있습니다.

```kotlin
val jsonData = """
{
    "name": "john",
    "age": 30
}
""".trimIndent()

val data = Json.decodeFromString<Person>(jsonData)
```

`data` 변수는 이제 `Person` 개체입니다. 데이터 클래스에서 정의한 속성을 사용하여 `Person` 개체의 데이터에 액세스할 수 있습니다.

```kotlin
val name = data.name // "john"
val age = data.age // 30
```

또한 `Json` 클래스를 사용하여 데이터 클래스를 JSON 데이터로 직렬화할 수 있습니다.

```kotlin
val data = Person("john", 30)
val jsonData = Json.encodeToString(data)
```

`jsonData` 변수는 이제 `Person` 개체의 데이터를 포함하는 JSON 문자열입니다.

### Gson 사용

Gson은 JSON 데이터 작업을 위한 인기 있는 타사 라이브러리입니다. Gson을 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'com.google.code.gson:gson:2.8.6'
```

그런 다음 `fromJson` 함수를 사용하여 JSON 데이터를 역직렬화할 수 있습니다.

```kotlin
val jsonData = """
{
    "name": "john",
    "age": 30
}
""".trimIndent()

val data = gson.fromJson(jsonData)
```

`data` 변수는 이제 `JsonObject`입니다. `get` 함수를 사용하여 `JsonObject`의 데이터에 액세스할 수 있습니다.

```kotlin
val name = data.get("name") // "john"
val age = data.get("age") // 30
```

`getAsJsonObject` 함수를 사용하여 데이터를 `JsonObject`로 가져올 수도 있습니다.

```kotlin
val name = data.getAsJsonObject("name") // "john"
val age = data.getAsJsonObject("age") // 30
```

존재하지 않는 값을 얻으려고 하면 `null` 값을 얻게 됩니다.

```kotlin
val address = data.getAsJsonObject("address") // null
```

이를 방지하기 위해 `optAsJsonObject` 함수를 사용할 수 있습니다. 이 함수는 요청된 값이 존재하지 않는 경우 `null` 값과 함께 `JsonObject`를 반환합니다.

```kotlin
val address = data.optAsJsonObject("address") // {"address":null}
```

또한 `fromJson` 함수를 사용하여 JSON 배열을 역직렬화할 수 있습니다.

```kotlin
val jsonData = """
[
    {
        "name": "john",
        "age": 30
    },
    {
        "name": "jane",
        "age": 20
    }
]
""".trimIndent()

val data = gson.fromJson(jsonData)
```

`data` 변수는 이제 `JsonArray`입니다. `get` 함수를 사용하여 `JsonArray`의 데이터를 가져올 수 있습니다.

```kotlin
val firstPerson = data.get(0) // { "name": "john", "age": 30 }
val secondPerson = data.get(1) // { "name": "jane", "age": 20 }
```

`getAsJsonArray` 함수를 사용하여 데이터를 `JsonArray`로 가져올 수도 있습니다.

```kotlin
val firstPerson = data.getAsJsonArray(0) // { "name": "john", "age": 30 }
val secondPerson = data.getAsJsonArray(1) // { "name": "jane", "age": 20 }
```

존재하지 않는 값을 얻으려고 하면 `null` 값을 얻게 됩니다.

```kotlin
val thirdPerson = data.getAsJsonArray(2) // null
```

이를 방지하기 위해 `optAsJsonArray` 함수를 사용할 수 있습니다. 이 함수는 요청된 값이 존재하지 않는 경우 `null` 값과 함께 `JsonArray`를 반환합니다.

```kotlin
val thirdPerson = data.optAsJsonArray(2) // [null]
```

또한 `toJson` 함수를 사용하여 데이터 클래스를 JSON 데이터로 직렬화할 수 있습니다.

```kotlin
val data = Person("john", 30)
val jsonData = gson.toJson(data)
```

`jsonData` 변수는 이제 `Person` 개체의 데이터를 포함하는 JSON 문자열입니다.

## JSON 데이터 생성

Kotlin에서 JSON 데이터를 생성하는 몇 가지 방법이 있습니다. 표준 라이브러리를 사용하거나 Kotlinx.Serialization을 사용하거나 Gson과 같은 타사 라이브러리를 사용할 수 있습니다.

### 표준 라이브러리 사용

Kotlin 표준 라이브러리는 JSON 데이터를 생성하기 위한 일련의 함수를 제공합니다. 이러한 함수는 `kotlin.io.json` 패키지에 있습니다.

표준 라이브러리를 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
```

`jsonObject` 함수를 사용하여 `JsonObject`를 만들 수 있습니다.

```kotlin
val data = jsonObject {
    "name" to "john"
    "age" to 30
}
```

그런 다음 `toString` 함수를 사용하여 `JsonObject`를 JSON 문자열로 변환할 수 있습니다.

```kotlin
val jsonData = data.toString()
```

`jsonData` 변수는 이제 `JsonObject`의 데이터를 포함하는 JSON 문자열입니다.

`jsonArray` 함수를 사용하여 `JsonArray`를 만들 수도 있습니다.

```kotlin
val data = jsonArray {
    + jsonObject {
        "name" to "john"
        "age" to 30
    }
    + jsonObject {
        "name" to "jane"
        "age" to 20
    }
}
```

그런 다음 `toString` 함수를 사용하여 `JsonArray`를 JSON 문자열로 변환할 수 있습니다.

```kotlin
val jsonData = data.toString()
```

`jsonData` 변수는 이제 `JsonArray`의 데이터를 포함하는 JSON 문자열입니다.

### Kotlinx.Serialization 사용

Kotlinx.Serialization은 JSON 데이터 직렬화 및 역직렬화를 지원하는 라이브러리입니다. Kotlinx.Serialization을 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'org.jetbrains.kotlinx:kotlinx-serialization-runtime:0.12.0'
```

그런 다음 `@Serializable` 주석을 사용하여 데이터 클래스에 주석을 달 수 있습니다.

```kotlin
@Serializable
data class Person(val name: String, val age: Int)
```

그런 다음 `Json` 클래스를 사용하여 데이터 클래스를 직렬화 및 역직렬화할 수 있습니다.

```kotlin
val data = Person("john", 30)
val jsonData = Json.encodeToString(data)
```

`jsonData` 변수는 이제 `Person` 개체의 데이터를 포함하는 JSON 문자열입니다.

### Gson 사용

Gson은 JSON 데이터 작업을 위한 인기 있는 타사 라이브러리입니다. Gson을 사용하려면 `build.gradle` 파일에 종속성을 추가해야 합니다.

```
implementation 'com.google.code.gson:gson:2.8.6'
```

그런 다음 `toJson` 함수를 사용하여 데이터 클래스를 JSON 데이터로 직렬화할 수 있습니다.

```kotlin
val data = Person("john", 30)
val jsonData = gson.toJson(data)
```

`jsonData` 변수는 이제 `Person` 개체의 데이터를 포함하는 JSON 문자열입니다.

## JSON 데이터 작업을 위한 팁

다음은 Kotlin에서 JSON 데이터로 작업하기 위한 몇 가지 팁입니다.

* `jsonObject` 함수를 사용하여 `JsonObject`를 만듭니다.
* `jsonArray` 함수를 사용하여 `JsonArray`를 만듭니다.
* `get` 함수를 사용하여 `JsonObject`의 키 값을 가져옵니다.
* `getValue` 함수를 사용하여 `JsonObject`의 키 값을 특정 유형으로 가져옵니다.
* `optValue` 함수를 사용하여 `JsonObject`의 키 값을 기본값이 있는 특정 유형으로 가져옵니다.
* `get` 함수를 사용하여 `JsonArray`의 인덱스에서 값을 가져옵니다.
* `getValue` 함수를 사용하여 `JsonArray`의 인덱스 값을 특정 유형으로 가져옵니다.
* `toString` 함수를 사용하여 `JsonObject` 또는 `JsonArray`를 JSON 문자열로 변환합니다.
* `@Serializable` 주석을 사용하여 데이터 클래스에 주석을 답니다.
* `Json` 클래스를 사용하여 데이터 클래스를 직렬화 및 역직렬화합니다.
* `toJson` 함수를 사용하여 데이터 클래스를 JSON 데이터로 직렬화합니다.

## 결론

이 기사에서는 Kotlin을 사용하여 JSON 데이터로 작업하는 방법을 살펴보았습니다. JSON 데이터를 처리하는 다양한 방법과 JSON 데이터를 생성하는 방법을 살펴보았습니다. 또한 Kotlin에서 JSON 데이터로 작업하기 위한 몇 가지 팁도 살펴보았습니다.