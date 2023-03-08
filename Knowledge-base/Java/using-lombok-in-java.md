---
title: 자바에서 롬복 사용하기
description: 
published: true
date: 2023-01-31T09:05:37.446Z
tags: 
editor: markdown
dateCreated: 2023-01-31T09:05:35.712Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Using Lombok in Java***English** version of this document is available*](/en/Knowledge-base/Java/using-lombok-in-java)
{.links-list}




# 자바에서 롬복 사용하기

Lombok은 Java에서 상용구 코드를 줄이는 데 사용할 수 있는 라이브러리입니다. getter, setter, toString, hashCode 및 equals 메서드와 생성자를 자동으로 생성하는 데 사용됩니다. Lombok은 오픈 소스이며 MIT 라이선스에 따라 사용할 수 있습니다.

# # 설치

Lombok은 IDE에 플러그인으로 설치하거나 프로젝트 빌드 경로에 추가할 수 있습니다.

## # IDE 플러그인

### # 이클립스

Eclipse에 사용할 수 있는 Lombok 플러그인이 있습니다. 설치하려면 Eclipse를 시작하고 도움말 > Eclipse Marketplace로 이동하십시오. Lombok을 검색하고 플러그인을 설치합니다.

### # IntelliJ IDEA

IntelliJ IDEA에 사용할 수 있는 Lombok 플러그인이 있습니다. 설치하려면 IntelliJ IDEA를 시작하고 파일 > 설정으로 이동합니다. 설정 창에서 플러그인으로 이동하여 리포지토리 찾아보기를 클릭합니다. Lombok을 검색하고 플러그인을 설치합니다.

## # 빌드 경로

Maven으로 빌드할 프로젝트에서 Lombok을 사용하는 경우 pom.xml 파일에 다음 종속성을 추가하여 프로젝트 빌드 경로에 Lombok을 추가할 수 있습니다.

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.16.20</version>
    <scope>provided</scope>
</dependency>
```

Gradle로 빌드할 프로젝트에서 Lombok을 사용하는 경우 build.gradle 파일에 다음 종속성을 추가하여 프로젝트 빌드 경로에 Lombok을 추가할 수 있습니다.

```groovy
dependencies {
    compileOnly 'org.projectlombok:lombok:1.16.20'
}
```

# # 용법

Java 코드에서 Lombok을 사용하려면 getter, setter 및 생성자를 생성하려는 필드에 주석을 달아야 합니다. 예를 들어:

```java
import lombok.Data;

@Data
public class Person {
    private String name;
    private int age;
}
```

@Data 주석은 Person 클래스의 모든 필드에 대해 getter, setter 및 생성자를 생성합니다.

필드에 대한 getter 및 setter만 생성하려는 경우 @Getter 및 @Setter 주석을 사용할 수 있습니다.

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

클래스에 대한 생성자만 생성하려는 경우 @RequiredArgsConstructor 주석을 사용할 수 있습니다.

```java
import lombok.RequiredArgsConstructor;

@RequiredArgsConstructor
public class Person {
    private final String name;
    private final int age;
}
```

@RequiredArgsConstructor 주석은 최종으로 표시되거나 @NonNull 주석이 있는 모든 필드에 대한 매개변수가 있는 생성자를 생성합니다.

클래스에 대한 toString 메서드를 생성하려면 @ToString 주석을 사용할 수 있습니다.

```java
import lombok.ToString;

@ToString
public class Person {
    private String name;
    private int age;
}
```

클래스에 대한 hashCode 메서드를 생성하려면 @HashCode 주석을 사용할 수 있습니다.

```java
import lombok.HashCode;

@HashCode
public class Person {
    private String name;
    private int age;
}
```

클래스에 대해 equals 메서드를 생성하려면 @EqualsAndHashCode 주석을 사용할 수 있습니다.

```java
import lombok.EqualsAndHashCode;

@EqualsAndHashCode
public class Person {
    private String name;
    private int age;
}
```

# # 장점과 단점

Lombok은 Java에서 상용구 코드를 줄이는 데 도움이 되는 매우 유용한 도구입니다. 그러나 Lombok 사용에는 몇 가지 잠재적인 단점이 있습니다.

첫째, Lombok은 소스 코드에 보이지 않는 코드를 생성합니다. 이로 인해 생성된 코드에서 발생하는 문제를 디버깅하기 어려울 수 있습니다.

둘째, Lombok은 코드를 읽기 어렵게 만들 수 있습니다. 예를 들어 @Data 주석은 소스 코드를 이해하기 더 어렵게 만들 수 있는 많은 코드를 생성합니다.

셋째, Lombok은 코드 검사 도구와 같은 특정 Java 도구를 사용하기 어렵게 만들 수 있습니다. 이는 Lombok 생성 코드가 소스 코드에 표시되지 않기 때문입니다.

넷째, Lombok은 코드를 새 버전의 Java로 마이그레이션하기 어렵게 만들 수 있습니다. 이는 Lombok 생성 코드가 컴파일된 Java 버전에 따라 다르기 때문입니다.

마지막으로 Lombok은 널리 사용되지 않습니다. 이는 Lombok에 사용할 수 있는 문서 및 지원이 적다는 것을 의미합니다.

# # 결론

Lombok은 Java에서 상용구 코드를 줄이는 데 사용할 수 있는 라이브러리입니다. getter, setter, toString, hashCode 및 equals 메서드와 생성자를 자동으로 생성하는 데 사용됩니다. Lombok은 오픈 소스이며 MIT 라이선스에 따라 사용할 수 있습니다.

Lombok은 Java에서 상용구 코드를 줄이는 데 도움이 되는 매우 유용한 도구입니다. 그러나 Lombok 사용에는 몇 가지 잠재적인 단점이 있습니다. 첫째, Lombok은 소스 코드에 보이지 않는 코드를 생성합니다. 이로 인해 생성된 코드에서 발생하는 문제를 디버깅하기 어려울 수 있습니다. 둘째, Lombok은 코드를 읽기 어렵게 만들 수 있습니다. 예를 들어 @Data 주석은 소스 코드를 이해하기 더 어렵게 만들 수 있는 많은 코드를 생성합니다. 셋째, Lombok은 코드 검사 도구와 같은 특정 Java 도구를 사용하기 어렵게 만들 수 있습니다. 이는 Lombok 생성 코드가 소스 코드에 표시되지 않기 때문입니다. 넷째, Lombok은 코드를 새 버전의 Java로 마이그레이션하기 어렵게 만들 수 있습니다. 이는 Lombok 생성 코드가 컴파일된 Java 버전에 따라 다르기 때문입니다. 마지막으로 Lombok은 널리 사용되지 않습니다. 이는 Lombok에 사용할 수 있는 문서 및 지원이 적다는 것을 의미합니다.