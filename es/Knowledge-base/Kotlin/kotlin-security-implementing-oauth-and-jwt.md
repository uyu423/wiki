---
title: Seguridad de Kotlin: implementación de OAuth y JWT
description: 
published: true
date: 2023-02-09T01:17:53.592Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:17:51.925Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin Security: Implementing OAuth and JWT***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-security-implementing-oauth-and-jwt)
{.links-list}


# Seguridad de Kotlin: implementación de OAuth y JWT

En este artículo, veremos cómo implementar la seguridad en una aplicación Kotlin usando OAuth y JSON Web Tokens (JWT). También exploraremos algunas de las mejores prácticas para hacerlo.

## ¿Qué es OAuth?

OAuth es un estándar abierto para la autorización que permite que las aplicaciones de terceros accedan a los recursos sin tener que almacenar ni administrar las credenciales de los usuarios. Lo hace delegando la autorización al propietario del recurso (es decir, el usuario).

Las aplicaciones web suelen utilizar OAuth para permitir que los usuarios inicien sesión con sus credenciales existentes desde otro servicio, como Facebook o Google. Esto se conoce como "autenticación de terceros".

## ¿Qué es JWT?

JSON Web Token (JWT) es un estándar abierto que define una forma compacta y autónoma de transmitir datos entre partes como un objeto JSON. Estos datos se pueden verificar y confiar porque están firmados digitalmente.

Los JWT a menudo se usan en escenarios de autenticación y autorización, ya que se pueden usar para transmitir información sobre el usuario de manera segura.

## Implementando OAuth en Kotlin

Veamos cómo implementar OAuth en una aplicación de Kotlin. Usaremos la biblioteca [ScribeJava](https://github.com/scribejava/scribejava) para simplificar el proceso.

Primero, necesitamos agregar la biblioteca ScribeJava a las dependencias de nuestro proyecto:

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.github.scribejava:scribejava-core:2.5.3")
}
```

A continuación, debemos crear una clase que represente nuestro servicio OAuth. Esta clase será responsable de configurar el flujo de OAuth y manejar la interacción con el proveedor de OAuth.

Para este ejemplo, usaremos la API OAuth de Facebook:

```kotlin
// FacebookOAuthService.kt

import com.github.scribejava.apis.FacebookApi
import com.github.scribejava.core.builder.ServiceBuilder
import com.github.scribejava.core.model.OAuth2AccessToken
import com.github.scribejava.core.model.OAuthRequest
import com.github.scribejava.core.model.Verb
import com.github.scribejava.core.oauth.OAuth20Service

class FacebookOAuthService(
    private val clientId: String,
    private val clientSecret: String,
    private val callbackUrl: String
) {
    private val service: OAuth20Service = ServiceBuilder(clientId)
        .apiSecret(clientSecret)
        .callback(callbackUrl)
        .build(FacebookApi.instance())

    fun getAuthorizationUrl(): String {
        return service.getAuthorizationUrl()
    }

    fun getAccessToken(code: String): OAuth2AccessToken {
        return service.getAccessToken(code)
    }

    fun getUserProfile(accessToken: OAuth2AccessToken): String {
        val request = OAuthRequest(Verb.GET, "https://graph.facebook.com/me")
        service.signRequest(accessToken, request)

        return service.execute(request).body
    }
}
```

En el método `getUserProfile`, usamos la API Graph de Facebook para obtener el perfil del usuario actual.

Ahora que tenemos nuestra clase de servicio OAuth, echemos un vistazo a cómo usarla en una aplicación de Kotlin.

Primero, necesitamos crear una ruta que redirija al usuario a la página de inicio de sesión del proveedor de OAuth:

```kotlin
// OAuthController.kt

import org.springframework.stereotype.Controller
import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RequestParam
import org.springframework.web.servlet.view.RedirectView

@Controller
@RequestMapping("/oauth")
class OAuthController(
    private val facebookOAuthService: FacebookOAuthService
) {
    @GetMapping("/login")
    fun login(): RedirectView {
        val authorizationUrl = facebookOAuthService.getAuthorizationUrl()
        return RedirectView(authorizationUrl)
    }
}
```

La ruta `login` redirige al usuario a la página de inicio de sesión de Facebook. Una vez que el usuario inicie sesión, será redirigido a la ruta de "devolución de llamada".

A continuación, necesitamos crear la ruta `devolución de llamada`. Esta ruta es responsable de obtener el token de acceso del proveedor de OAuth y luego obtener el perfil del usuario:

```kotlin
// OAuthController.kt (continued)

@GetMapping("/callback")
fun callback(@RequestParam("code") code: String): String {
    val accessToken = facebookOAuthService.getAccessToken(code)
    val userProfile = facebookOAuthService.getUserProfile(accessToken)

    // ...

    return "redirect:/"
}
```

## Implementando JWT en Kotlin

Ahora que hemos visto cómo implementar OAuth, echemos un vistazo a cómo implementar JWT en Kotlin. Usaremos la biblioteca [Kotlin-JWT](https://github.com/kittinunf/kotlin-jwt) para simplificar el proceso.

Primero, necesitamos agregar la biblioteca Kotlin-JWT a las dependencias de nuestro proyecto:

```kotlin
// build.gradle

repositories {
    mavenCentral()
}

dependencies {
    implementation("com.auth0:kotlin-jwt:3.3.0")
}
```

A continuación, debemos crear una clase que represente nuestro servicio JWT. Esta clase será responsable de crear y verificar tokens JWT.

Para este ejemplo, usaremos el algoritmo HS256:

```kotlin
// JWTService.kt

