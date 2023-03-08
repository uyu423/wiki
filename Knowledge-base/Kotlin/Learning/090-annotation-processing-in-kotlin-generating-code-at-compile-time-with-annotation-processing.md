---
title: 090: Kotlin의 주석 처리: 주석 처리를 통해 컴파일 타임에 코드 생성
description: 
published: true
date: 2023-02-16T05:18:20.255Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:18:12.410Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [090: Annotation Processing in Kotlin: Generating Code at Compile-Time with Annotation Processing***English** document is available*](/en/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}


# Kotlin의 주석 처리: 주석 처리로 컴파일 타임에 코드 생성

주석 처리는 Kotlin에서 코드 생성을 위한 강력한 도구입니다. 주석 프로세서를 사용하면 컴파일 타임에 Kotlin 애플리케이션에서 사용할 수 있는 코드를 생성할 수 있습니다.

이 게시물에서는 주석 프로세서를 사용하여 Kotlin에서 코드를 생성하는 방법을 살펴보겠습니다. 주석 프로세서가 무엇이고 어떻게 작동하는지 살펴보겠습니다. 또한 자체 주석 프로세서를 작성하고 Kotlin 애플리케이션에서 사용하는 방법도 살펴보겠습니다.

## 주석 프로세서란?

주석 프로세서는 코드를 컴파일하는 동안 실행되고 코드에 있는 주석을 기반으로 코드를 생성하는 프로그램입니다. 주석 프로세서를 사용하여 상용구 코드를 생성하거나 코드를 검증하거나 자동화할 수 있는 다른 작업을 수행할 수 있습니다.

주석 프로세서는 Kotlin 또는 Java로 작성되며 kotlinc 컴파일러를 사용하여 실행됩니다. 자체 주석 프로세서를 작성하거나 타사 라이브러리에서 제공하는 주석 프로세서를 사용할 수 있습니다.

## 주석 프로세서는 어떻게 작동합니까?

주석 프로세서는 코드를 컴파일할 때 kotlinc 컴파일러에 의해 실행됩니다. kotlinc 컴파일러는 먼저 주석 프로세서를 실행하지 않고 코드를 컴파일합니다. 이를 통해 주석 프로세서는 소스 코드와 컴파일된 바이트코드에 액세스할 수 있습니다.

초기 컴파일 후 kotlinc 컴파일러는 주석 프로세서를 실행합니다. 그러면 주석 프로세서가 코드를 생성할 수 있으며, 이 코드는 컴파일되어 컴파일의 최종 출력에 추가됩니다.

## 자체 주석 프로세서 작성

상용구 코드를 생성하기 위해 고유한 주석 프로세서를 작성해 보겠습니다. IntelliJ IDEA에서 새 Kotlin 프로젝트를 생성하여 시작하겠습니다.

