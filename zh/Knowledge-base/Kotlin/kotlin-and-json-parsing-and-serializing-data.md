---
title: Kotlin 和 JSON：解析和序列化数据
description: 
published: true
date: 2023-02-01T18:04:48.198Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:04:43.867Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Kotlin and JSON: Parsing and Serializing Data***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-json-parsing-and-serializing-data)
{.links-list}


Kotlin 和 JSON：解析和序列化数据
============================================

随着 Kotlin 的日益流行，越来越多的开发人员正在寻找在解析和序列化 JSON 数据时使用这种语言的方法也就不足为奇了。

在本文中，我们将了解一些最流行的方法。

使用 Kotlin 标准库解析 JSON
------------------------------------------

在 Kotlin 中解析 JSON 的第一个也是最明显的方法是使用 Kotlin 标准库中的内置 [JSON 类][1]。

此类提供了许多用于读取和写入 JSON 数据的方法，以及用于执行常见任务的方法，例如将 JSON 数据与 Kotlin 对象相互转换。

JSON 类中最有用的方法之一是 `parse()` 方法，它可用于将 JSON 字符串解析为 Kotlin `JsonObject`：

```kotlin
val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = JSON.parse(jsonString)
```

一旦有了 JsonObject，就可以使用该类的各种方法来访问它包含的数据。例如，`get()` 方法可用于检索特定键的值：

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

如果需要解析 JSON 数组，可以使用 parseArray() 方法，该方法将返回一个 JsonArray。该类提供了与 JsonObject 类类似的方法，例如 get() 和 size() ，可用于从数组中检索数据。

使用 Gson 库解析 JSON
----------------------------------

在 Kotlin 中解析 JSON 的另一种流行方法是使用 [Gson][2] 库。

Gson 是一个 Java 库，可用于将 Java 对象与 JSON 数据相互转换。它还具有出色的 Kotlin 支持，可用于将 JSON 数据解析为 Kotlin 对象。

要使用 Gson，您首先需要将其添加到您的项目中。如果您使用的是 Gradle，则可以将以下依赖项添加到 `build.gradle` 文件中：

```groovy
implementation 'com.google.code.gson:gson:2.8.5'
```

将 Gson 添加到您的项目后，您可以创建一个 `Gson` 实例并使用它来解析 JSON 数据：

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

如您所见，`fromJson()` 方法将一个 JSON 字符串和一个 Kotlin 类作为参数。 `JsonObject` 类是标准 Java `JsonObject` 类的 Kotlin 包装器。

一旦有了 JsonObject，就可以使用该类的各种方法来访问它包含的数据。例如，`get()` 方法可用于检索特定键的值：

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

如果需要解析 JSON 数组，可以使用带有 `JsonArray` 类的 `fromJson()` 方法。该类提供了与 JsonObject 类类似的方法，例如 get() 和 size() ，可用于从数组中检索数据。

使用 Jackson 库解析 JSON
--------------------------------------

在 Kotlin 中解析 JSON 的另一种流行方法是使用 [Jackson][3] 库。

Jackson 是一个 Java 库，可用于将 Java 对象与 JSON 数据相互转换。它还具有出色的 Kotlin 支持，可用于将 JSON 数据解析为 Kotlin 对象。

要使用 Jackson，您首先需要将其添加到您的项目中。如果您使用的是 Gradle，则可以将以下依赖项添加到 `build.gradle` 文件中：

```groovy
implementation 'com.fasterxml.jackson.core:jackson-databind:2.9.8'
```

将 Jackson 添加到您的项目后，您可以创建一个 ObjectMapper 实例并使用它来解析 JSON 数据：

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

如您所见，`readValue()` 方法将一个 JSON 字符串和一个 Kotlin 类作为参数。 `JsonNode` 类是标准 Java `JsonNode` 类的 Kotlin 包装器。

一旦有了 JsonNode，就可以使用该类的各种方法来访问它包含的数据。例如，`get()` 方法可用于检索特定键的值：

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

如果需要解析 JSON 数组，可以使用带有 `JsonNode` 类的 `readValue()` 方法。该类提供了与 JsonObject 类类似的方法，例如 get() 和 size() ，可用于从数组中检索数据。

使用 Kotlin 标准库序列化 JSON
----------------------------------------------

Kotlin 标准库还提供了许多序列化 JSON 数据的方法。

最常用的方法是 `stringify()` 方法，可用于将 `JsonObject` 序列化为 JSON 字符串：

```kotlin
val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = JSON.stringify(jsonObject)
```

如果需要序列化 JSON 数组，可以使用带有 `JsonArray` 的 `stringify()` 方法。

使用 Gson 库序列化 JSON
--------------------------------------

Gson 库也可用于序列化 JSON 数据。

为此，您首先需要创建一个 `Gson` 实例，然后在该实例上调用 `toJson()` 方法，传入要序列化的对象：

```kotlin
val gson = Gson()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = gson.toJson(jsonObject)
```

如果需要序列化 JSON 数组，可以使用带有 `JsonArray` 的 `toJson()` 方法。

使用 Jackson 库序列化 JSON
------------------------------------------

Jackson 库也可用于序列化 JSON 数据。

为此，您首先需要创建一个 ObjectMapper 实例，然后在该实例上调用 writeValueAsString() 方法，传入要序列化的对象：

```kotlin
val objectMapper = ObjectMapper()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = objectMapper.writeValueAsString(jsonObject)
```

如果需要序列化 JSON 数组，可以使用带有 `JsonArray` 的 `writeValueAsString()` 方法。

结论
----------

在本文中，我们了解了在 Kotlin 中解析和序列化 JSON 数据的一些最流行的方法。

我们已经了解了如何使用 Kotlin 标准库中的内置 JSON 类，以及如何使用 Gson 和 Jackson 库。

您选择哪种方法最终取决于您自己的个人喜好。

[1]: https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-json/
[2]: https://github.com/google/gson
[3]：https://github.com/FasterXML/jackson