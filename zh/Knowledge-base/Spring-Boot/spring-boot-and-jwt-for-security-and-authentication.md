---
title: 用于安全和身份验证的 Spring Boot 和 JWT
description: 
published: true
date: 2023-02-03T10:18:21.170Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:18:19.462Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Spring Boot and JWT for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}


# 用于安全和身份验证的 Spring Boot 和 JWT

Java Web 令牌 (JWT) 是保护 Spring Boot 微服务的一种流行方式。按照设计，它们是无状态的，因此可以轻松扩展。 JWT 可用于身份验证、授权和信息交换。

在本文中，我们将了解如何将 JWT 与 Spring Boot 结合使用以实现安全性和身份验证。我们将涵盖：

- 什么是 JWT 及其工作原理
- 为什么 JWT 是 Spring Boot 微服务的好选择
- 如何在 Spring Boot 中使用 JWT

## 什么是 JWT 及其工作原理

JWT 是一种开放标准 (RFC 7519)，它定义了一种紧凑且独立的方式，用于在各方之间安全地传输信息作为 JSON 对象。此信息可以被验证和信任，因为它是经过数字签名的。 JWT 可以使用秘密或公钥/私钥对进行签名。

JWT 通常用于微服务和单页应用程序 (SPA) 的上下文中。以这种方式使用时，JWT 通常使用私钥签名，而公钥可供应用程序使用。然后应用程序可以使用公钥来验证 JWT。

JWT由三部分组成：

- 标头：这包含令牌的类型和用于对其进行签名的算法。
- 有效载荷：这包含声明。声明是关于实体（通常是用户）和附加元数据的陈述。
- 签名：用于验证令牌未被篡改。

![](https://jwt.io/assets/jwt-diagram.png)

## 为什么 JWT 是 Spring Boot 微服务的好选择

JWT 是 Spring Boot 微服务的不错选择，因为：

- JWT 是无状态的，因此可以轻松扩展。
- JWT 是独立的，因此无需在数据库中存储会话状态。
- JWT 可用于身份验证、授权和信息交换。
- JWT 是一个开放标准，具有详细记录的规范。

## 如何在 Spring Boot 中使用 JWT

我们可以按照以下步骤将 JWT 与 Spring Boot 一起使用：

1. 将 Spring Boot Starter Security 依赖项添加到我们的项目中。
2.配置Spring Security使用JWT。
3. 实施自定义身份验证过滤器。
4. 实施自定义身份验证提供程序。
5. 配置 Spring Security 以使用我们的自定义身份验证过滤器和身份验证提供程序。
6. 创建一个 RestController 来测试我们的实现。

### 1. 将 Spring Boot Starter 安全依赖添加到我们的项目中

首先，我们需要将 Spring Boot Starter Security 依赖项添加到我们的项目中。我们可以通过将以下依赖项添加到我们的 `pom.xml` 文件来做到这一点：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 2.配置Spring Security使用JWT

接下来，我们需要配置 Spring Security 以使用 JWT。我们可以通过将以下配置添加到我们的 application.properties 文件来做到这一点：

```properties
spring.security.jwt.secret=secret
spring.security.jwt.resource-ids=jwt
```

在上面的配置中，我们将 `secret` 属性设置为 `secret`。这是将用于签署我们的 JWT 的密钥。我们还将 `resource-ids` 属性设置为 `jwt`。这是将用于验证我们的 JWT 的资源 ID。

### 3. 实现自定义身份验证过滤器

接下来，我们需要实现自定义身份验证过滤器。此过滤器将用于验证 JWT。我们可以通过创建一个扩展 `AbstractAuthenticationProcessingFilter` 类并覆盖 `attemptAuthentication` 方法的类来做到这一点：

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

在上面的代码中，我们实现了 attemptAuthentication 方法。此方法用于对用户进行身份验证。

首先，我们从“授权”标头中提取 JWT。如果 `Authorization` 标头不存在或不以 `Bearer` 开头，我们将抛出 `JwtException`。

接下来，我们创建一个“JwtAuthenticationToken”并使用“authenticate”方法对其进行身份验证。

### 4. 实现自定义身份验证提供程序

接下来，我们需要实现自定义身份验证提供程序。该提供程序将用于验证 JWT。我们可以通过创建一个扩展 `AuthenticationProvider` 类并覆盖 `supports` 和 `authenticate` 方法的类来做到这一点：

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

在上面的代码中，我们实现了 `supports` 和 `authenticate` 方法。

`supports` 方法用于确定身份验证提供程序是否支持给定的身份验证类型。在我们的例子中，我们只支持“JwtAuthenticationToken”。

`authenticate` 方法用于对用户进行身份验证。首先，我们使用 parser 方法解析 JWT。然后，我们从声明中获取主题和角色。最后，我们创建一个 JwtAuthenticationToken 并返回它。

### 5. 配置 Spring Security 以使用我们的自定义身份验证过滤器和身份验证提供程序

接下来，我们需要配置 Spring Security 以使用我们的自定义身份验证过滤器和身份验证提供程序。我们可以通过将以下配置添加到我们的 application.properties 文件来做到这一点：

```properties
spring.security.jwt.filter=JwtAuthenticationFilter
spring.security.jwt.provider=JwtAuthenticationProvider
```

### 6. 创建一个 RestController 来测试我们的实现

最后，我们需要创建一个 RestController 来测试我们的实现。我们可以通过创建一个用“@RestController”和“@RequestMapping”注释的类来做到这一点：

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

在上面的代码中，我们创建了一个带有 `test` 方法的 RestController。此方法返回字符串“test”。

## 结论

在本文中，我们了解了如何将 JWT 与 Spring Boot 结合使用以实现安全性和身份验证。我们涵盖了：

- 什么是 JWT 及其工作原理
- 为什么 JWT 是 Spring Boot 微服务的好选择
- 如何在 Spring Boot 中使用 JWT

有关 JWT 的更多信息，请参阅以下资源：

- [JSON 网络令牌 (JWT) - 维基百科](https://en.wikipedia.org/wiki/JSON_Web_Token)
- [JWT.io](https://jwt.io/)
- [Spring Security参考-为JWT配置Spring Security](https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jwt)