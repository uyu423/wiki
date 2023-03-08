---
title: 095: Kotlin으로 웹 개발: Kotlin과 Spring으로 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-07T01:17:30.391Z
tags: 
editor: markdown
dateCreated: 2023-02-07T01:17:28.755Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [095: Web Development in Kotlin: Building Web Applications with Kotlin and Spring***English** document is available*](/en/Knowledge-base/Kotlin/Learning/095-web-development-in-kotlin-building-web-applications-with-kotlin-and-spring)
{.links-list}


# 095: Kotlin으로 웹 개발: Kotlin과 Spring으로 웹 애플리케이션 구축

Kotlin과 Spring을 사용한 웹 개발은 최신 웹 애플리케이션을 구축하는 좋은 방법입니다. Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 서버 측 및 클라이언트 측 애플리케이션을 모두 개발하는 데 사용할 수 있습니다. Spring은 웹 애플리케이션을 쉽게 만들 수 있게 해주는 널리 사용되는 Java 애플리케이션 프레임워크입니다.

이 게시물에서는 Kotlin과 Spring을 사용하여 웹 애플리케이션을 빌드하는 방법을 살펴보겠습니다. 먼저 웹 개발에 Kotlin을 사용할 때의 몇 가지 이점을 살펴보겠습니다. 그런 다음 Kotlin 및 Spring 개발 환경을 설정하는 방법을 살펴보겠습니다. 마지막으로 Kotlin과 Spring을 사용하는 간단한 예제 웹 애플리케이션을 살펴보겠습니다.

## 웹 개발에 Kotlin을 사용하는 이유는 무엇입니까?

웹 개발에 Kotlin 사용을 고려해야 하는 많은 이유가 있습니다. Kotlin은 코드를 적게 작성하고 더 많은 작업을 수행할 수 있도록 도와주는 간결하고 표현력이 풍부한 프로그래밍 언어입니다. Kotlin은 Java와도 상호 운용 가능합니다. 즉, Kotlin 코드에서 기존 Java 라이브러리를 사용할 수 있습니다. Kotlin은 또한 인기 있는 IntelliJ IDEA Java IDE의 배후에 있는 회사인 JetBrains의 지원을 받기 때문에 Kotlin이 계속해서 개발 및 지원될 것이라는 확신을 가질 수 있습니다.

## Kotlin 및 Spring 개발 환경 설정

Kotlin과 Spring으로 웹 애플리케이션 개발을 시작하기 전에 개발 환경을 설정해야 합니다. Kotlin 컴파일러 및 런타임과 Java 개발 키트(JDK)를 설치해야 합니다. Spring Framework도 설치해야 합니다.

Kotlin을 설치하는 몇 가지 방법이 있습니다. Kotlin 웹사이트에서 Kotlin 컴파일러를 다운로드하거나 Gradle 또는 Maven과 같은 빌드 도구를 사용할 수 있습니다. 이 예제에서는 Gradle을 사용합니다.

먼저 프로젝트의 루트 디렉토리에 `build.gradle`이라는 파일을 만들어야 합니다. 파일에 다음 줄을 추가합니다.

```groovy
plugins {
    id 'org.jetbrains.kotlin.jvm' version '1.3.72'
}

repositories {
    jcenter()
}

dependencies {
    implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
    implementation 'org.springframework.boot:spring-boot-starter-webflux'
}
```

이 파일은 Gradle에게 Kotlin 컴파일러 및 런타임과 Spring Framework를 다운로드하도록 지시합니다.

다음으로 프로젝트의 루트 디렉터리에 `settings.gradle`이라는 파일을 만들어야 합니다. 파일에 다음 줄을 추가합니다.

```groovy
include ':kotlin-web-example'
```

이 파일은 빌드에 프로젝트를 포함하도록 Gradle에 지시합니다.

마지막으로 프로젝트의 루트 디렉터리에 `kotlin-web-example.gradle`이라는 파일을 만들어야 합니다. 파일에 다음 줄을 추가합니다.

```groovy
group 'com.example'
version '0.0.1-SNAPSHOT'

apply plugin: 'org.jetbrains.kotlin.jvm'

repositories {
    jcenter()
}

dependencies {
    implementation 'org.jetbrains.kotlin:kotlin-stdlib-jdk8'
    implementation 'org.springframework.boot:spring-boot-starter-webflux'
}

```

이 파일은 Gradle에게 프로젝트의 그룹과 버전은 물론 필요한 종속성을 알려줍니다.

이제 빌드 파일이 설정되었으므로 `gradle build` 명령을 실행하여 프로젝트를 빌드할 수 있습니다. 이렇게 하면 Kotlin 컴파일러 및 런타임과 Spring Framework가 다운로드됩니다.

## 간단한 Kotlin 및 Spring 웹 애플리케이션

이제 개발 환경이 설정되었으므로 일부 코드를 작성할 준비가 되었습니다. 먼저 프로젝트의 `src/main/kotlin` 디렉토리에 `HelloController.kt`라는 파일을 생성합니다. 파일에 다음 코드 줄을 추가합니다.

```kotlin
package com.example.helloworld

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class HelloController {

    @GetMapping("/hello")
    fun hello(): String {
        return "Hello, world!"
    }

}
```

이 코드는 `hello` 메서드가 있는 간단한 `HelloController` 클래스를 정의합니다. 이 메서드는 `/hello` 경로에 대한 `GET` 요청이 생성될 때 이 메서드가 호출되어야 한다는 것을 Spring에 알리는 `@GetMapping` 주석으로 주석 처리됩니다. `@RestController` 주석은 이 클래스가 웹 요청을 처리하는 컨트롤러임을 Spring에 알려줍니다.

다음으로 프로젝트의 `src/main/kotlin` 디렉토리에 `Application.kt`라는 파일을 생성해야 합니다. 파일에 다음 코드 줄을 추가합니다.

```kotlin
package com.example.helloworld

import org.springframework.boot.SpringApplication
import org.springframework.boot.autoconfigure.SpringBootApplication

@SpringBootApplication
class Application

fun main(args: Array<String>) {
    SpringApplication.run(Application::class.java, *args)
}
```

이 코드는 `@SpringBootApplication` 주석이 달린 간단한 `Application` 클래스를 정의합니다. 이 주석은 이것이 Spring Boot 애플리케이션임을 Spring에 알려줍니다. `main` 메서드는 애플리케이션의 진입점입니다. 이 메서드는 애플리케이션을 시작하는 `SpringApplication.run` 메서드를 호출합니다.

이제 코드를 작성했으므로 `gradle build` 명령을 실행하여 프로젝트를 빌드할 수 있습니다. 그러면 Kotlin 코드가 컴파일되어 JAR 파일로 패키징됩니다.

그런 다음 `java -jar build/libs/kotlin-web-example-0.0.1-SNAPSHOT.jar` 명령을 실행하여 애플리케이션을 시작할 수 있습니다. 그런 다음 http://localhost:8080/hello에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 게시물에서는 Kotlin과 Spring을 사용하여 웹 애플리케이션을 빌드하는 방법을 살펴보았습니다. 우리는 Kotlin이 어떻게 우리가 더 적은 코드를 작성하는 데 도움을 주고 Spring이 어떻게 웹 애플리케이션을 쉽게 만들 수 있게 하는지 살펴보았습니다. 또한 Kotlin 및 Spring 개발 환경을 설정하는 방법과 간단한 웹 애플리케이션을 작성하는 방법도 살펴보았습니다.