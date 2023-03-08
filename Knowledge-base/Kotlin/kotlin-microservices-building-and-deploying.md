---
title: Kotlin 마이크로서비스: 구축 및 배포
description: 
published: true
date: 2023-02-17T18:02:20.447Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:11:53.352Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin Microservices: Building and Deploying***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-microservices-building-and-deploying)
{.links-list}


# Kotlin 마이크로서비스: 빌드 및 배포

마이크로서비스는 애플리케이션을 느슨하게 결합된 서비스 모음으로 구성하는 일종의 소프트웨어 아키텍처입니다. 이 접근 방식은 모듈성을 개선하고 개발, 배포 및 유지 관리를 더 쉽게 하기 위해 사용됩니다.

Kotlin은 JVM(Java Virtual Machine)에서 실행되고 Android 앱, 웹 앱, 서버 측 애플리케이션 등을 개발하는 데 사용할 수 있는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 Java 프로그래밍 언어와 완벽하게 호환되며 간결한 구문 및 null 안전 기능으로 인해 인기를 얻고 있습니다.

이 기사에서는 Kotlin 마이크로서비스를 구축하고 배포하는 방법을 살펴보겠습니다. 먼저 마이크로서비스가 무엇이고 왜 유익한지 살펴보겠습니다. 그런 다음 Gradle 빌드 도구를 사용하여 Kotlin 프로젝트를 만드는 방법을 살펴보겠습니다. 마지막으로 Kotlin 마이크로서비스를 서버에 배포합니다.

## 마이크로서비스란?

마이크로서비스는 애플리케이션을 느슨하게 결합된 서비스 모음으로 구성하는 일종의 소프트웨어 아키텍처입니다. 이 접근 방식은 모듈성을 개선하고 개발, 배포 및 유지 관리를 더 쉽게 하기 위해 사용됩니다.

마이크로서비스는 일반적으로 비즈니스 기능을 중심으로 구축되며 각 마이크로서비스에는 잘 정의된 경계가 있습니다. 이 경계는 물리적(예: 다른 기계) 또는 논리적(예: 다른 프로세스)일 수 있습니다.

각 마이크로 서비스는 단일 비즈니스 기능을 담당하며 다른 마이크로 서비스와 독립적으로 배포 및 확장할 수 있습니다. 즉, 하나의 마이크로 서비스를 업데이트해야 하는 경우 해당 마이크로 서비스만 재배포하면 됩니다. 다른 마이크로 서비스는 중단 없이 계속 실행할 수 있습니다.

## 마이크로서비스를 사용하는 이유

마이크로서비스를 사용하면 다음과 같은 많은 이점이 있습니다.

* **향상된 모듈성:** 마이크로서비스는 일반적으로 비즈니스 기능을 중심으로 구축되어 모듈성을 개선하고 애플리케이션 전체를 더 쉽게 이해할 수 있도록 합니다.

* **더 쉬운 개발:** 서비스를 독립적으로 개발 및 배포할 수 있으므로 개발자가 다른 서비스에 영향을 주지 않고 자체 서비스에서 작업할 수 있습니다.

* **더 쉬운 테스트:** 서비스를 독립적으로 테스트할 수 있으므로 버그를 쉽게 식별하고 수정할 수 있습니다.

* **간편한 배포:** 서비스를 독립적으로 배포할 수 있으므로 애플리케이션의 나머지 부분에 영향을 주지 않고 업데이트할 수 있습니다.

* **더 쉬운 확장:** 서비스는 독립적으로 확장될 수 있습니다. 즉, 사용 중인 서비스만 확장하면 됩니다.

## Kotlin 마이크로서비스 구축

이 섹션에서는 Gradle 빌드 도구를 사용하여 Kotlin 마이크로서비스를 빌드하는 방법을 살펴보겠습니다. Gradle Kotlin DSL을 사용하여 새로운 Kotlin 프로젝트를 만드는 것으로 시작하겠습니다.

### 프로젝트 만들기

먼저 Gradle Kotlin DSL을 사용하여 새 Kotlin 프로젝트를 만듭니다. 프로젝트 이름을 "helloworld-microservice"로 지정합니다.

    $ gradle init --type kotlin-library

이렇게 하면 다음 디렉터리 구조로 새 Kotlin 프로젝트가 생성됩니다.

    .
    └── helloworld-마이크로서비스
        ├── build.gradle.kts
        └── 소스
            └── 메인
                └── 코틀린
                    └── com
                        └── 예
                            └── helloworld마이크로서비스
                                └── HelloWorld.kt

### 종속성 추가

다음으로 `build.gradle.kts` 파일에 다음 종속 항목을 추가합니다.

```kotlin
plugins {
    kotlin("plugin.spring") version "1.3.72"
}

repositories {
    mavenCentral()
}

dependencies {
    implementation("org.springframework.boot:spring-boot-starter-web:2.3.3.RELEASE")
    implementation("org.jetbrains.kotlin:kotlin-reflect:1.3.72")
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.3.72")
    testImplementation("org.springframework.boot:spring-boot-starter-test:2.3.3.RELEASE") {
        exclude(group = "org.junit.vintage", module = "junit-vintage-engine")
    }
}
```

