---
title: 스프링 부트 자동 구성 프로세스
description: 
published: true
date: 2023-02-07T07:32:34.093Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:32:32.517Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Autoconfiguration Process***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-autoconfiguration-process)
{.links-list}


# 스프링 부트 자동 구성 프로세스

Spring Boot 자동 구성은 클래스 경로에서 감지한 종속성을 기반으로 Spring 애플리케이션을 자동으로 구성하는 프로세스입니다. 이 자동 구성은 속성, 환경 변수 및 명령줄 인수의 형태로 명시적 구성을 제공하여 미세 조정할 수 있습니다.

Spring Boot에서 자동 구성이 어떻게 작동하는지 이해하려면 Spring 프로파일의 개념을 이해해야 합니다. 프로필은 Spring 애플리케이션에서 활성화할 수 있는 구성 설정 집합입니다. 기본적으로 Spring Boot는 `default` 프로필을 기반으로 애플리케이션을 구성합니다. 그러나 다른 프로필은 `spring.profiles.active` 속성을 사용하거나 환경 변수를 설정하거나 명령줄 인수를 사용하여 활성화할 수 있습니다.

Spring Boot 애플리케이션에서 자동 구성이 활성화되면 Spring Boot 애플리케이션은 클래스 경로에서 감지한 종속성을 기반으로 자체 구성을 자동으로 시도합니다. 예를 들어 클래스 경로에서 `spring-boot-starter-data-jpa` 종속성이 감지되면 Spring Boot는 자동으로 DataSource 및 EntityManagerFactory를 구성합니다.

경우에 따라 명시적 구성을 제공하여 자동 구성 프로세스를 미세 조정해야 할 수도 있습니다. 이는 속성, 환경 변수 및 명령줄 인수를 사용하여 수행할 수 있습니다.

예를 들어 EntityManagerFactory에서 사용할 데이터 소스를 구성하려면 `spring.datasource.url` 속성을 사용할 수 있습니다.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
```

또는 `DATASOURCE_URL` 환경 변수를 사용할 수 있습니다.

```
DATASOURCE_URL=jdbc:mysql://localhost:3306/test
```

마지막으로 `--spring.datasource.url` 명령줄 인수를 사용할 수 있습니다.

```
--spring.datasource.url=jdbc:mysql://localhost:3306/test
```

여러 구성 소스가 제공되면 다음 순서로 평가됩니다.

1. `application.properties` 또는 `application.yml`에 정의된 속성.
2. `@Configuration` 클래스에 정의된 속성.
3. 환경 변수.
4. 명령줄 인수.

자동 구성 프로세스는 `spring.boot.autoconfigure.EnableAutoConfiguration` 주석을 사용하여 비활성화할 수 있습니다.

```java
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }

}
```

위의 예에서 `@EnableAutoConfiguration` 주석은 자동 구성을 활성화하는 데 사용됩니다. `exclude` 속성은 DataSource의 자동 구성을 비활성화하는 `DataSourceAutoConfiguration` 클래스를 제외하는 데 사용됩니다.

`@Conditional` 주석을 사용하여 특정 빈에 대한 자동 구성을 비활성화할 수도 있습니다.

```java
@Configuration
@ConditionalOnProperty(name="spring.datasource.url", matchIfMissing=false)
public class DataSourceConfig {

    @Bean
    public DataSource dataSource() {
        // configure and return DataSource
    }

}
```

위의 예에서 `@ConditionalOnProperty` 주석은 `DataSourceConfig` 클래스를 조건부로 구성하는 데 사용됩니다. `name` 속성은 확인해야 하는 속성의 이름을 지정하는 데 사용됩니다. `matchIfMissing` 속성은 속성이 누락된 경우 조건이 일치해야 하는지 여부를 나타내는 데 사용됩니다. 이 경우 조건은 `spring.datasource.url` 속성이 정의된 경우에만 일치합니다.

속성, 환경 변수 및 명령줄 인수의 형태로 명시적 구성을 제공하여 자동 구성 프로세스를 더욱 미세 조정할 수 있습니다.