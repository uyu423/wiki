---
title: 액추에이터를 사용한 스프링 부트 모니터링
description: 
published: true
date: 2023-02-07T15:33:16.630Z
tags: 
editor: markdown
dateCreated: 2023-02-07T15:33:14.971Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Monitoring with Actuator***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}


# 액츄에이터를 이용한 스프링부트 모니터링

프로덕션 Spring Boot 애플리케이션에서는 발생할 수 있는 모든 문제를 식별하고 진단할 수 있도록 애플리케이션을 모니터링할 수 있어야 합니다. Spring Boot는 액추에이터를 포함하여 이를 돕기 위해 즉시 사용 가능한 여러 기능을 제공합니다.

Actuator는 Spring Boot 애플리케이션을 모니터링하고 관리할 수 있는 도구입니다. 코드를 작성하지 않고도 애플리케이션을 모니터링하고 관리할 수 있는 여러 엔드포인트를 제공합니다.

이 기사에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하는 방법을 살펴보겠습니다. 또한 액추에이터를 사용하여 애플리케이션별 정보를 노출하는 사용자 지정 끝점을 만드는 방법도 살펴보겠습니다.

## 액추에이터 활성화

Actuator를 사용하려면 먼저 프로젝트에 spring-boot-starter-actuator 종속성을 추가해야 합니다. 이는 pom.xml 파일에 다음 종속성을 추가하여 수행할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

또는 Gradle을 사용하는 경우 build.gradle 파일에 다음 종속성을 추가할 수 있습니다.

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-actuator')
}
```

spring-boot-starter-actuator 종속성을 프로젝트에 추가하면 Actuator가 기본적으로 활성화됩니다. 기본적으로 Actuator는 'ADMIN' 역할을 가진 사용자만 액세스할 수 있습니다.

이를 변경하려면 application.properties 파일에 다음 속성을 추가하면 됩니다.

```properties
management.security.enabled=false
```

이렇게 하면 Actuator 끝점에 대한 보안이 비활성화됩니다. 또는 프로젝트에 spring-boot-starter-security 종속성을 추가하여 액추에이터 엔드포인트에 대한 보안을 구성할 수 있습니다.

## 액추에이터 끝점

Actuator는 여러 끝점을 노출합니다. 이러한 끝점을 사용하여 애플리케이션을 모니터링하고 관리할 수 있습니다. 끝점은 두 그룹으로 나뉩니다.

* productionEndpoints: 이 엔드포인트는 프로덕션에서 사용하기 위한 것이며 애플리케이션의 상태에 대한 정보를 제공합니다.
* allEndpoints: 이 끝점은 응용 프로그램의 상태 및 응용 프로그램별 정보에 대한 정보를 제공합니다.

allEndpoints 그룹에는 모든 productionEndpoints와 사용자가 생성한 모든 사용자 지정 엔드포인트가 포함됩니다.

다음 표에는 Actuator에서 제공하는 productionEndpoints가 나열되어 있습니다.

| 끝점 | 설명 |
| --- | --- |
| /감사 이벤트 | 이 엔드포인트는 감사된 애플리케이션 이벤트에 대한 정보를 제공합니다. |
| /콩 | 이 끝점은 Spring 컨테이너에서 생성된 빈에 대한 정보를 제공합니다. |
| /configprops | 이 끝점은 애플리케이션에 대해 설정된 구성 속성에 대한 정보를 제공합니다. |
| /덤프 | 이 엔드포인트는 애플리케이션의 상태를 덤프하는 데 사용할 수 있습니다. 이는 문제 해결에 유용합니다. |
| /env | 이 엔드포인트는 애플리케이션에 대해 설정된 환경 변수에 대한 정보를 제공합니다. |
| /이동경로 | 이 엔드포인트는 Flyway에서 적용된 데이터베이스 마이그레이션에 대한 정보를 제공합니다. |
| /건강 | 이 엔드포인트는 애플리케이션의 상태에 대한 정보를 제공합니다. |
| /정보 | 이 엔드포인트는 애플리케이션별 정보를 제공합니다. |
| /리퀴베이스 | 이 끝점은 Liquibase가 적용한 데이터베이스 마이그레이션에 대한 정보를 제공합니다. |
| /로거 | 이 엔드포인트는 애플리케이션의 로깅 수준을 구성하는 데 사용할 수 있습니다. |
| /메트릭 | 이 엔드포인트는 애플리케이션에 대해 수집된 메트릭에 대한 정보를 제공합니다. |
| /매핑 | 이 엔드포인트는 애플리케이션에 대해 정의된 @RequestMapping 경로에 대한 정보를 제공합니다. |
| /종료 | 이 엔드포인트는 애플리케이션을 종료하는 데 사용할 수 있습니다. |
| /추적 | 이 엔드포인트는 애플리케이션에 대한 HTTP 요청에 대한 정보를 제공합니다. |

이러한 엔드포인트에 액세스하려면 애플리케이션의 경로에 엔드포인트를 추가해야 합니다. 예를 들어 애플리케이션이 http://localhost:8080에서 실행 중인 경우 http://localhost:8080/health에서 /health 엔드포인트에 액세스합니다.

## 액추에이터 끝점 읽기

Actuator 끝점에서 정보를 읽으려면 curl, wget 또는 브라우저와 같은 도구를 사용할 수 있습니다.

예를 들어 /health 엔드포인트를 읽으려면 다음과 같이 curl을 사용할 수 있습니다.

```
$ curl http://localhost:8080/health
```

또는 다음과 같이 wget을 사용할 수 있습니다.

```
$ wget http://localhost:8080/health
```

브라우저를 사용하여 /health 엔드포인트에 액세스하면 다음 출력이 표시됩니다.

```json
{
    "status": "UP",
    "diskSpace": {
        "status": "UP",
        "total": 499963648,
        "free": 367030272,
        "threshold": 10485760
    },
    "db": {
        "status": "UP",
        "database": "H2",
        "hello": 1
    },
    "redis": {
        "status": "UP"
    }
}
```

/health 엔드포인트의 출력은 애플리케이션의 상태에 대한 정보가 포함된 JSON 문서입니다. 상태 필드는 애플리케이션의 전반적인 상태를 나타냅니다. diskSpace, db 및 redis 필드에는 특정 하위 시스템의 상태에 대한 정보가 포함되어 있습니다.

## 사용자 지정 끝점 만들기

기본 제공 끝점 외에도 사용자 지정 끝점을 만들 수도 있습니다. 이렇게 하려면 org.springframework.boot.actuate.endpoint.annotation.Endpoint 인터페이스를 구현하는 클래스를 만들어야 합니다.

예를 들어 다음 클래스는 사용자 목록을 반환하는 사용자 지정 엔드포인트를 정의합니다.

```java
@Endpoint(id="users")
public class UserEndpoint {

