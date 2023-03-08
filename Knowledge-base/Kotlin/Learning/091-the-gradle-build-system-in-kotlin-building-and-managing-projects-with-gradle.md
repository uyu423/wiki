---
title: 091: Kotlin의 Gradle 빌드 시스템: Gradle로 프로젝트 빌드 및 관리
description: 
published: true
date: 2023-02-17T21:06:36.038Z
tags: 
editor: markdown
dateCreated: 2023-02-17T21:06:34.668Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [091: The Gradle Build System in Kotlin: Building and Managing Projects with Gradle***English** document is available*](/en/Knowledge-base/Kotlin/Learning/091-the-gradle-build-system-in-kotlin-building-and-managing-projects-with-gradle)
{.links-list}


# 091: Kotlin의 Gradle 빌드 시스템: Gradle로 프로젝트 빌드 및 관리

Gradle은 모든 규모의 프로젝트를 빌드하고 관리할 수 있는 Kotlin으로 작성된 빌드 시스템입니다. 개발자 커뮤니티에서 적극적으로 유지 관리하는 오픈 소스 프로젝트입니다.

## 왜 Gradle을 사용하나요?

Gradle을 빌드 시스템으로 사용하는 데는 여러 가지 이유가 있습니다. Gradle은 유연하고 확장 가능하도록 설계되었습니다. 빌드에 새로운 기능을 추가할 수 있는 풍부한 플러그인 생태계가 있습니다. Gradle은 Apache Maven과 같은 다른 빌드 시스템보다 훨씬 빠릅니다.

## 시작하기

Gradle을 시작하려면 프로젝트의 루트 디렉터리에 `build.gradle` 파일을 만들어야 합니다. 이 파일은 프로젝트의 빌드 구성을 정의합니다.

```groovy
apply plugin: 'java'

repositories {
    jcenter()
}

dependencies {
    compile group: 'org.apache.commons', name: 'commons-lang3', version: '3.5'
}
```

`apply plugin: 'java'` 행은 Java 플러그인을 프로젝트에 적용합니다. 이 플러그인은 Java 코드를 컴파일하고 JAR 파일로 패키징하기 위한 지원을 추가합니다.

`repositories` 블록은 Gradle이 종속성을 찾아야 하는 위치를 정의합니다. 이 예에서는 JCenter 저장소를 사용하고 있습니다.

`dependencies` 블록은 프로젝트의 종속성을 정의합니다. 우리는 Apache Commons Lang 라이브러리에 의존하고 있습니다.

프로젝트를 빌드하기 위해 `gradle build` 명령을 실행할 수 있습니다. 그러면 Java 코드가 컴파일되고 JAR 파일로 패키징됩니다. JAR 파일은 `build/libs` 디렉토리에 배치됩니다.

## 래퍼

Gradle은 Gradle을 시스템에 설치하지 않고 실행할 수 있는 래퍼를 제공합니다. 래퍼는 프로젝트와 함께 제공되는 Gradle 스크립트입니다. 래퍼를 사용하려면 `build.gradle` 파일에 다음을 추가해야 합니다.

```groovy
apply plugin: 'java'

task wrapper(type: Wrapper) {
    gradleVersion = '2.9'
}
```

`wrapper` 작업은 Gradle 래퍼 스크립트(`gradlew`)와 속성 파일(`gradle/wrapper/gradle-wrapper.properties`)을 생성합니다. 이러한 파일은 버전 관리 시스템에 추가해야 합니다.

래퍼를 사용하여 프로젝트를 빌드하려면 `gradlew build` 명령을 실행할 수 있습니다.

## 작업

Gradle 작업은 코드 컴파일, 테스트 실행 또는 애플리케이션 패키징과 같은 작업을 수행하는 데 사용됩니다. 작업에는 이름과 유형이 있습니다. 작업 이름은 작업을 식별하는 데 사용되며 유형은 작업이 수행할 작업을 정의합니다.

다음 예제에는 `JavaCompile` 유형의 `compile`이라는 작업이 있습니다. 이 작업은 `src/main/java` 디렉토리에서 Java 코드를 컴파일합니다.

```groovy
task compile(type: JavaCompile) {
    source = sourceSets.main.java
    classpath = configurations.compile
}
```

작업은 다른 작업에 종속될 수도 있습니다. 다음 예에서 `compile` 작업은 `classes` 작업에 종속됩니다. 이는 `classes` 작업이 `compile` 작업 전에 실행됨을 의미합니다.

```groovy
task compile(type: JavaCompile) {
    dependsOn 'classes'
    source = sourceSets.main.java
    classpath = configurations.compile
}
```

## 플러그인

Gradle 플러그인은 Gradle의 기능을 확장하는 데 사용됩니다. 다양한 언어와 도구에 사용할 수 있는 많은 플러그인이 있습니다. 다음 예제에서는 `java` 플러그인을 사용하여 Java 코드 컴파일 지원을 추가합니다.

```groovy
apply plugin: 'java'

repositories {
    jcenter()
}

dependencies {
    compile group: 'org.apache.commons', name: 'commons-lang3', version: '3.5'
}
```

플러그인을 적용하려면 `apply plugin: 'name'` 구문을 사용합니다. 위의 예에서는 `java` 플러그인을 적용하고 있습니다.

## 결론

이 게시물에서는 Gradle을 사용하여 프로젝트를 빌드하고 관리하는 기본 사항을 다뤘습니다. Gradle은 빠르고 유연하며 확장 가능한 강력한 빌드 시스템입니다. 빌드에 새로운 기능을 추가할 수 있는 풍부한 플러그인 생태계가 있습니다.