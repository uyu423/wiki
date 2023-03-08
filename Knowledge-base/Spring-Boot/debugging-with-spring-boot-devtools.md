---
title: Spring Boot DevTools로 디버깅
description: 
published: true
date: 2023-02-07T02:32:31.394Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:32:29.838Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Debugging with Spring Boot DevTools***English** document is available*](/en/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}


# Spring Boot DevTools로 디버깅하기

Spring Boot에는 개발자가 애플리케이션을 사용하는 데 도움이 되는 여러 가지 뛰어난 기능이 포함되어 있습니다. DevTools는 이러한 기능 중 하나입니다. 디버깅, 다시 로드 등에 도움이 될 수 있습니다.

## DevTools란 무엇인가요?

DevTools는 개발에 도움이 되는 도구 세트입니다. 서버를 다시 시작하지 않고 애플리케이션을 다시 로드하고 파일이 변경되면 서버를 자동으로 다시 시작하는 등의 작업을 수행할 수 있습니다. 또한 IDE에서 애플리케이션을 디버깅할 수 있도록 하여 디버깅에 도움이 될 수 있습니다.

## DevTools 설정

DevTools를 사용하려면 프로젝트에 추가해야 합니다. 종속 항목에 추가하여 이 작업을 수행할 수 있습니다. 예를 들어 Maven에서는 `pom.xml`에 추가합니다.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
    </dependency>
</dependencies>
```

또는 Gradle을 사용하는 경우 `build.gradle`에 추가합니다.

```groovy
dependencies {
    compile 'org.springframework.boot:spring-boot-devtools'
}
```

## DevTools 사용

프로젝트에 DevTools가 구성되면 사용을 시작할 수 있습니다.

### 애플리케이션 다시 로드

DevTools의 가장 유용한 기능 중 하나는 서버를 다시 시작하지 않고 애플리케이션을 다시 로드하는 기능입니다. 이렇게 하려면 IDE에서 `Ctrl+F9`(또는 macOS의 경우 `Cmd+F9`)를 누르기만 하면 됩니다. 이렇게 하면 애플리케이션이 완전히 다시 시작됩니다.

서버만 다시 시작하려면 `Ctrl+Shift+F9`(또는 macOS의 경우 `Cmd+Shift+F9`)를 누르십시오. 이렇게 하면 응용 프로그램이 아닌 서버만 다시 시작됩니다.

### 애플리케이션 디버깅

DevTools의 또 다른 유용한 기능은 IDE에서 애플리케이션을 디버깅하는 기능입니다. 이렇게 하려면 디버그 모드에서 애플리케이션을 시작해야 합니다. `--debug` 플래그를 `spring-boot` CLI에 전달하여 이를 수행할 수 있습니다.

```
$ spring-boot --debug
```

또는 `application.properties`에서 `spring.boot.debug` 속성을 설정할 수 있습니다.

```properties
spring.boot.debug=true
```

애플리케이션이 디버그 모드에서 실행되면 디버거를 연결할 수 있습니다. 예를 들어 IntelliJ IDEA에서는 `실행 > 로컬 프로세스에 디버거 연결`로 이동하여 이 작업을 수행할 수 있습니다.

## 결론

DevTools는 개발에 도움이 되는 훌륭한 도구입니다. 서버를 다시 시작하지 않고 애플리케이션을 다시 로드하고 파일이 변경되면 서버를 자동으로 다시 시작하는 등의 작업을 수행할 수 있습니다. 또한 IDE에서 애플리케이션을 디버깅할 수 있도록 하여 디버깅에 도움이 될 수 있습니다.