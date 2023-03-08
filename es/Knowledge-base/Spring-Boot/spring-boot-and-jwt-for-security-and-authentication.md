---
title: Spring Boot y JWT para seguridad y autenticación
description: 
published: true
date: 2023-02-03T10:18:21.135Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:18:19.480Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and JWT for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-jwt-for-security-and-authentication)
{.links-list}


# Spring Boot y JWT para seguridad y autenticación

Los tokens web de Java (JWT) son una forma popular de proteger los microservicios de Spring Boot. Por diseño, no tienen estado y, por lo tanto, se pueden escalar fácilmente. JWT se puede utilizar para autenticación, autorización e intercambio de información.

En este artículo, veremos cómo usar JWT con Spring Boot para seguridad y autenticación. Cubriremos:

- ¿Qué es JWT y cómo funciona?
- Por qué JWT es una buena opción para los microservicios de Spring Boot
- Cómo usar JWT con Spring Boot

## ¿Qué es JWT y cómo funciona?

JWT es un estándar abierto (RFC 7519) que define una forma compacta y autónoma de transmitir información de forma segura entre las partes como un objeto JSON. Esta información se puede verificar y confiar porque está firmada digitalmente. JWT se puede firmar usando un secreto o un par de claves pública/privada.

JWT se usa comúnmente en el contexto de microservicios y aplicaciones de una sola página (SPA). Cuando se usa de esta manera, el JWT generalmente se firma con una clave privada y la clave pública se pone a disposición de la aplicación. Luego, la aplicación puede usar la clave pública para verificar el JWT.

JWT consta de tres partes:

- Cabecera: Contiene el tipo de token y el algoritmo utilizado para firmarlo.
- Payload: Contiene las reclamaciones. Las reclamaciones son declaraciones sobre una entidad (normalmente, el usuario) y metadatos adicionales.
- Firma: Sirve para comprobar que el token no ha sido manipulado.

![](https://jwt.io/assets/jwt-diagram.png)

## Por qué JWT es una buena opción para los microservicios Spring Boot

JWT es una buena opción para los microservicios de Spring Boot porque:

- JWT no tiene estado y, por lo tanto, se puede escalar fácilmente.
- JWT es autónomo y, por lo tanto, elimina la necesidad de almacenar el estado de la sesión en una base de datos.
- JWT se puede utilizar para autenticación, autorización e intercambio de información.
- JWT es un estándar abierto con especificaciones bien documentadas.

## Cómo usar JWT con Spring Boot

Podemos usar JWT con Spring Boot siguiendo estos pasos:

1. Agregue la dependencia Spring Boot Starter Security a nuestro proyecto.
2. Configure Spring Security para usar JWT.
3. Implemente un filtro de autenticación personalizado.
4. Implemente un proveedor de autenticación personalizado.
5. Configure Spring Security para usar nuestro filtro de autenticación personalizado y proveedor de autenticación.
6. Cree un RestController para probar nuestra implementación.

### 1. Agregar la dependencia de seguridad de Spring Boot Starter a nuestro proyecto

Primero, debemos agregar la dependencia Spring Boot Starter Security a nuestro proyecto. Podemos hacer esto agregando la siguiente dependencia a nuestro archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

### 2. Configure Spring Security para usar JWT

A continuación, debemos configurar Spring Security para usar JWT. Podemos hacer esto agregando la siguiente configuración a nuestro archivo `application.properties`:

```properties
spring.security.jwt.secret=secret
spring.security.jwt.resource-ids=jwt
```

En la configuración anterior, hemos establecido la propiedad `secret` en `secret`. Esta es la clave secreta que se utilizará para firmar nuestro JWT. También hemos establecido la propiedad `resource-ids` en `jwt`. Este es el ID de recurso que se usará para verificar nuestro JWT.

### 3. Implementar un filtro de autenticación personalizado

A continuación, debemos implementar un filtro de autenticación personalizado. Este filtro se utilizará para validar el JWT. Podemos hacer esto creando una clase que amplíe la clase `AbstractAuthenticationProcessingFilter` y reemplazando el método `attemptAuthentication`:

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

En el código anterior, implementamos el método `attemptAuthentication`. Este método se utiliza para autenticar al usuario.

Primero, extraemos el JWT del encabezado `Autorización`. Si el encabezado `Autorización` no está presente o no comienza con `Bearer`, lanzamos una `JwtException`.

A continuación, creamos un `JwtAuthenticationToken` y lo autenticamos usando el método `authenticate`.

### 4. Implementar un proveedor de autenticación personalizado

A continuación, debemos implementar un proveedor de autenticación personalizado. Este proveedor se utilizará para validar el JWT. Podemos hacer esto creando una clase que amplíe la clase `AuthenticationProvider` y reemplazando los métodos `supports` y `authenticate`:

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

En el código anterior, hemos implementado los métodos `support` y `authenticate`.

El método `supports` se utiliza para determinar si el proveedor de autenticación admite el tipo de autenticación dado. En nuestro caso, solo admitimos `JwtAuthenticationToken`.

El método `authenticate` se utiliza para autenticar al usuario. Primero, analizamos el JWT usando el método `parser`. Luego, obtenemos el tema y los roles de los reclamos. Finalmente, creamos un `JwtAuthenticationToken` y lo devolvemos.

### 5. Configure Spring Security para usar nuestro filtro de autenticación personalizado y proveedor de autenticación

A continuación, debemos configurar Spring Security para usar nuestro filtro de autenticación personalizado y nuestro proveedor de autenticación. Podemos hacer esto agregando la siguiente configuración a nuestro archivo `application.properties`:

```properties
spring.security.jwt.filter=JwtAuthenticationFilter
spring.security.jwt.provider=JwtAuthenticationProvider
```

### 6. Crear un RestController para probar nuestra implementación

Finalmente, necesitamos crear un RestController para probar nuestra implementación. Podemos hacer esto creando una clase que anote con `@RestController` y `@RequestMapping`:

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

En el código anterior, hemos creado un RestController con un método `test`. Este método devuelve la cadena `test`.

## Conclusión

En este artículo, hemos visto cómo usar JWT con Spring Boot para seguridad y autenticación. Hemos cubierto:

- ¿Qué es JWT y cómo funciona?
- Por qué JWT es una buena opción para los microservicios de Spring Boot
- Cómo usar JWT con Spring Boot

Para obtener más información sobre JWT, consulte los siguientes recursos:

- [Token web JSON (JWT) - Wikipedia](https://en.wikipedia.org/wiki/JSON_Web_Token)
- [JWT.io](https://jwt.io/)
- [Referencia de Spring Security - Configuración de Spring Security para JWT](https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jwt)