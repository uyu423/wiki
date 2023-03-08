---
title: 在 Java 中使用龙目岛
description: 
published: true
date: 2023-01-31T09:05:37.378Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:05:35.708Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Using Lombok in Java***English** version of this document is available*](/en/Knowledge-base/Java/using-lombok-in-java)
{.links-list}




# 在 Java 中使用 Lombok

Lombok 是一个可用于减少 Java 样板代码的库。它用于自动生成 getter、setter、toString、hashCode 和 equals 方法以及构造函数。 Lombok 是开源的，在 MIT 许可下可用。

## 安装

Lombok 可以作为插件安装在您的 IDE 中或添加到您的项目构建路径中。

## # IDE 插件

#### 日蚀

Eclipse 有一个 Lombok 插件。要安装它，请启动 Eclipse 并转到帮助 > Eclipse 市场。搜索 Lombok 并安装插件。

### # IntelliJ IDEA

有一个 Lombok 插件可用于 IntelliJ IDEA。要安装它，请启动 IntelliJ IDEA 并转到“文件”>“设置”。在设置窗口中，转到插件并单击浏览存储库。搜索 Lombok 并安装插件。

### 构建路径

如果您在将使用 Maven 构建的项目中使用 Lombok，则可以通过将以下依赖项添加到 pom.xml 文件来将 Lombok 添加到项目构建路径：

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.20</version>
    <scope>provided</scope>
</dependency>
```

如果您在将使用 Gradle 构建的项目中使用 Lombok，则可以通过将以下依赖项添加到 build.gradle 文件来将 Lombok 添加到项目构建路径：

```groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.16.20'
}
```

## 用法

要在 Java 代码中使用 Lombok，您需要注释要为其生成 getter、setter 和构造函数的字段。例如：

```java
import lombok.Data;

@Data
public class Person {
    private String name;
    private int age;
}
```

@Data 注释将为 Person 类中的所有字段生成 getter、setter 和构造函数。

如果只想为某个字段生成 getter 和 setter，可以使用 @Getter 和 @Setter 注解：

```java
import lombok.Getter;
import lombok.Setter;

public class Person {
    @Getter
    @Setter
    private String name;

    private int age;
}
```

如果只想为类生成构造函数，可以使用@RequiredArgsConstructor 注解：

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Person {
    private final String name;
    private final int age;
}
```

@RequiredArgsConstructor 注释将为所有标记为 final 或具有 @NonNull 注释的字段生成带有参数的构造函数。

如果要为类生成 toString 方法，可以使用 @ToString 注解：

```java
import lombok.ToString;

@ToString
public class Person {
    private String name;
    private int age;
}
```

如果要为类生成hashCode方法，可以使用@HashCode注解：

```java
import lombok.HashCode;

@HashCode
public class Person {
    private String name;
    private int age;
}
```

如果你想为一个类生成一个equals方法，你可以使用@EqualsAndHashCode注解：

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Person {
    private String name;
    private int age;
}
```

# # 优点和缺点

Lombok 是一个非常有用的工具，可以帮助减少 Java 中的样板代码。但是，使用 Lombok 有一些潜在的缺点。

首先，Lombok 生成在源代码中不可见的代码。这会使调试由生成的代码引起的问题变得困难。

其次，Lombok 会降低代码的可读性。例如，@Data 注解会生成很多代码，这会使源代码更难理解。

第三，Lombok 会使某些 Java 工具难以使用，例如代码覆盖工具。这是因为 Lombok 生成的代码在源代码中是不可见的。

第四，Lombok 会使将代码迁移到新版本的 Java 变得困难。这是因为 Lombok 生成的代码特定于编译它的 Java 版本。

最后，Lombok 并没有被广泛使用。这意味着可用于 Lombok 的文档和支持较少。

## 结论

Lombok 是一个可用于减少 Java 样板代码的库。它用于自动生成 getter、setter、toString、hashCode 和 equals 方法以及构造函数。 Lombok 是开源的，在 MIT 许可下可用。

Lombok 是一个非常有用的工具，可以帮助减少 Java 中的样板代码。但是，使用 Lombok 有一些潜在的缺点。首先，Lombok 生成在源代码中不可见的代码。这会使调试由生成的代码引起的问题变得困难。其次，Lombok 会降低代码的可读性。例如，@Data 注解会生成很多代码，这会使源代码更难理解。第三，Lombok 会使某些 Java 工具难以使用，例如代码覆盖工具。这是因为 Lombok 生成的代码在源代码中是不可见的。第四，Lombok 会使将代码迁移到新版本的 Java 变得困难。这是因为 Lombok 生成的代码特定于编译它的 Java 版本。最后，Lombok 并没有被广泛使用。这意味着可用于 Lombok 的文档和支持较少。