---
title: 021：Kotlin 中的注释处理：在编译时生成代码
description: 
published: true
date: 2023-02-01T16:44:21.511Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:44:19.782Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [021: Annotation Processing in Kotlin: Generating Code at Compile Time***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}


# 021：Kotlin 中的注释处理：在编译时生成代码

Kotlin 是一种在 JVM 上运行的静态类型编程语言。它与 Java 完全互操作，可用于开发 Android 应用程序。 Kotlin 还对注释处理提供了出色的支持。

注解处理是一种在编译时生成代码的方式。它通常用于创建不易在编程语言的源代码中表达的代码。例如，注释处理可用于生成数据绑定代码、创建 Android Parceables 或为 Dagger 2 生成代码。

在本文中，我们将了解如何在 Kotlin 中使用注解处理来为一个简单的数据绑定库生成代码。我们还将了解如何使用 kotlin-apt 插件进行注解处理。

## 什么是注解处理？

注解处理是一种在编译时生成代码的方式。注释处理器是读取程序源代码并根据源代码中存在的注释生成代码的程序。

注释是一种向程序添加元数据的方法。在 Kotlin 中，注释是使用“@”符号添加到程序中的。例如，@Override 注释可用于注释覆盖超类中方法的方法。

 注释也可用于向类添加元数据。在 Kotlin 中，可以使用“@Deprecated”注解对类进行注解，以指示该类已弃用且不应使用。

注释也可用于将元数据添加到包中。在 Kotlin 中，可以使用 @file:JvmName 注释对包进行注释，以指示应将包编译为具有给定名称的 Java 类。

注释也可用于向文件添加元数据。在 Kotlin 中，可以使用 @file:Suppress("unused") 注释对文件进行注释，以指示编译器不应为文件中未使用的变量生成警告。

## 如何在 Kotlin 中使用注解处理

注解处理是一种在编译时生成代码的方式。在 Kotlin 中，注释处理是使用 kotlin-apt 插件完成的。 kotlin-apt 插件是一个 Kotlin 编译器插件，增加了对注解处理的支持。

要使用 kotlin-apt 插件，您需要将以下内容添加到您的 `build.gradle` 文件中：

```groovy
buildscript {
    repositories {
        jcenter()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
        classpath "com.google.auto.service:auto-service:1.0-rc4"
    }
}

apply plugin: 'kotlin-apt'

dependencies {
    apt "com.google.auto.service:auto-service:1.0-rc4"
}
```

kotlin-apt 插件将 `apt` 配置添加到 `build.gradle` 文件。 `apt` 配置用于配置将要使用的注解处理器。在上面的示例中，配置了“auto-service”注解处理器。

`auto-service` 注释处理器用于为`@AutoService` 注释生成代码。 `@AutoService` 注释用于注释应向 `auto-service` 提供程序注册的类。

`auto-service` 提供者是一种提供类列表的服务，这些类已使用 `@AutoService` 注释进行注释。 `auto-service` 提供程序可用于为服务提供程序接口 (SPI) 生成代码。

在上面的示例中，@AutoService 注释用于注释应向 auto-service 提供程序注册的类。 `auto-service` 提供程序将为 `com.google.auto.service.AutoService` 接口生成代码。

`com.google.auto.service.AutoService` 接口是一个 SPI，用于向 `auto-service` 提供程序注册类。 `auto-service` 提供程序将使用 `com.google.auto.service.AutoService` 接口为 `META-INF/services/` 文件生成代码。

`META-INF/services/` 文件用于存储已向 `auto-service` 提供程序注册的类列表。 `java.util.ServiceLoader` 使用 `META-INF/services/` 文件从服务提供者加载类。

在上面的示例中，“META-INF/services/”文件将包含以下内容：

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader` 将使用 `META-INF/services/` 文件加载 `com.example.MyClass` 类。 `com.example.MyClass` 类将在 `auto-service` 提供程序中注册。

`auto-service` 提供程序将为 `com.google.auto.service.AutoService` 接口生成代码。 `com.google.auto.service.AutoService` 接口用于向 `auto-service` 提供程序注册类。

在上面的示例中，`com.google.auto.service.AutoService` 接口用于向 `auto-service` 提供程序注册 `com.example.MyClass` 类。 `auto-service` 提供程序将为 `META-INF/services/` 文件生成代码。

`META-INF/services/` 文件用于存储已向 `auto-service` 提供程序注册的类列表。 `java.util.ServiceLoader` 使用 `META-INF/services/` 文件从服务提供者加载类。

在上面的示例中，“META-INF/services/”文件将包含以下内容：

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader` 将使用 `META-INF/services/` 文件加载 `com.example.MyClass` 类。 `com.example.MyClass` 类将在 `auto-service` 提供程序中注册。

## 结论

注解处理是一种在编译时生成代码的方式。在 Kotlin 中，注释处理是使用 kotlin-apt 插件完成的。 kotlin-apt 插件是一个 Kotlin 编译器插件，增加了对注解处理的支持。

kotlin-apt 插件将 `apt` 配置添加到 `build.gradle` 文件。 `apt` 配置用于配置将要使用的注解处理器。在上面的示例中，配置了“auto-service”注解处理器。

`auto-service` 注释处理器用于为`@AutoService` 注释生成代码。 `@AutoService` 注释用于注释应向 `auto-service` 提供程序注册的类。

`auto-service` 提供者是一种提供类列表的服务，这些类已使用 `@AutoService` 注释进行注释。 `auto-service` 提供程序可用于为服务提供程序接口 (SPI) 生成代码。

在上面的示例中，@AutoService 注释用于注释应向 auto-service 提供程序注册的类。 `auto-service` 提供程序将为 `com.google.auto.service.AutoService` 接口生成代码。

`com.google.auto.service.AutoService` 接口是一个 SPI，用于向 `auto-service` 提供程序注册类。 `auto-service` 提供程序将使用 `com.google.auto.service.AutoService` 接口为 `META-INF/services/` 文件生成代码。

`META-INF/services/` 文件用于存储已向 `auto-service` 提供程序注册的类列表。 `java.util.ServiceLoader` 使用 `META-INF/services/` 文件从服务提供者加载类。

在上面的示例中，“META-INF/services/”文件将包含以下内容：

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader` 将使用 `META-INF/services/` 文件加载 `com.example.MyClass` 类。 `com.example.MyClass` 类将在 `auto-service` 提供程序中注册。

`auto-service` 提供程序将为 `com.google.auto.service.AutoService` 接口生成代码。 `com.google.auto.service.AutoService` 接口用于向 `auto-service` 提供程序注册类。

在上面的示例中，`com.google.auto.service.AutoService` 接口用于向 `auto-service` 提供程序注册 `com.example.MyClass` 类。 `auto-service` 提供程序将为 `META-INF/services/` 文件生成代码。

`META-INF/services/` 文件用于存储已向 `auto-service` 提供程序注册的类列表。 `java.util.ServiceLoader` 使用 `META-INF/services/` 文件从服务提供者加载类。

在上面的示例中，“META-INF/services/”文件将包含以下内容：

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader` 将使用 `META-INF/services/` 文件加载 `com.example.MyClass` 类。 `com.example.MyClass` 类将在 `auto-service` 提供程序中注册。