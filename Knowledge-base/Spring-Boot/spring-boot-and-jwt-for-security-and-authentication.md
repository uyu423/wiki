---
title: 보안 및 인증을 위한 Spring Boot 및 JWT
description: 
published: true
date: 2023-02-03T10:18:21.163Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:18:19.455Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and JWT for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}


# 보안 및 인증을 위한 Spring Boot 및 JWT

JWT(Java Web Tokens)는 Spring Boot 마이크로서비스를 보호하는 널리 사용되는 방법입니다. 설계상 상태 비저장이므로 쉽게 확장할 수 있습니다. JWT는 인증, 권한 부여 및 정보 교환에 사용할 수 있습니다.

이 기사에서는 보안 및 인증을 위해 Spring Boot와 함께 JWT를 사용하는 방법을 살펴보겠습니다. 우리는 다음을 다룰 것입니다:

- JWT 란 무엇이며 어떻게 작동합니까?
- JWT가 Spring Boot 마이크로서비스에 적합한 이유
- Spring Boot에서 JWT를 사용하는 방법

## JWT란 무엇이며 어떻게 작동합니까?

JWT는 당사자 간에 정보를 JSON 개체로 안전하게 전송하기 위한 간결하고 독립적인 방법을 정의하는 개방형 표준(RFC 7519)입니다. 이 정보는 디지털 서명되어 있으므로 확인하고 신뢰할 수 있습니다. JWT는 비밀 또는 공개/개인 키 쌍을 사용하여 서명할 수 있습니다.

JWT는 일반적으로 마이크로서비스 및 SPA(단일 페이지 애플리케이션) 컨텍스트에서 사용됩니다. 이러한 방식으로 사용되는 경우 JWT는 일반적으로 개인 키로 서명되며 공개 키는 애플리케이션에서 사용할 수 있습니다. 그런 다음 애플리케이션은 공개 키를 사용하여 JWT를 확인할 수 있습니다.

JWT는 세 부분으로 구성됩니다.

- 헤더: 여기에는 토큰의 유형과 서명에 사용된 알고리즘이 포함됩니다.
- 페이로드: 클레임을 포함합니다. 클레임은 엔터티(일반적으로 사용자) 및 추가 메타데이터에 대한 설명입니다.
- 서명: 토큰이 변조되지 않았음을 확인하기 위해 사용됩니다.