![Kotlin 프로젝트 만들기](https://i.imgur.com/p0lC5Nq.png)

프로젝트 이름을 "Annotation Processor"로 지정하고 프로젝트 구조에 대한 기본 설정을 그대로 둡니다.

![프로젝트 구조](https://i.imgur.com/gY0CWt6.png)

다음으로 `src/main/kotlin` 디렉터리에 새 Kotlin 파일을 만듭니다. 이 파일의 이름은 "GenerateBoilerplate.kt"입니다.

이 파일에서 주석 프로세서를 작성할 것입니다. `@GenerateBoilerplate`라는 새 주석을 정의하여 시작하겠습니다.

```kotlin
@Retention(AnnotationRetention.SOURCE)
@Target(AnnotationTarget.CLASS)
annotation class GenerateBoilerplate
```

이 주석은 클래스에서 사용할 수 있습니다. 소스 코드에는 유지되지만 컴파일된 바이트 코드에는 존재하지 않습니다.

다음으로 `@GenerateBoilerplate` 주석이 달린 클래스에 대한 상용구 코드를 생성하는 함수를 작성합니다. 이 함수는 `Class<*>`를 매개변수로 사용하고 생성된 코드를 포함하는 `String`을 반환합니다.

```kotlin
fun generateBoilerplate(clazz: Class<*>): String {
    val className = clazz.simpleName
    return "class $className {\n}\n"
}
```

이 함수는 단순히 주석이 달린 클래스의 이름으로 `class` 선언을 생성합니다.

이제 상용구 코드를 생성하는 함수를 작성했으므로 주석 프로세서를 작성할 것입니다. `GenerateBoilerplateProcessor`라는 새 클래스를 정의하는 것으로 시작하겠습니다. 이 클래스는 `AbstractProcessor` 클래스를 확장합니다.

```kotlin
class GenerateBoilerplateProcessor : AbstractProcessor() {
}
```

다음으로 `process` 함수를 재정의합니다. 이 함수는 주석 프로세서를 실행할 때 kotlinc 컴파일러에 의해 호출됩니다.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
}
```

이 함수는 두 개의 매개변수를 사용합니다. 첫 번째 매개변수는 프로세서가 처리해야 하는 주석 세트입니다. 두 번째 매개변수는 프로세서가 실행되는 환경입니다.

`roundEnv` 매개변수를 사용하여 코드에서 주석이 달린 요소에 액세스할 수 있습니다. `getElementsAnnotatedWith` 함수를 사용하여 `@GenerateBoilerplate` 주석이 달린 요소 목록을 가져옵니다.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)
}
```

그런 다음 이 목록을 반복하고 주석이 달린 각 요소에 대한 상용구 코드를 생성할 수 있습니다.

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

마지막으로 생성된 코드를 파일에 작성합니다. 새 파일을 생성하기 위해 `Filer` 클래스를 사용할 것입니다. `Filer` 클래스는 `javax.annotation.processing` 패키지의 일부입니다.

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

`createSourceFile` 함수를 사용하여 새 파일을 생성합니다. 주석이 달린 요소의 정규화된 이름을 파일 이름으로 사용합니다.

그런 다음 `Writer` 클래스를 사용하여 생성된 코드를 파일에 작성할 수 있습니다.

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

이제 주석 프로세서를 작성했으므로 Kotlin 코드에서 사용할 수 있습니다. `src/main/kotlin` 디렉토리에 새로운 Kotlin 파일을 생성합니다. 이 파일의 이름을 "Main.kt"로 지정합니다.

이 파일에서 클래스에 `@GenerateBoilerplate` 주석을 추가합니다.

```kotlin
@GenerateBoilerplate
class Foo
```

이 코드를 컴파일하면 kotlinc 컴파일러가 주석 프로세서를 실행합니다. 주석 프로세서는 다음 코드를 생성합니다.

```kotlin
class Foo {
}
```

## Kotlin 애플리케이션에서 주석 프로세서 사용

자체 주석 프로세서를 작성하는 방법을 살펴보았으니 이제 Kotlin 애플리케이션에서 주석 프로세서를 사용하는 방법을 살펴보겠습니다.

먼저 `build.gradle` 파일에 `kotlin-annotation-processing` 플러그인을 추가합니다.

```groovy
plugins {
    id "org.jetbrains.kotlin.plugin.allopen" version "1.3.72"
}
```

그런 다음 주석 프로세서를 실행하도록 `kotlin-annotation-processing` 플러그인을 구성할 수 있습니다. `build.gradle` 파일에 다음 구성을 추가합니다.

```groovy
kotlinAnnotationProcessing {
    processors = [
            "com.example.GenerateBoilerplateProcessor"
    ]
}
```

이제 Kotlin 코드에서 주석 프로세서를 사용할 수 있습니다. `src/main/kotlin` 디렉토리에 새로운 Kotlin 파일을 생성합니다. 이 파일의 이름을 "Main.kt"로 지정합니다.

이 파일에서 클래스에 `@GenerateBoilerplate` 주석을 추가합니다.

```kotlin
@GenerateBoilerplate
class Foo
```

이 코드를 컴파일하면 kotlinc 컴파일러가 주석 프로세서를 실행합니다. 주석 프로세서는 다음 코드를 생성합니다.

```kotlin
class Foo {
}
```

## 결론

이 게시물에서는 주석 프로세서를 사용하여 Kotlin에서 코드를 생성하는 방법을 살펴보았습니다. 자체 주석 프로세서를 작성하는 방법과 이를 Kotlin 애플리케이션에서 사용하는 방법을 살펴보았습니다.