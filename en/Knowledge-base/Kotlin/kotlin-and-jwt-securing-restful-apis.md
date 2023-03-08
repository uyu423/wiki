---
title: Kotlin and JWT: Securing RESTful APIs
description: 
published: true
date: 2023-02-13T15:17:52.274Z
tags: 
editor: markdown
dateCreated: 2023-02-13T15:17:44.946Z
---

- [Kotlin y JWT: Protección de las API RESTful***Spanish** document is available*](/es/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}
- [Kotlin 和 JWT：保护 RESTful API***Chinese Simplified** document is available*](/zh/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}
- [Kotlin 및 JWT: RESTful API 보안***Korean** document is available*](/ko/Knowledge-base/Kotlin/kotlin-and-jwt-securing-restful-apis)
{.links-list}


# Kotlin and JWT: Securing RESTful APIs

With the rise of Kotlin as a first-class language for developing Android apps, it's no surprise that more and more developers are interested in using Kotlin for server-side development as well. In this article, we'll take a look at how to use Kotlin and the Java Web Tokens (JWT) framework to secure a RESTful API.

JWT is a standard for creating access tokens that allow servers to verify the identity of clients. This is especially important in a RESTful API, where clients can be anything from a mobile app to a browser extension. By using JWT, we can be sure that only authorized clients can access our API.

To use JWT with Kotlin, we'll need to install the kotlin-jwt library. This library provides a set of functions for creating and verifying JWT tokens.

Once we have the kotlin-jwt library installed, we can use it to create a JWT token like this:

```kotlin
val jwt = JWT.create()
    .withSubject("user@example.com")
    .withExpiresAt(Date())
    .sign(algorithm)
```

where `algorithm` is an instance of `Algorithm` that specifies the signing algorithm to use. For example, we could use the `HMAC256` algorithm like this:

```kotlin
val algorithm = Algorithm.HMAC256("secret")
```

We can then use the `jwt` variable to generate a token:

```kotlin
val token = jwt.generate()
```

Now that we have a token, we can use it to secure our API. For example, we can add it to the `Authorization` header of our HTTP requests:

```kotlin
val request = Request.Builder()
    .url("https://example.com/api/v1/users")
    .header("Authorization", "Bearer $token")
    .build()
```

The server can then use the `verify` function to verify the token:

```kotlin
val jwt = JWT.require(algorithm)
    .build()

val verifiedToken = jwt.verify(token)
```

If the token is valid, the `verifiedToken` variable will contain the decoded token. We can then use the `getSubject` function to get the user's email address:

```kotlin
val userEmail = verifiedToken.getSubject()
```

Now that we know how to use Kotlin and JWT to secure a RESTful API, let's look at some resources for further reading.

## Resources

- [JSON Web Tokens](https://jwt.io/)
- [kotlin-jwt](https://github.com/kotlinc-es/kotlin-jwt)
- [Kotlin Security](https://kotlinlang.org/docs/reference/security.html)