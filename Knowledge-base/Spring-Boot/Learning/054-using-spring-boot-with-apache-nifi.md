---
title: 054: Apache Nifi와 함께 Spring Boot 사용
description: 
published: true
date: 2023-02-03T01:23:38.949Z
tags: 
editor: markdown
dateCreated: 2023-02-03T01:23:37.385Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [054: Using Spring Boot with Apache Nifi***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/054-using-spring-boot-with-apache-nifi)
{.links-list}


# Apache Nifi와 함께 스프링 부트 사용

Spring Boot는 마이크로서비스를 생성하는 데 사용되는 널리 사용되는 Java 기반 프레임워크입니다. Apache NiFi는 데이터를 처리하고 라우팅하는 데 사용할 수 있는 강력한 데이터 흐름 도구입니다.

이 게시물에서는 Apache NiFi와 함께 Spring Boot를 사용하는 방법을 보여줍니다. 다음 주제를 다룹니다.

* Spring Boot 프로젝트 설정
* 아파치 NiFi 구성
* Spring Boot 서비스 생성
* 데이터 흐름 테스트

## 스프링 부트 프로젝트 설정

가장 먼저 해야 할 일은 새로운 Spring Boot 프로젝트를 만드는 것입니다. [Spring Initializr](https://start.spring.io/)를 사용하여 필요한 종속성이 있는 프로젝트를 생성할 수 있습니다.

이 예에서는 다음과 같은 종속성이 필요합니다.

* 웹 - 웹 애플리케이션 생성용
* H2 - 메모리 내 데이터베이스용

프로젝트가 설정되면 Apache NiFi 구성을 시작할 수 있습니다.

## Apache NiFi 구성

생성할 Spring Boot 서비스를 사용하려면 Apache NiFi를 구성해야 합니다. NiFi 구성에 다음을 추가해야 합니다.

* Spring Boot 서비스를 호출하기 위한 프로세서
* 프로세서를 위한 연결 풀
* 연결 풀에 대한 컨트롤러 서비스

NiFi GUI를 사용하여 이러한 설정을 구성할 수 있습니다. 먼저 프로세서를 추가합니다.

![프로세서 추가](https://i.imgur.com/Lb6qyFW.png)

다음으로 연결 풀을 추가합니다.

![연결 풀 추가](https://i.imgur.com/vH8X3zJ.png)

마지막으로 컨트롤러 서비스를 추가합니다.

![컨트롤러 서비스 추가](https://i.imgur.com/g4SVfyi.png)

## 스프링 부트 서비스 생성

이제 Apache NiFi가 구성되었으므로 Spring Boot 서비스를 만들 수 있습니다. 서비스는 REST 엔드포인트를 노출하는 간단한 웹 애플리케이션입니다.

엔드포인트는 JSON 페이로드를 받아 응답을 반환합니다. 응답은 생성된 ID가 있는 동일한 JSON 페이로드입니다.

서비스 코드는 다음과 같습니다.

```java
@RestController
public class DataController {

    @PostMapping("/data")
    public ResponseEntity<String> data(@RequestBody String data) {
        // Generate ID
        String id = UUID.randomUUID().toString();
        // Return response
        return ResponseEntity.ok().body(id);
    }
}
```

## 데이터 흐름 테스트

이제 서비스가 실행 중이므로 데이터 흐름을 테스트할 수 있습니다. NiFi GUI를 사용하여 JSON 페이로드를 엔드포인트로 보냅니다.

먼저 새 FlowFile을 만듭니다.

![FlowFile 만들기](https://i.imgur.com/TGiukC5.png)

다음으로 JSON 페이로드를 추가합니다.

![JSON 페이로드 추가](https://i.imgur.com/l0v4tqO.png)

마지막으로 프로세서를 트리거하고 응답을 확인합니다.

![트리거 프로세서](https://i.imgur.com/JY4fZUO.png)

![응답 확인](https://i.imgur.com/5AFw8gG.png)

보시다시피 응답에는 생성된 ID가 포함되어 있습니다.

## 결론

이 게시물에서는 Apache NiFi와 함께 Spring Boot를 사용하는 방법을 보여주었습니다. Spring Boot 서비스를 호출하고 응답을 반환하는 간단한 데이터 흐름을 설정했습니다.

NiFi에 대해 자세히 알아보려면 [공식 문서](https://nifi.apache.org/docs.html)를 확인하세요.