---
title: Kotlin 지속적 배포: 배포 프로세스 자동화
description: 
published: true
date: 2023-01-31T21:36:42.692Z
tags: 
editor: markdown
dateCreated: 2023-01-31T21:36:41.112Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin Continuous Deployment: Automating the Deployment Process***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-continuous-deployment-automating-the-deployment-process)
{.links-list}



# Kotlin 지속적 배포: 배포 프로세스 자동화

개발자는 항상 소프트웨어 개발 프로세스를 자동화하는 방법을 찾고 있습니다. 소프트웨어 개발에서 가장 중요하고 시간이 많이 걸리는 작업 중 하나는 배포입니다. 배포는 로컬 개발 환경에서 코드를 가져와 프로덕션 환경으로 푸시하는 프로세스입니다. 이 프로세스는 수동 또는 자동일 수 있습니다.

배포 프로세스를 자동화하면 많은 이점이 있습니다. 배포를 자동화하면 시간을 절약하고 일관성을 개선하며 인적 오류 가능성을 줄일 수 있습니다. 이 기사에서는 Kotlin을 사용하여 배포 프로세스를 자동화하는 방법에 중점을 둘 것입니다.

## 왜 코틀린인가?

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 Java와 100% 상호 운용 가능하므로 Java에 이미 익숙한 개발자에게 매력적인 옵션입니다. Kotlin은 또한 간결한 언어로, 더 읽기 쉽고 유지 관리가 쉬운 코드로 이어질 수 있습니다.

## Kotlin 프로젝트 설정

배포 프로세스 자동화를 시작하려면 먼저 Kotlin 프로젝트를 설정해야 합니다. 우리는 Gradle 빌드 도구를 사용하여 프로젝트 종속성을 관리하고 프로젝트를 빌드할 것입니다.

프로젝트의 루트 디렉터리에 `build.gradle.kts`라는 파일을 만들어야 합니다. `build.gradle.kts` 파일은 Gradle 빌드를 구성하는 데 사용됩니다.

```kotlin
plugins {
    id("org.jetbrains.kotlin.jvm") version "1.3.72"
}

group = "com.example"
version = "0.0.1"

repositories {
    jcenter()
}

dependencies {
    implementation("org.jetbrains.kotlin:kotlin-stdlib-jdk8")
}

tasks.withType<org.jetbrains.kotlin.gradle.tasks.KotlinCompile> {
    kotlinOptions.jvmTarget = "1.8"
}
```

`build.gradle.kts` 파일은 `build.gradle` 파일과 유사하지만 Kotlin으로 작성되었습니다. `build.gradle.kts` 파일에서 Kotlin 프로그래밍 언어용 플러그인을 정의하고 사용할 Kotlin 버전을 지정했습니다. 또한 프로젝트의 그룹과 버전도 정의했습니다.

또한 프로젝트 종속성이 해결될 리포지토리도 정의했습니다. 이 경우 JCenter 저장소를 사용하고 있습니다. 마지막으로 Kotlin 표준 라이브러리에 대한 종속성을 정의했습니다.

Kotlin 표준 라이브러리는 Kotlin 애플리케이션 개발에 필요한 일련의 핵심 라이브러리를 제공합니다. 또한 프로젝트를 Java 8용으로 컴파일하도록 지정했습니다.

## 배포 프로세스 자동화

이제 Kotlin 프로젝트가 설정되었으므로 배포 프로세스 자동화를 시작할 수 있습니다. Gradle 빌드 도구를 사용하여 배포 프로세스를 자동화합니다.

가장 먼저 해야 할 일은 프로젝트의 루트 디렉토리에 `deploy.gradle`이라는 파일을 만드는 것입니다. `deploy.gradle` 파일에는 배포 프로세스에 대한 구성이 포함되어 있습니다.

```kotlin
plugins {
    id("com.bmuschko.gradle.plugins.tooling-api") version "2.3.3"
}

apply(plugin = "com.bmuschko.tomcat")

group = "com.example"
version = "0.0.1"

repositories {
    jcenter()
}

dependencies {
    tomcat "org.apache.tomcat.embed:tomcat-embed-core:9.0.33"
    tomcat "org.apache.tomcat.embed:tomcat-embed-logging-juli:9.0.33"
    tomcat "org.apache.tomcat.embed:tomcat-embed-jasper:9.0.33"
}

tomcat {
    httpPort = 8080
    ajpPort = 8009
    enableSSL = false
    keystoreFile = file("src/main/resources/keystore.jks")
    keystorePass = "secret"
    keyAlias = "tomcat"
}

tasks.withType<org.jetbrains.kotlin.gradle.tasks.KotlinCompile> {
    kotlinOptions.jvmTarget = "1.8"
}
```

`deploy.gradle` 파일에서 Tomcat 웹 서버용 플러그인을 정의했습니다. 또한 프로젝트의 그룹과 버전도 지정했습니다.

또한 프로젝트 종속성이 해결될 리포지토리도 정의했습니다. 이 경우 JCenter 저장소를 사용하고 있습니다. 마지막으로 Tomcat 라이브러리에 대한 종속성을 정의했습니다.

Tomcat 라이브러리는 Kotlin 애플리케이션을 Tomcat 웹 서버에 배포하는 데 필요합니다. Tomcat이 HTTP 요청을 수신하는 데 사용해야 하는 포트도 지정했습니다.

Tomcat이 AJP 요청을 수신하는 데 사용해야 하는 포트도 지정했습니다. AJP는 웹 서버와 애플리케이션 서버 간의 통신에 사용되는 프로토콜입니다. 또한 애플리케이션에서 SSL을 사용하지 않도록 지정했습니다.

마지막으로 키 저장소 파일의 위치와 키 저장소의 암호를 지정했습니다. 키 저장소는 데이터를 암호화하고 해독하는 데 사용되는 암호화 키가 포함된 파일입니다.

## 애플리케이션 배포

이제 배포 프로세스가 자동화되었으므로 애플리케이션을 배포할 수 있습니다. Gradle Tomcat 플러그인을 사용하여 애플리케이션을 배포합니다.

애플리케이션을 배포하려면 `gradle tomcatRun` 명령을 실행해야 합니다. 이 명령은 Tomcat 웹 서버를 시작하고 여기에 애플리케이션을 배포합니다.

Tomcat 웹 서버가 실행되면 `http://localhost:8080`에서 애플리케이션에 액세스할 수 있습니다.