---
title: 029: Apache Camel에서 Spring Boot 사용
description: 
published: true
date: 2023-02-03T21:32:17.182Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:32:15.345Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [029: Using Spring Boot with Apache Camel***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}


# Apache Camel과 함께 Spring Boot 사용

Camel 2.0 릴리스와 함께 Spring Framework에서 Camel을 더 쉽게 사용할 수 있도록 새로운 주석 세트가 도입되었습니다. 이번 포스트에서는 Spring Boot를 Camel과 함께 사용하는 방법에 대해 알아보겠습니다.

HTTP 요청을 로그로 라우팅하는 간단한 예제부터 시작하겠습니다. 먼저 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>2.22.0</version>
</dependency>
```

이제 Camel을 설정하는 `@Configuration` 클래스를 만들 수 있습니다.

```java
@Configuration
public class MyRouteBuilder extends RouteBuilder {

    @Override
    public void configure() {
        from("jetty:http://0.0.0.0:8080/myapp")
            .to("log:requests");
    }
}
```

마지막으로 Jetty 서버를 구성하려면 `application.properties` 파일이 필요합니다.

```properties
server.port=8080
```

그게 다야! 이제 응용 프로그램을 실행하고 브라우저 또는 `curl`로 `http://localhost:8080/myapp`을 누를 수 있습니다. 콘솔에 기록된 요청이 표시되어야 합니다.

물론 이 예제는 매우 간단합니다. Camel은 더 복잡한 애플리케이션을 구축하는 데 사용할 수 있는 수많은 구성 요소를 제공합니다. Camel을 Spring Boot와 함께 사용하는 방법에 대한 자세한 내용은 [문서](http://camel.apache.org/spring-boot.html)를 확인하세요.