import com.auth0.jwt.JWT
import com.auth0.jwt.algorithms.Algorithm
import com.auth0.jwt.exceptions.JWTVerificationException
import java.util.*

class JWTService(private val secret: String) {
    private val algorithm = Algorithm.HMAC256(secret)

    fun generateToken(claims: Map<String, Any>): String {
        return JWT.create()
            .withClaim("iss", "kotlin-jwt-demo")
            .withClaim("iat", Date())
            .withClaim("exp", Date(Date().time + 60 * 60 * 1000)) // 1 hour
            .withClaim("sub", "user@example.com")
            .withClaim("aud", "https://example.com")
            .withClaim("nbf", Date())
            .withClaim("jti", UUID.randomUUID().toString())
            .withClaim("foo", "bar")
            .withClaim("foo2", "baz")
            .withClaim("qaz", "wsx")
            .sign(algorithm)
    }

    fun verifyToken(token: String): Boolean {
        return try {
            JWT.require(algorithm).build().verify(token)
            true
        } catch (e: JWTVerificationException) {
            false
        }
    }
}
```

En el método `generateToken`, usamos el método `withClaim` para especificar las notificaciones que queremos incluir en el token.

Ahora que tenemos nuestra clase de servicio JWT, echemos un vistazo a cómo usarla en una aplicación de Kotlin.

Primero, necesitamos crear una ruta que genere un token JWT:

```kotlin
// JWTController.kt

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RequestMapping
import org.springframework.web.bind.annotation.RestController

@RestController
@RequestMapping("/jwt")
class JWTController(
    private val jwtService: JWTService
) {
    @GetMapping("/generate")
    fun generateToken(): String {
        return jwtService.generateToken(emptyMap())
    }
}
```

La ruta `generateToken` genera un token JWT sin reclamos.

A continuación, debemos crear una ruta que verifique un token JWT:

```kotlin
// JWTController.kt (continued)

@GetMapping("/verify")
fun verifyToken(@RequestParam("token") token: String): Boolean {
    return jwtService.verifyToken(token)
}
```

La ruta `verifyToken` verifica que el token JWT sea válido.

## Mejores prácticas

Al implementar la seguridad en una aplicación de Kotlin, hay algunas prácticas recomendadas que se deben tener en cuenta:

- **Utilice OAuth para la autenticación, no para la autorización.** OAuth es un estándar abierto para la autorización, no para la autenticación. Si bien se puede usar para ambos propósitos, es mejor usarlo para la autorización (es decir, delegar la autorización al propietario del recurso) y usar otro método, como JWT, para la autenticación.

- **Use JWT para la autenticación, no para la autorización.** Si bien JWT se puede usar para ambos propósitos, es mejor usarlo para la autenticación (es decir, transmitir información sobre el usuario) y usar otro método, como OAuth, para la autorización.

- **No almacene datos confidenciales en reclamos de JWT.** Los reclamos de JWT son públicos y cualquier persona puede leerlos. Por lo tanto, es importante no almacenar datos confidenciales, como contraseñas de usuarios, en notificaciones de JWT.

- **Utilice un secreto seguro para firmar tokens JWT.** El secreto utilizado para firmar tokens JWT debe mantenerse confidencial y no codificarse en la aplicación. Una buena manera de hacer esto es usar variables de entorno.

- **Verifique el reclamo `iss` al validar tokens JWT. ** El reclamo `iss` (emisor) se usa para identificar la fuente del token JWT. Al validar un token JWT, es importante verificar que el reclamo `iss` coincida con el valor esperado.

- **Verifique el reclamo `aud` al validar tokens JWT.** El reclamo `aud` (audiencia) se usa para identificar al destinatario previsto del token JWT. Al validar un token JWT, es importante verificar que el reclamo `aud` coincida con el valor esperado.

- **Verifique el reclamo `exp` al validar tokens JWT.** El reclamo `exp` (caducidad) se usa para especificar la fecha de vencimiento del token JWT. Al validar un token JWT, es importante verificar que la fecha actual sea anterior a la fecha de vencimiento.

- **Verifique el reclamo `nbf` al validar tokens JWT. ** El reclamo `nbf` (no antes) se usa para especificar la fecha antes de la cual el token JWT no debe aceptarse para su procesamiento. Al validar un token JWT, es importante verificar que la fecha actual sea posterior a la fecha no anterior.

- **Verifique el reclamo `jti` al validar tokens JWT. ** El reclamo `jti` (JWT ID) se usa para proporcionar un identificador único para el token JWT. Al validar un token JWT, es importante verificar que el reclamo `jti` esté presente y que su valor sea único.

- **No utilices la autenticación básica.** Si bien la autenticación básica es fácil de implementar, no es muy segura. Es mejor usar un método más seguro, como OAuth o JWT.

- **No use el mismo secreto para firmar tokens JWT y cifrar datos.** Si bien es conveniente usar el mismo secreto para ambos propósitos, no es muy seguro. Es mejor usar un secreto diferente para cada propósito.

- **Rote los secretos regularmente.** Los secretos deben rotarse regularmente para reducir el riesgo de que se vean comprometidos. Una buena regla general es rotar los secretos cada 90 días.

## Conclusión

En este artículo, hemos visto cómo implementar la seguridad en una aplicación de Kotlin utilizando OAuth y JWT. También hemos visto algunas de las mejores prácticas para hacerlo.