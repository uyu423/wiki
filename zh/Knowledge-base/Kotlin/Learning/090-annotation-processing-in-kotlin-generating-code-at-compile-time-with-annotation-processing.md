---
title: 090：Kotlin 中的注释处理：在编译时使用注释处理生成代码
description: 
published: true
date: 2023-02-16T05:18:20.255Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:18:12.409Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [090: Annotation Processing in Kotlin: Generating Code at Compile-Time with Annotation Processing***English** document is available*](/en/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}


# Kotlin 中的注释处理：在编译时使用注释处理生成代码

注解处理是 Kotlin 代码生成的强大工具。通过使用注释处理器，我们可以在编译时生成代码，这些代码可以在我们的 Kotlin 应用程序中使用。

在本文中，我们将了解如何使用注解处理器在 Kotlin 中生成代码。我们将探索注释处理器是什么以及它们是如何工作的。我们还将了解如何编写自己的注释处理器并在我们的 Kotlin 应用程序中使用它们。

## 什么是注解处理器？

注解处理器是在我们的代码编译期间运行的程序，并根据我们代码中存在的注解生成代码。我们可以使用注释处理器来生成样板代码、验证我们的代码或执行任何其他可以自动化的任务。

注释处理器是用 Kotlin 或 Java 编写的，并使用 kotlinc 编译器运行。我们可以编写自己的注释处理器或使用第三方库提供的注释处理器。

## 注释处理器如何工作？

注释处理器由 kotlinc 编译器在编译我们的代码时运行。 kotlinc 编译器首先编译代码而不运行注释处理器。这允许注释处理器访问源代码和编译的字节码。

初始编译后，kotlinc 编译器运行注解处理器。然后注释处理器可以生成代码，这些代码被编译并添加到编译的最终输出中。

## 编写我们自己的注释处理器

让我们编写自己的注释处理器来生成样板代码。我们将从在 IntelliJ IDEA 中创建一个新的 Kotlin 项目开始。

![创建 Kotlin 项目](https://i.imgur.com/p0lC5Nq.png)

我们将项目命名为“Annotation Processor”，并保留项目结构的默认设置。

![项目结构](https://i.imgur.com/gY0CWt6.png)

接下来，我们将在 `src/main/kotlin` 目录中创建一个新的 Kotlin 文件。我们将此文件命名为“GenerateBoilerplate.kt”。

在这个文件中，我们将编写注释处理器。我们将从定义一个名为“@GenerateBoilerplate”的新注解开始。

```kotlin
@Retention(AnnotationRetention.SOURCE)
@Target(AnnotationTarget.CLASS)
annotation class GenerateBoilerplate
```

这个注解可以用在类上。它会保留在源代码中，但不会出现在编译后的字节码中。

接下来，我们将编写一个函数来为用“@GenerateBoilerplate”注释的类生成样板代码。此函数将采用 Class<*> 作为参数，并将返回包含生成代码的 String。

```kotlin
fun generateBoilerplate(clazz: Class<*>): String {
    val className = clazz.simpleName
    return "class $className {\n}\n"
}
```

此函数将简单地生成一个带有注释类名称的“类”声明。

现在我们已经编写了生成样板代码的函数，我们将编写注释处理器。我们将从定义一个名为“GenerateBoilerplateProcessor”的新类开始。此类将扩展 `AbstractProcessor` 类。

```kotlin
class GenerateBoilerplateProcessor : AbstractProcessor() {
}
```

接下来，我们将覆盖 `process` 函数。 kotlinc 编译器在运行我们的注释处理器时将调用此函数。

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
}
```

这个函数有两个参数。第一个参数是处理器应该处理的一组注释。第二个参数是处理器运行的环境。

我们可以使用 `roundEnv` 参数来访问代码中带注释的元素。我们将使用 `getElementsAnnotatedWith` 函数来获取用我们的 `@GenerateBoilerplate` 注释注释的元素列表。

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)
}
```

然后我们可以遍历这个列表并为每个带注释的元素生成样板代码。

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)
    }
}
```

最后，我们将生成的代码写入文件。我们将使用 `Filer` 类来创建一个新文件。 `Filer` 类是 `javax.annotation.processing` 包的一部分。

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())
    }
}
```

我们将使用 `createSourceFile` 函数来创建一个新文件。我们将使用注释元素的完全限定名称作为文件名。

然后我们可以使用 Writer 类将生成的代码写入文件。

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())

        val writer = file.openWriter()
        writer.write(generatedCode)
        writer.close()
    }
}
```

现在我们已经编写了注解处理器，可以在 Kotlin 代码中使用它了。我们将在 `src/main/kotlin` 目录中创建一个新的 Kotlin 文件。我们将此文件命名为“Main.kt”。

在这个文件中，我们将使用我们的“@GenerateBoilerplate”注释来注释一个类。

```kotlin
@GenerateBoilerplate
class Foo
```

当我们编译这段代码时，kotlinc 编译器将运行我们的注解处理器。我们的注释处理器将生成以下代码：

```kotlin
class Foo {
}
```

## 在我们的 Kotlin 应用程序中使用注释处理器

现在我们已经了解了如何编写自己的注释处理器，让我们来看看如何在我们的 Kotlin 应用程序中使用它们。

我们首先将 `kotlin-annotation-processing` 插件添加到我们的 `build.gradle` 文件中。

```groovy
plugins {
    id "org.jetbrains.kotlin.plugin.allopen" version "1.3.72"
}
```

然后我们可以配置“kotlin-annotation-processing”插件来运行我们的注解处理器。我们将以下配置添加到我们的 build.gradle 文件中。

```groovy
kotlinAnnotationProcessing {
    processors = [
            "com.example.GenerateBoilerplateProcessor"
    ]
}
```

我们现在可以在 Kotlin 代码中使用注释处理器。我们将在 `src/main/kotlin` 目录中创建一个新的 Kotlin 文件。我们将此文件命名为“Main.kt”。

在这个文件中，我们将使用我们的“@GenerateBoilerplate”注释来注释一个类。

```kotlin
@GenerateBoilerplate
class Foo
```

当我们编译这段代码时，kotlinc 编译器将运行我们的注解处理器。我们的注释处理器将生成以下代码：

```kotlin
class Foo {
}
```

## 结论

在本文中，我们了解了如何使用注解处理器在 Kotlin 中生成代码。我们已经研究了如何编写我们自己的注释处理器以及如何在我们的 Kotlin 应用程序中使用它们。