![](https://jwt.io/assets/jwt-diagram.png)

## JWT가 Spring Boot 마이크로서비스에 적합한 이유

JWT는 다음과 같은 이유로 Spring Boot 마이크로서비스에 적합합니다.

- JWT는 상태 비저장이므로 쉽게 확장할 수 있습니다.
- JWT는 독립적이므로 데이터베이스에 세션 상태를 저장할 필요가 없습니다.
- JWT는 인증, 권한 부여 및 정보 교환에 사용할 수 있습니다.
- JWT는 사양이 잘 문서화된 개방형 표준입니다.

## Spring Boot에서 JWT를 사용하는 방법

다음 단계에 따라 Spring Boot에서 JWT를 사용할 수 있습니다.

1. 프로젝트에 Spring Boot Starter Security 종속성을 추가합니다.
2. JWT를 사용하도록 Spring Security를 구성합니다.
3. 사용자 지정 인증 필터를 구현합니다.
4. 사용자 지정 인증 공급자를 구현합니다.
5. 사용자 지정 인증 필터 및 인증 공급자를 사용하도록 Spring Security를 구성합니다.
6. 구현을 테스트하기 위해 RestController를 만듭니다.

### 1. 프로젝트에 Spring Boot Starter 보안 종속성 추가

먼저 프로젝트에 Spring Boot Starter Security 종속성을 추가해야 합니다. `pom.xml` 파일에 다음 종속성을 추가하여 이를 수행할 수 있습니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 2. JWT를 사용하도록 스프링 보안 구성

다음으로 JWT를 사용하도록 Spring Security를 구성해야 합니다. `application.properties` 파일에 다음 구성을 추가하여 이를 수행할 수 있습니다.

```properties
spring.security.jwt.secret=secret
spring.security.jwt.resource-ids=jwt
```

위 구성에서 `비밀` 속성을 `비밀`로 설정했습니다. 이것은 JWT에 서명하는 데 사용될 비밀 키입니다. 또한 `resource-ids` 속성을 `jwt`로 설정했습니다. JWT를 확인하는 데 사용할 리소스 ID입니다.

### 3. 사용자 지정 인증 필터 구현

다음으로 사용자 지정 인증 필터를 구현해야 합니다. 이 필터는 JWT의 유효성을 검사하는 데 사용됩니다. `AbstractAuthenticationProcessingFilter` 클래스를 확장하고 `attemptAuthentication` 메서드를 재정의하는 클래스를 생성하여 이를 수행할 수 있습니다.

```java
public class JwtAuthenticationFilter extends AbstractAuthenticationProcessingFilter {

    public JwtAuthenticationFilter(RequestMatcher requiresAuthenticationRequestMatcher) {
        super(requiresAuthenticationRequestMatcher);
    }

    @Override
    public Authentication attemptAuthentication(HttpServletRequest httpServletRequest,
                                                HttpServletResponse httpServletResponse) throws AuthenticationException, IOException, ServletException {

        String header = httpServletRequest.getHeader("Authorization");

        if (header == null || !header.startsWith("Bearer ")) {
            throw new JwtException("No JWT token found in request headers");
        }

        String token = header.substring(7);

        JwtAuthenticationToken jwtAuthenticationToken = new JwtAuthenticationToken(token);
        return getAuthenticationManager().authenticate(jwtAuthenticationToken);
    }
}
```

위의 코드에서 `attemptAuthentication` 메서드를 구현했습니다. 이 방법은 사용자를 인증하는 데 사용됩니다.

먼저 `Authorization` 헤더에서 JWT를 추출합니다. `Authorization` 헤더가 없거나 `Bearer`로 시작하지 않으면 `JwtException`이 발생합니다.

다음으로 `JwtAuthenticationToken`을 만들고 `authenticate` 메서드를 사용하여 인증합니다.

### 4. 사용자 지정 인증 공급자 구현

다음으로 사용자 지정 인증 공급자를 구현해야 합니다. 이 공급자는 JWT의 유효성을 검사하는 데 사용됩니다. `AuthenticationProvider` 클래스를 확장하고 `supports` 및 `authenticate` 메서드를 재정의하는 클래스를 생성하여 이를 수행할 수 있습니다.

```java
public class JwtAuthenticationProvider implements AuthenticationProvider {

    @Override
    public boolean supports(Class<?> aClass) {
        return JwtAuthenticationToken.class.equals(aClass);
    }

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {

        String token = authentication.getCredentials().toString();

        try {
            Claims claims = Jwts.parser()
                    .setSigningKey("secret")
                    .parseClaimsJws(token)
                    .getBody();

            String username = claims.getSubject();

            if (username == null) {
                throw new JwtException("JWT token is missing subject");
            }

            List<String> roles = claims.get("roles", List.class);

            if (roles == null) {
                throw new JwtException("JWT token is missing roles");
            }

            return new JwtAuthenticationToken(
                    username,
                    roles,
                    authentication.getAuthorities());

        } catch (JwtException e) {
            throw new BadCredentialsException("Invalid JWT token", e);
        }
    }
}
```

위의 코드에서 `supports` 및 `authenticate` 메소드를 구현했습니다.

`supports` 메소드는 인증 공급자가 주어진 인증 유형을 지원하는지 확인하는 데 사용됩니다. 우리의 경우에는 `JwtAuthenticationToken`만 지원합니다.

`authenticate` 메소드는 사용자를 인증하는 데 사용됩니다. 먼저 `parser` 메서드를 사용하여 JWT를 구문 분석합니다. 그런 다음 주장에서 주제와 역할을 얻습니다. 마지막으로 `JwtAuthenticationToken`을 생성하고 반환합니다.

### 5. 사용자 지정 인증 필터 및 인증 공급자를 사용하도록 Spring Security 구성

다음으로 사용자 지정 인증 필터 및 인증 공급자를 사용하도록 Spring Security를 구성해야 합니다. `application.properties` 파일에 다음 구성을 추가하여 이를 수행할 수 있습니다.

```properties
spring.security.jwt.filter=JwtAuthenticationFilter
spring.security.jwt.provider=JwtAuthenticationProvider
```

### 6. 구현을 테스트하기 위한 RestController 생성

마지막으로 구현을 테스트하기 위해 RestController를 생성해야 합니다. `@RestController` 및 `@RequestMapping`으로 주석이 달린 클래스를 생성하여 이를 수행할 수 있습니다.

```java
@RestController
@RequestMapping("/test")
public class TestController {

    @GetMapping
    public String test() {
        return "test";
    }
}
```

위의 코드에서 우리는 `test` 메서드로 RestController를 만들었습니다. 이 메서드는 문자열 `test`를 반환합니다.

## 결론

이 기사에서는 보안 및 인증을 위해 Spring Boot와 함께 JWT를 사용하는 방법을 살펴보았습니다. 우리는 다음을 다루었습니다.

- JWT 란 무엇이며 어떻게 작동합니까?
- JWT가 Spring Boot 마이크로서비스에 적합한 이유
- Spring Boot에서 JWT를 사용하는 방법

JWT에 대한 자세한 내용은 다음 리소스를 참조하세요.

- [JSON 웹 토큰(JWT) - Wikipedia](https://en.wikipedia.org/wiki/JSON_Web_Token)
- [JWT.io](https://jwt.io/)
- [스프링 보안 레퍼런스 - JWT용 스프링 보안 구성](https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jwt)