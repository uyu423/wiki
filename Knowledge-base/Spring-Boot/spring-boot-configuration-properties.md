---
title: Spring Boot 구성 속성
description: 
published: true
date: 2023-02-01T21:23:40.627Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:23:38.943Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot Configuration Properties***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-configuration-properties)
{.links-list}


# 소개

개발자로서 애플리케이션에서 구성의 중요성을 알고 있을 것입니다. 구성 파일은 애플리케이션 동작 방식을 제어하는 값을 설정하는 방법을 제공합니다. Spring Boot는 작업할 도구 세트를 제공하여 구성 속성 작업을 쉽게 합니다.

이 기사에서는 Spring Boot 구성 속성이 무엇이며 어떻게 작동하는지 살펴보겠습니다. 또한 구성 속성으로 작업할 때 발생할 수 있는 문제 중 일부를 살펴보겠습니다.

# Spring Boot 구성 속성이 무엇인가요?

Spring Boot 구성 속성은 Spring Boot 애플리케이션을 구성하는 데 사용할 수 있는 키/값 쌍입니다. 데이터베이스 연결 문자열, 애플리케이션 이름 및 서버 포트와 같은 다양한 애플리케이션 설정에 대한 값을 설정하는 데 사용할 수 있습니다. 구성 속성은 환경 변수, 시스템 속성 및 명령줄 인수를 포함하여 다양한 방법으로 설정할 수 있습니다.

# Spring Boot 구성 속성으로 작업하는 방법은 무엇입니까?

Spring Boot는 구성 속성을 사용하는 여러 가지 방법을 제공합니다. 이 섹션에서는 구성 속성을 사용하는 가장 일반적인 방법 중 일부를 살펴보겠습니다.

## @ConfigurationProperties 사용

구성 속성으로 작업하는 한 가지 방법은 `@ConfigurationProperties` 주석을 사용하는 것입니다. 이 주석은 클래스에서 구성 속성을 클래스의 필드에 바인딩하는 데 사용할 수 있습니다. 예를 들어 다음 클래스는 `spring.datasource.url` 속성을 `url` 필드에 바인딩합니다.

```java
@ConfigurationProperties(prefix = "spring.datasource")
public class DataSourceConfig {
    private String url;
 
    public String getUrl() {
        return url;
    }
 
    public void setUrl(String url) {
        this.url = url;
    }
}
```

이 클래스를 사용하려면 Spring Boot 애플리케이션에 빈으로 추가해야 합니다.

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @Bean
    public DataSourceConfig dataSourceConfig() {
        return new DataSourceConfig();
    }
}
```

## 환경 추상화 사용

구성 속성을 사용하는 또 다른 방법은 'Environment' 추상화를 사용하는 것입니다. 이 추상화는 특정 속성 이름을 몰라도 구성 속성에 액세스하는 방법을 제공합니다. 예를 들어 다음 코드는 `spring.datasource.url` 속성 값을 가져옵니다.

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @Autowired
    private Environment environment;
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = environment.getProperty("spring.datasource.url");
    }
}
```

## @Value 주석 사용

구성 속성을 사용하는 또 다른 방법은 `@Value` 주석을 사용하는 것입니다. 이 주석은 구성 속성 값을 삽입하기 위해 필드에서 사용할 수 있습니다. 예를 들어 다음 코드는 `url` 필드에 `spring.datasource.url` 속성 값을 삽입합니다.

```java
@SpringBootApplication
public class Application {
    @Value("${spring.datasource.url}")
    private String url;
 
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

# Spring Boot 구성 속성 문제

Spring Boot 구성 속성으로 작업할 때 발생할 수 있는 몇 가지 문제가 있습니다. 이 섹션에서는 가장 일반적인 몇 가지를 살펴보겠습니다.

## 속성은 대소문자를 구분합니다.

Spring Boot 구성 속성은 대/소문자를 구분합니다. 이는 `spring.datasource.url` 속성이 `spring.datasource.URL` 속성과 동일하지 않음을 의미합니다. 속성을 작동시키는 데 문제가 있는 경우 올바른 대소문자를 사용하고 있는지 확인하십시오.

## 응용 프로그램이 시작될 때까지 속성이 확인되지 않습니다.

Spring Boot 구성 속성은 애플리케이션이 시작될 때까지 확인되지 않습니다. 즉, 애플리케이션의 `main` 메서드에서 속성에 액세스하려고 하면 해결되지 않습니다. 예를 들어 다음 코드는 작동하지 않습니다.

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        String dataSourceUrl = System.getProperty("spring.datasource.url");
        SpringApplication.run(Application.class, args);
    }
}
```

이 문제를 해결하기 위해 `@PostConstruct` 주석을 사용할 수 있습니다. 이 주석은 속성이 확인된 후 호출해야 함을 나타내기 위해 메서드에서 사용할 수 있습니다. 예를 들어:

```java
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = System.getProperty("spring.datasource.url");
    }
}
```

## 응용 프로그램 컨텍스트가 초기화될 때까지 속성이 확인되지 않습니다.

알아야 할 또 다른 문제는 응용 프로그램 컨텍스트가 초기화될 때까지 속성이 확인되지 않는다는 것입니다. 즉, `@Configuration` 클래스의 속성에 액세스하려고 하면 해결되지 않습니다. 예를 들어 다음 코드는 작동하지 않습니다.

```java
@Configuration
public class MyConfig {
    @Value("${spring.datasource.url}")
    private String url;
}
```

이 문제를 해결하기 위해 `Environment` 추상화를 사용할 수 있습니다. 예를 들어:

```java
@Configuration
public class MyConfig {
    @Autowired
    private Environment environment;
 
    @PostConstruct
    public void init() {
        String dataSourceUrl = environment.getProperty("spring.datasource.url");
    }
}
```

## 응용 프로그램이 완전히 시작될 때까지 속성이 확인되지 않습니다.

알아야 할 또 다른 문제는 응용 프로그램이 완전히 시작될 때까지 속성이 확인되지 않는다는 것입니다. 즉, `@Bean` 메서드에서 속성에 액세스하려고 하면 해결되지 않습니다. 예를 들어 다음 코드는 작동하지 않습니다.

```java
@Configuration
public class MyConfig {
    @Bean
    public DataSource dataSource() {
        String url = System.getProperty("spring.datasource.url");
        // ...
    }
}
```

이 문제를 해결하기 위해 `Environment` 추상화를 사용할 수 있습니다. 예를 들어:

```java
@Configuration
public class MyConfig {
    @Autowired
    private Environment environment;
 
    @Bean
    public DataSource dataSource() {
        String url = environment.getProperty("spring.datasource.url");
        // ...
    }
}
```

# 결론

이 기사에서는 Spring Boot 구성 속성이 무엇이며 이를 사용하는 방법을 살펴보았습니다. 또한 구성 속성으로 작업할 때 발생할 수 있는 문제 중 일부를 살펴보았습니다.

Spring Boot 애플리케이션 구성은 까다로울 수 있지만 이 기사가 시작하는 데 필요한 정보를 제공했기를 바랍니다.