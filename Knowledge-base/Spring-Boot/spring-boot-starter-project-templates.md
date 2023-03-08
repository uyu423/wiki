---
title: Spring Boot Starter 프로젝트 템플릿
description: 
published: true
date: 2023-02-01T18:57:52.715Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:57:48.590Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Spring Boot Starter Project Templates***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-starter-project-templates)
{.links-list}


# Spring Boot Starter 프로젝트 템플릿

Spring Boot 애플리케이션 개발은 어려운 작업이 될 수 있습니다. 움직이는 부분이 많고 어디서부터 시작해야 할지 알기 어려울 수 있습니다. 여기에서 Spring Boot 스타터 프로젝트 템플릿이 필요합니다.

시작 프로젝트 템플릿은 자체 애플리케이션의 시작점으로 사용할 수 있는 미리 구성된 Spring Boot 애플리케이션입니다. 이러한 템플릿은 번거로움을 최소화하면서 신속하게 시작하고 실행할 수 있는 좋은 방법이 될 수 있습니다.

이 기사에서는 가장 인기 있는 몇 가지 시작 프로젝트 템플릿을 살펴보고 Spring Boot 애플리케이션을 시작하는 데 어떻게 도움이 되는지 알아봅니다.

## 스프링 부트 웹 스타터

Spring Boot Web Starter는 가장 인기 있는 시작 프로젝트 템플릿입니다. 기본 Spring Boot 웹 애플리케이션을 시작하고 실행하는 데 필요한 모든 것을 제공합니다.

Web Starter에는 다음과 같은 종속성이 포함됩니다.

- 스프링 부트 스타터 웹
- 스프링 부트 스타터 톰캣
- spring-boot-starter-thymeleaf

또한 다음과 같은 주요 기능이 포함되어 있습니다.

- 임베디드 톰캣
- Thymeleaf 템플릿 지원
- Spring MVC를 위한 자동 설정

Web Starter를 시작하는 방법은 간단합니다. Spring Initializr를 사용하고 스타터 목록에서 Web Starter를 선택하여 새 프로젝트를 생성할 수 있습니다.

프로젝트가 설정되면 컨트롤러를 추가하여 애플리케이션에 대한 요청을 처리할 수 있습니다. 예를 들어 다음 컨트롤러는 `/` 경로에 대한 요청을 `index.html`이라는 이름의 Thymeleaf 템플릿에 매핑합니다.

```java
@Controller
public class IndexController {

    @RequestMapping("/")
    public String index() {
        return "index";
    }

}
```

그런 다음 `index.html` 템플릿을 `src/main/resources/templates` 디렉토리에 추가할 수 있습니다. Web Starter는 자동으로 Thymeleaf를 구성하고 `http://localhost:8080/`에서 템플릿에 액세스할 수 있습니다.

## 스프링 부트 데이터 JPA 스타터

Spring Boot Data JPA Starter는 또 다른 인기 있는 시작 프로젝트 템플릿입니다. Spring Data JPA를 시작하는 데 필요한 모든 것을 제공합니다.

Data JPA Starter에는 다음 종속성이 포함됩니다.

- spring-boot-starter-data-jpa
- spring-boot-starter-aop
- 스프링 부트 스타터-jdbc

또한 다음과 같은 주요 기능이 포함되어 있습니다.

- Spring Data JPA에 대한 자동 구성
- 거래 지원
- 감사 지원

Data JPA Starter를 시작하는 것은 Web Starter만큼 간단합니다. Spring Initializr를 사용하고 스타터 목록에서 Data JPA Starter를 선택하여 새 프로젝트를 생성할 수 있습니다.

프로젝트가 설정되면 JPA 엔터티를 추가하여 데이터를 나타낼 수 있습니다. 예를 들어 다음 엔터티는 사용자를 나타냅니다.

```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    private String email;

    // Getters and setters...

}
```

그런 다음 저장소 인터페이스를 추가하여 데이터에 액세스할 수 있습니다. 다음 저장소는 ID 또는 이메일로 사용자를 찾는 방법을 제공합니다.

```java
public interface UserRepository extends JpaRepository<User, Long> {

    User findById(Long id);

    User findByEmail(String email);

}
```

Spring Data JPA는 이 인터페이스를 자동으로 구현합니다. 그런 다음 리포지토리를 컨트롤러에 주입하고 이를 사용하여 데이터에 액세스할 수 있습니다.

## 스프링 부트 보안 스타터

Spring Boot Security Starter는 인증 및 권한 부여를 제공해야 하는 애플리케이션을 위한 훌륭한 출발점입니다.

Security Starter에는 다음과 같은 종속성이 포함됩니다.

- 스프링 부트 스타터 보안
- 스프링 보안 구성

또한 다음과 같은 주요 기능이 포함되어 있습니다.

- 스프링 시큐리티를 위한 자동 설정
- 양식 기반 인증 지원
- 정적 자원에 대한 보안

Security Starter로 시작하는 것은 다른 스타터만큼 간단합니다. Spring Initializr를 사용하고 스타터 목록에서 Security Starter를 선택하여 새 프로젝트를 생성할 수 있습니다.

프로젝트가 설정되면 애플리케이션에 보안 구성을 추가할 수 있습니다. 예를 들어 다음 구성은 `/admin` 경로가 있는 모든 URL을 보호합니다.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().permitAll()
            .and()
            .formLogin()
                .loginPage("/login")
                .permitAll();
    }

}
```

이 구성은 `/admin` 경로가 있는 모든 URL을 보호하고 사용자가 `ADMIN` 역할로 인증되어야 합니다. 또한 사용자가 인증할 수 있는 로그인 페이지를 `/login`에 제공합니다.

## 스프링 부트 액추에이터 스타터

Spring Boot Actuator Starter는 모니터링 및 관리 기능을 제공해야 하는 애플리케이션을 위한 훌륭한 출발점입니다.

액추에이터 스타터에는 다음과 같은 종속성이 포함됩니다.

- 스프링 부트 스타터 액추에이터

또한 다음과 같은 주요 기능이 포함되어 있습니다.

- Spring Boot Actuator 자동 구성
- 애플리케이션 모니터링 및 관리를 위한 엔드포인트

액추에이터 스타터로 시작하는 것은 다른 스타터만큼 간단합니다. Spring Initializr를 사용하고 스타터 목록에서 Actuator Starter를 선택하여 새 프로젝트를 생성할 수 있습니다.

프로젝트가 설정되면 액추에이터 엔드포인트를 애플리케이션에 추가할 수 있습니다. 예를 들어 다음 구성은 `info` 및 `health` 엔드포인트를 활성화합니다.

```java
@Configuration
@EnableWebSecurity
public class ActuatorConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .antMatchers("/actuator/**").permitAll()
                .anyRequest().authenticated()
            .and()
            .httpBasic();
    }

}
```

이 구성은 `info` 및 `health` 엔드포인트를 활성화합니다. 이러한 엔드포인트는 애플리케이션 및 해당 상태에 대한 정보를 제공합니다.

## 결론

스타터 프로젝트 템플릿은 최소한의 노력으로 빠르게 시작하고 실행할 수 있는 좋은 방법입니다. 그들은 귀하의 응용 프로그램에 대한 훌륭한 출발점을 제공할 수 있으며 많은 시간과 노력을 절약할 수 있습니다.

이 기사에서는 가장 인기 있는 스타터 프로젝트 템플릿을 살펴보고 Spring Boot 애플리케이션을 시작하는 데 어떻게 도움이 되는지 살펴보았습니다.