    private List<User> users;

    @ReadOperation
    public List<User> getUsers() {
        return this.users;
    }

    public void setUsers(List<User> users) {
        this.users = users;
    }

}
```

@Endpoint 주석은 클래스에 주석을 추가하는 데 사용됩니다. id 속성은 끝점의 식별자를 지정하는 데 사용됩니다. 끝점에 액세스하는 데 사용할 식별자입니다.

getUsers() 메서드에는 @ReadOperation 주석이 추가됩니다. 이 주석은 메서드를 사용하여 끝점에서 정보를 읽을 수 있음을 나타냅니다.

setUsers() 메서드에는 @WriteOperation 주석이 추가됩니다. 이 주석은 메서드를 사용하여 끝점에 정보를 쓸 수 있음을 나타냅니다.

끝점을 등록하려면 클래스에 @Component 주석을 추가해야 합니다. 예를 들어:

```java
@Component
@Endpoint(id="users")
public class UserEndpoint {
    // ...
}
```

또는 응용 프로그램 컨텍스트에 추가하여 끝점을 등록할 수 있습니다. 예를 들어:

```java
@Configuration
public class EndpointConfig {

    @Bean
    public UserEndpoint userEndpoint() {
        return new UserEndpoint();
    }

}
```

엔드포인트를 등록한 후에는 애플리케이션 경로에 엔드포인트 식별자를 추가하여 액세스할 수 있습니다. 예를 들어 애플리케이션이 http://localhost:8080에서 실행 중인 경우 http://localhost:8080/users에서 /users 엔드포인트에 액세스할 수 있습니다.

## 결론

이 기사에서는 Actuator를 사용하여 Spring Boot 애플리케이션을 모니터링하는 방법을 살펴보았습니다. 또한 액추에이터를 사용하여 애플리케이션별 정보를 노출하는 사용자 지정 끝점을 만드는 방법도 살펴보았습니다.