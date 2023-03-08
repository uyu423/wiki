---
title: 021: Kotlin의 주석 처리: 컴파일 시 코드 생성
description: 
published: true
date: 2023-02-01T16:44:21.482Z
tags: 
editor: markdown
dateCreated: 2023-02-01T16:44:19.777Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [021: Annotation Processing in Kotlin: Generating Code at Compile Time***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/021-annotation-processing-in-kotlin-generating-code-at-compile-time)
{.links-list}


# 021: Kotlin의 주석 처리: 컴파일 시 코드 생성

Kotlin은 JVM에서 실행되는 정적 유형 프로그래밍 언어입니다. Java와 완벽하게 상호 운용 가능하며 Android 앱을 개발하는 데 사용할 수 있습니다. Kotlin은 또한 주석 처리를 훌륭하게 지원합니다.

주석 처리는 컴파일 타임에 코드를 생성하는 방법입니다. 프로그래밍 언어의 소스 코드에서 쉽게 표현할 수 없는 코드를 만드는 데 자주 사용됩니다. 예를 들어 주석 처리를 사용하여 데이터 바인딩용 코드를 생성하거나 Android Parcelables를 생성하거나 Dagger 2용 코드를 생성할 수 있습니다.

이 기사에서는 Kotlin에서 주석 처리를 사용하여 간단한 데이터 바인딩 라이브러리용 코드를 생성하는 방법을 살펴보겠습니다. 주석 처리를 위해 kotlin-apt 플러그인을 사용하는 방법도 살펴보겠습니다.

## 주석 처리란?

주석 처리는 컴파일 타임에 코드를 생성하는 방법입니다. 주석 프로세서는 프로그램의 소스 코드를 읽고 소스 코드에 있는 주석을 기반으로 코드를 생성하는 프로그램입니다.

주석은 프로그램에 메타데이터를 추가하는 방법입니다. Kotlin에서 주석은 `@` 기호를 사용하여 프로그램에 추가됩니다. 예를 들어, `@Override` 주석은 슈퍼클래스의 메서드를 재정의하는 메서드에 주석을 추가하는 데 사용할 수 있습니다.

 주석을 사용하여 클래스에 메타데이터를 추가할 수도 있습니다. Kotlin에서는 클래스에 '@Deprecated' 주석을 추가하여 해당 클래스가 더 이상 사용되지 않으며 사용해서는 안 됨을 나타낼 수 있습니다.

주석을 사용하여 패키지에 메타데이터를 추가할 수도 있습니다. Kotlin에서는 패키지에 `@file:JvmName` 주석을 추가하여 패키지를 지정된 이름의 Java 클래스로 컴파일해야 함을 나타낼 수 있습니다.

주석을 사용하여 파일에 메타데이터를 추가할 수도 있습니다. Kotlin에서는 파일에 `@file:Suppress("unused")` 주석을 추가하여 컴파일러가 파일에서 사용되지 않는 변수에 대한 경고를 생성하지 않아야 함을 나타낼 수 있습니다.

## Kotlin에서 주석 처리를 사용하는 방법

주석 처리는 컴파일 타임에 코드를 생성하는 방법입니다. Kotlin에서 주석 처리는 kotlin-apt 플러그인을 사용하여 수행됩니다. kotlin-apt 플러그인은 주석 처리 지원을 추가하는 Kotlin 컴파일러 플러그인입니다.

kotlin-apt 플러그인을 사용하려면 `build.gradle` 파일에 다음을 추가해야 합니다.

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

kotlin-apt 플러그인은 `build.gradle` 파일에 `apt` 구성을 추가합니다. 'apt' 구성은 사용될 주석 프로세서를 구성하는 데 사용됩니다. 위의 예에서 `auto-service` 주석 프로세서가 구성되었습니다.

`auto-service` 주석 프로세서는 `@AutoService` 주석에 대한 코드를 생성하는 데 사용됩니다. `@AutoService` 주석은 `auto-service` 공급자에 등록해야 하는 클래스에 주석을 추가하는 데 사용됩니다.

`auto-service` 공급자는 `@AutoService` 주석이 달린 클래스 목록을 제공하는 서비스입니다. 'auto-service' 제공자는 서비스 제공자 인터페이스(SPI)용 코드를 생성하는 데 사용할 수 있습니다.

