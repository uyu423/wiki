---
title: Spring Boot and JWT for Security and Authentication
description: 
published: true
date: 2023-02-03T10:18:24.392Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:18:19.481Z
---

- [Spring Boot y JWT para seguridad y autenticación***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}
- [用于安全和身份验证的 Spring Boot 和 JWT***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}
- [보안 및 인증을 위한 Spring Boot 및 JWT***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}


# Spring Boot and JWT for Security and Authentication

Java Web Tokens (JWT) are a popular way to secure Spring Boot microservices. By design, they are stateless and therefore can be easily scaled. JWT can be used for authentication, authorization, and information exchange.

In this article, we'll look at how to use JWT with Spring Boot for security and authentication. We'll cover:

- What is JWT and how it works
- Why JWT is a good choice for Spring Boot microservices
- How to use JWT with Spring Boot

## What is JWT and How it Works

JWT is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWT can be signed using a secret or a public/private key pair.

JWT is commonly used in the context of microservices and single page applications (SPAs). When used in this way, the JWT is typically signed with a private key and the public key is made available to the application. The application can then use the public key to verify the JWT.

JWT consists of three parts:

- Header: This contains the type of the token and the algorithm used to sign it.
- Payload: This contains the claims. Claims are statements about an entity (typically, the user) and additional metadata.
- Signature: This is used to verify that the token has not been tampered with.

![](https://jwt.io/assets/jwt-diagram.png)

## Why JWT is a Good Choice for Spring Boot Microservices

JWT is a good choice for Spring Boot microservices because:

- JWT is stateless and therefore can be easily scaled.
- JWT is self-contained and therefore eliminates the need to store session state in a database.
- JWT can be used for authentication, authorization, and information exchange.
- JWT is an open standard with well-documented specifications.

## How to Use JWT with Spring Boot

We can use JWT with Spring Boot by following these steps:

1. Add the Spring Boot Starter Security dependency to our project.
2. Configure Spring Security to use JWT.
3. Implement a custom authentication filter.
4. Implement a custom authentication provider.
5. Configure Spring Security to use our custom authentication filter and authentication provider.
6. Create a RestController to test our implementation.

### 1. Add the Spring Boot Starter Security Dependency to Our Project

First, we need to add the Spring Boot Starter Security dependency to our project. We can do this by adding the following dependency to our `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 2. Configure Spring Security to Use JWT

Next, we need to configure Spring Security to use JWT. We can do this by adding the following configuration to our `application.properties` file:

```properties
spring.security.jwt.secret=secret
spring.security.jwt.resource-ids=jwt
```

In the above configuration, we've set the `secret` property to `secret`. This is the secret key that will be used to sign our JWT. We've also set the `resource-ids` property to `jwt`. This is the resource ID that will be used to verify our JWT.

### 3. Implement a Custom Authentication Filter

Next, we need to implement a custom authentication filter. This filter will be used to validate the JWT. We can do this by creating a class that extends the `AbstractAuthenticationProcessingFilter` class and overriding the `attemptAuthentication` method:

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

In the above code, we've implemented the `attemptAuthentication` method. This method is used to authenticate the user.

First, we extract the JWT from the `Authorization` header. If the `Authorization` header is not present or does not start with `Bearer`, we throw a `JwtException`.

Next, we create a `JwtAuthenticationToken` and authenticate it using the `authenticate` method.

### 4. Implement a Custom Authentication Provider

Next, we need to implement a custom authentication provider. This provider will be used to validate the JWT. We can do this by creating a class that extends the `AuthenticationProvider` class and overriding the `supports` and `authenticate` methods:

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

In the above code, we've implemented the `supports` and `authenticate` methods.

The `supports` method is used to determine if the authentication provider supports the given authentication type. In our case, we're only supporting `JwtAuthenticationToken`.

The `authenticate` method is used to authenticate the user. First, we parse the JWT using the `parser` method. Then, we get the subject and roles from the claims. Finally, we create a `JwtAuthenticationToken` and return it.

### 5. Configure Spring Security to Use Our Custom Authentication Filter and Authentication Provider

Next, we need to configure Spring Security to use our custom authentication filter and authentication provider. We can do this by adding the following configuration to our `application.properties` file:

```properties
spring.security.jwt.filter=JwtAuthenticationFilter
spring.security.jwt.provider=JwtAuthenticationProvider
```

### 6. Create a RestController to Test Our Implementation

Finally, we need to create a RestController to test our implementation. We can do this by creating a class that annotated with `@RestController` and `@RequestMapping`:

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

In the above code, we've created a RestController with a `test` method. This method returns the string `test`.

## Conclusion

In this article, we've looked at how to use JWT with Spring Boot for security and authentication. We've covered:

- What is JWT and how it works
- Why JWT is a good choice for Spring Boot microservices
- How to use JWT with Spring Boot

For more information on JWT, please see the following resources:

- [JSON Web Token (JWT) - Wikipedia](https://en.wikipedia.org/wiki/JSON_Web_Token)
- [JWT.io](https://jwt.io/)
- [Spring Security Reference - Configuring Spring Security for JWT](https://docs.spring.io/spring-security/site/docs/current/reference/html5/#jc-authentication-jwt)