`kotlin-spring` 플러그인은 Spring Framework에 대한 지원을 Kotlin에 추가합니다. `spring-boot-starter-web` 종속성은 Spring MVC를 사용하여 웹 애플리케이션을 빌드하기 위한 지원을 추가합니다. `kotlin-reflect` 및 `kotlin-stdlib-jdk8` 종속성은 Kotlin에 리플렉션 및 Java 8 표준 라이브러리에 대한 지원을 추가합니다. `spring-boot-starter-test` 종속성은 Spring 애플리케이션 테스트에 대한 지원을 추가합니다.

### 서비스 만들기

다음으로 마이크로 서비스를 나타내는 Kotlin 클래스를 만듭니다. 클래스 이름을 `HelloWorldService`로 지정하고 `@Service` 주석으로 주석을 추가합니다.

```kotlin
@Service
class HelloWorldService {

    fun sayHello(): String {
        return "Hello, world!"
    }

}
```

`@Service` 주석은 클래스를 Spring Bean으로 표시하는 데 사용됩니다. Spring Bean은 Spring Framework에 의해 관리되며 다른 Spring Bean에 삽입될 수 있습니다.

### 컨트롤러 만들기

다음으로 마이크로 서비스의 HTTP API를 나타내는 Kotlin 클래스를 만듭니다. 클래스 이름을 `HelloWorldController`로 지정하고 `@RestController` 주석으로 주석을 추가합니다.

```kotlin
@RestController
class HelloWorldController(
    private val helloWorldService: HelloWorldService
) {

    @GetMapping("/hello")
    fun sayHello(): String {
        return helloWorldService.sayHello()
    }

}
```

`@RestController` 주석은 클래스를 Spring MVC 컨트롤러로 표시하는 데 사용됩니다. Spring MVC 컨트롤러는 HTTP 요청 처리 및 응답 반환을 담당합니다.

`HelloWorldController` 클래스에는 `@GetMapping` 주석이 달린 단일 `sayHello()` 메서드가 있습니다. 이 주석은 `sayHello()` 메서드를 `/hello` HTTP 끝점에 매핑합니다.

### 메인 클래스 만들기

마지막으로 마이크로서비스의 진입점을 나타내는 Kotlin 클래스를 만듭니다. 클래스 이름을 `HelloWorldApplication`으로 지정하고 `@SpringBootApplication` 주석으로 주석을 추가합니다.

```kotlin
@SpringBootApplication
class HelloWorldApplication

fun main(args: Array<String>) {
    runApplication<HelloWorldApplication>(*args)
}
```

`@SpringBootApplication` 주석은 클래스를 Spring Boot 애플리케이션으로 표시하는 데 사용됩니다. Spring Boot 애플리케이션은 `java -jar` 명령을 사용하여 실행할 수 있습니다.

## Kotlin 마이크로서비스 배포

이 섹션에서는 Kotlin 마이크로서비스를 서버에 배포하는 방법을 살펴보겠습니다. 먼저 Kotlin 마이크로서비스를 배포하는 데 사용할 수 있는 다양한 유형의 서버를 살펴보겠습니다. 그런 다음 Kotlin 마이크로서비스를 Heroku dyno에 배포하는 방법을 살펴보겠습니다.

### 서버 유형

Kotlin 마이크로서비스를 배포하는 데 사용할 수 있는 다양한 유형의 서버가 있습니다. 가장 일반적인 유형의 서버는 회사에서 소유하고 운영하는 물리적 서버인 전용 서버입니다. 전용 서버는 비용이 많이 들 수 있으며 일반적으로 대규모 조직에서 사용합니다.

또 다른 유형의 서버는 VPS(가상 사설 서버)로, 공유 물리적 서버에서 호스팅되는 서버입니다. VPS는 전용 서버보다 저렴할 수 있으며 일반적으로 중소 규모의 조직에서 사용됩니다.

마지막으로 클라우드 컴퓨팅 플랫폼에서 호스팅되는 서버인 클라우드 기반 서버가 있습니다. 클라우드 기반 서버는 전용 및 VPS 서버보다 저렴할 수 있으며 일반적으로 소규모 조직에서 사용됩니다.

### Heroku에 배포

Heroku는 애호가를 위한 프리 티어와 비즈니스를 위한 유료 티어를 제공하는 클라우드 컴퓨팅 플랫폼입니다. Heroku를 사용하면 Kotlin 마이크로서비스를 쉽게 배포, 확장 및 관리할 수 있습니다.

Kotlin 마이크로서비스를 Heroku에 배포하려면 먼저 새 Heroku 계정을 만들고 Heroku CLI를 설치해야 합니다. 이 작업을 완료하면 새 Heroku 앱을 만들고 Kotlin 마이크로서비스를 여기에 푸시할 수 있습니다.

    $ 헤로쿠 생성
    $ git push 헤로쿠 마스터

## 결론

이 기사에서는 Kotlin 마이크로서비스를 구축하고 배포하는 방법을 살펴보았습니다. 우리는 마이크로서비스가 어떻게 모듈성을 향상시킬 수 있는지, 그리고 어떻게 다양한 유형의 서버에 배포할 수 있는지 살펴보았습니다.