위의 예에서 `@AutoService` 주석은 `auto-service` 공급자에 등록해야 하는 클래스에 주석을 추가하는 데 사용됩니다. `auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스에 대한 코드를 생성합니다.

`com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 클래스를 등록하는 데 사용되는 SPI입니다. `auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스를 사용하여 `META-INF/services/` 파일용 코드를 생성합니다.

`META-INF/services/` 파일은 `auto-service` 공급자에 등록된 클래스 목록을 저장하는 데 사용됩니다. `META-INF/services/` 파일은 `java.util.ServiceLoader`에서 서비스 제공자로부터 클래스를 로드하는 데 사용됩니다.

위의 예에서 `META-INF/services/` 파일에는 다음이 포함됩니다.

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader`는 `META-INF/services/` 파일을 사용하여 `com.example.MyClass` 클래스를 로드합니다. `com.example.MyClass` 클래스는 `auto-service` 공급자에 등록됩니다.

`auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스에 대한 코드를 생성합니다. `com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 클래스를 등록하는 데 사용됩니다.

위의 예에서 `com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 `com.example.MyClass` 클래스를 등록하는 데 사용됩니다. `자동 서비스` 공급자는 `META-INF/services/` 파일에 대한 코드를 생성합니다.

`META-INF/services/` 파일은 `auto-service` 공급자에 등록된 클래스 목록을 저장하는 데 사용됩니다. `META-INF/services/` 파일은 `java.util.ServiceLoader`에서 서비스 제공자로부터 클래스를 로드하는 데 사용됩니다.

위의 예에서 `META-INF/services/` 파일에는 다음이 포함됩니다.

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader`는 `META-INF/services/` 파일을 사용하여 `com.example.MyClass` 클래스를 로드합니다. `com.example.MyClass` 클래스는 `auto-service` 공급자에 등록됩니다.

## 결론

주석 처리는 컴파일 타임에 코드를 생성하는 방법입니다. Kotlin에서 주석 처리는 kotlin-apt 플러그인을 사용하여 수행됩니다. kotlin-apt 플러그인은 주석 처리 지원을 추가하는 Kotlin 컴파일러 플러그인입니다.

kotlin-apt 플러그인은 `build.gradle` 파일에 `apt` 구성을 추가합니다. 'apt' 구성은 사용될 주석 프로세서를 구성하는 데 사용됩니다. 위의 예에서 `auto-service` 주석 프로세서가 구성되었습니다.

`auto-service` 주석 프로세서는 `@AutoService` 주석에 대한 코드를 생성하는 데 사용됩니다. `@AutoService` 주석은 `auto-service` 공급자에 등록해야 하는 클래스에 주석을 추가하는 데 사용됩니다.

`auto-service` 공급자는 `@AutoService` 주석이 달린 클래스 목록을 제공하는 서비스입니다. 'auto-service' 제공자는 서비스 제공자 인터페이스(SPI)용 코드를 생성하는 데 사용할 수 있습니다.

위의 예에서 `@AutoService` 주석은 `auto-service` 공급자에 등록해야 하는 클래스에 주석을 추가하는 데 사용됩니다. `auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스에 대한 코드를 생성합니다.

`com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 클래스를 등록하는 데 사용되는 SPI입니다. `auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스를 사용하여 `META-INF/services/` 파일용 코드를 생성합니다.

`META-INF/services/` 파일은 `auto-service` 공급자에 등록된 클래스 목록을 저장하는 데 사용됩니다. `META-INF/services/` 파일은 `java.util.ServiceLoader`에서 서비스 제공자로부터 클래스를 로드하는 데 사용됩니다.

위의 예에서 `META-INF/services/` 파일에는 다음이 포함됩니다.

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader`는 `META-INF/services/` 파일을 사용하여 `com.example.MyClass` 클래스를 로드합니다. `com.example.MyClass` 클래스는 `auto-service` 공급자에 등록됩니다.

`auto-service` 공급자는 `com.google.auto.service.AutoService` 인터페이스에 대한 코드를 생성합니다. `com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 클래스를 등록하는 데 사용됩니다.

위의 예에서 `com.google.auto.service.AutoService` 인터페이스는 `auto-service` 공급자에 `com.example.MyClass` 클래스를 등록하는 데 사용됩니다. `자동 서비스` 공급자는 `META-INF/services/` 파일에 대한 코드를 생성합니다.

`META-INF/services/` 파일은 `auto-service` 공급자에 등록된 클래스 목록을 저장하는 데 사용됩니다. `META-INF/services/` 파일은 `java.util.ServiceLoader`에서 서비스 제공자로부터 클래스를 로드하는 데 사용됩니다.

위의 예에서 `META-INF/services/` 파일에는 다음이 포함됩니다.

```
com.google.auto.service.AutoService
com.example.MyClass
```

`java.util.ServiceLoader`는 `META-INF/services/` 파일을 사용하여 `com.example.MyClass` 클래스를 로드합니다. `com.example.MyClass` 클래스는 `auto-service` 공급자에 등록됩니다.