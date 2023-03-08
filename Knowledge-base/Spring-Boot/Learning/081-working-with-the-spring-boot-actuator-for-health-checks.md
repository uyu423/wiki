---
title: 081: 상태 확인을 위한 Spring Boot Actuator 작업
description: 
published: true
date: 2023-02-05T12:32:18.517Z
tags: 
editor: markdown
dateCreated: 2023-02-05T12:32:16.945Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [081: Working with the Spring Boot Actuator for Health Checks***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/081-working-with-the-spring-boot-actuator-for-health-checks)
{.links-list}


# Health Check용 Spring Boot Actuator란?

Health Checks용 Spring Boot Actuator는 개발자가 애플리케이션의 상태를 쉽게 확인할 수 있는 도구입니다. 애플리케이션 성능을 모니터링하고 잠재적인 문제를 식별하며 애플리케이션의 전반적인 상태에 대한 정보를 제공하는 데 사용할 수 있습니다.

상태 확인을 위한 Spring Boot Actuator는 Spring Boot 프레임워크에 포함된 기본 제공 도구입니다. 사용하기 쉽고 응용 프로그램의 상태에 대한 풍부한 정보를 제공합니다.

# Health Check를 위해 Spring Boot Actuator를 사용하는 이유는 무엇입니까?

상태 확인용 Spring Boot Actuator는 개발자에게 유용한 도구입니다. 애플리케이션의 잠재적인 문제를 식별하고 애플리케이션의 전반적인 상태에 대한 정보를 제공하는 데 도움이 될 수 있습니다.

상태 확인을 위한 Spring Boot Actuator는 사용하기 쉽고 풍부한 정보를 제공합니다. 애플리케이션의 상태를 모니터링하려는 개발자에게 유용한 도구입니다.

# 상태 확인을 위해 Spring Boot Actuator를 사용하는 방법

상태 확인을 위해 Spring Boot Actuator를 사용하는 것은 쉽습니다. 프로젝트에 다음 종속성을 추가하기만 하면 됩니다.

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

종속성을 추가한 후에는 application.properties 파일에 다음을 추가하여 Actuator 끝점에 액세스할 수 있습니다.

```properties
management.endpoints.web.exposure.include=health
```

그런 다음 http://localhost:8080/actuator/health에서 상태 엔드포인트에 액세스할 수 있습니다.

# 결론

상태 확인용 Spring Boot Actuator는 개발자에게 유용한 도구입니다. 사용하기 쉽고 응용 프로그램의 상태에 대한 풍부한 정보를 제공합니다. 애플리케이션의 상태를 모니터링하려는 개발자에게 유용한 도구입니다.