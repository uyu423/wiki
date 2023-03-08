---
title: 토큰 및 쿠키로 사용자 세션 관리
description: 
published: true
date: 2023-02-17T18:16:22.611Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:57:34.472Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Managing User Sessions with Tokens and Cookies***English** version of this document is available*](/en/Knowledge-base/Backend/managing-user-sessions-with-tokens-and-cookies)
{.links-list}



# 토큰과 쿠키로 사용자 세션 관리하기

쿠키와 토큰은 사용자 세션을 관리하는 데 사용되는 두 가지 메커니즘입니다. 이 기사에서는 둘 사이의 차이점과 웹 애플리케이션에서 각각을 구현하는 방법에 대해 설명합니다.

## 쿠키

쿠키는 사용자의 컴퓨터에 저장되는 작은 데이터 조각입니다. 각 요청과 함께 서버로 전송되며 사용자 세션에 대한 정보를 저장하는 데 사용할 수 있습니다.

쿠키에는 두 가지 유형이 있습니다.

* **세션 쿠키**: 사용자가 브라우저를 닫을 때 삭제되는 임시 쿠키입니다. 일반적으로 세션 ID와 같이 현재 세션에 필요한 정보를 저장하는 데 사용됩니다.

* **영구 쿠키**: 일정 기간 동안 사용자의 컴퓨터에 저장되는 쿠키입니다. 일반적으로 사용자 ID와 같이 향후 세션에 필요한 정보를 저장하는 데 사용됩니다.

쿠키는 일반적으로 HTTP 요청의 `cookie` 헤더에 저장됩니다. 'Set-Cookie' 헤더는 사용자 컴퓨터에 쿠키를 설정하는 데 사용됩니다.

## 토큰

토큰은 사용자의 ID를 나타내는 데 사용되는 문자열입니다. 일반적으로 서버에서 생성되어 저장되는 클라이언트로 전송됩니다. 그런 다음 각 요청과 함께 서버로 다시 전송됩니다.

토큰은 세션 ID와 같은 사용자 세션에 대한 정보를 저장하는 데 사용할 수 있습니다. 그러나 이에 국한되지 않습니다. 또한 사용자 ID와 같은 사용자 ID에 대한 정보를 저장하는 데 사용할 수도 있습니다.

토큰에는 두 가지 유형이 있습니다.

* **일반 텍스트 토큰**: 암호화되지 않은 토큰입니다. 생성하기 쉽지만 위조하기도 쉽습니다.

* **암호화된 토큰**: 암호화된 토큰입니다. 그것들은 생성하기도 더 어렵지만 위조하기도 더 어렵습니다.

토큰은 일반적으로 HTTP 요청의 `Authorization` 헤더에 저장됩니다. 'Bearer' 토큰은 가장 일반적인 유형의 토큰입니다.

## 토큰 구현

토큰을 구현하는 방법에는 여러 가지가 있습니다. 다음은 한 가지 예입니다.

```java
public class TokenService {
    
    public static final String TOKEN_SECRET = "secret";
    
    public static String generateToken(String userId) {
        String token = JWT.create()
                .withSubject(userId)
                .sign(Algorithm.HMAC256(TOKEN_SECRET));
        return token;
    }
    
    public static String validateToken(String token) {
        try {
            JWT.decode(token).getSubject();
        } catch (JWTDecodeException e) {
            return null;
        }
        return token;
    }
}
```

이 예에서는 [`java-jwt`](https://github.com/jwtk/jjwt) 라이브러리를 사용하여 토큰을 생성하고 검증했습니다. 또한 [`HMAC256`](https://en.wikipedia.org/wiki/HMAC) 알고리즘을 사용하여 토큰을 암호화했습니다.

## 쿠키 구현

쿠키를 구현하는 방법에는 여러 가지가 있습니다. 다음은 한 가지 예입니다.

```java
public class CookieService {
    
    public static void setCookie(HttpServletResponse response, String name, String value) {
        Cookie cookie = new Cookie(name, value);
        cookie.setSecure(true); // Set this to true in production
        cookie.setHttpOnly(true);
        cookie.setMaxAge(3600); // Set this to a negative value to make the cookie session-only
        cookie.setPath("/");
        response.addCookie(cookie);
    }
    
    public static Cookie getCookie(HttpServletRequest request, String name) {
        Cookie[] cookies = request.getCookies();
        if (cookies != null) {
            for (Cookie cookie : cookies) {
                if (cookie.getName().equals(name)) {
                    return cookie;
                }
            }
        }
        return null;
    }
    
    public static void deleteCookie(HttpServletResponse response, String name) {
        Cookie cookie = new Cookie(name, "");
        cookie.setSecure(true); // Set this to true in production
        cookie.setHttpOnly(true);
        cookie.setMaxAge(0);
        cookie.setPath("/");
        response.addCookie(cookie);
    }
}
```

이 예에서는 [`java-cookie`](https://github.com/jwtk/jjwt) 라이브러리를 사용하여 쿠키를 생성하고 검증했습니다. 쿠키의 `Secure`, `HttpOnly` 및 `MaxAge` 속성도 설정했습니다.

## 참조

* [https://en.wikipedia.org/wiki/HTTP_cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
* [https://tools.ietf.org/html/rfc6265](https://tools.ietf.org/html/rfc6265)
* [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)
* [https://jwt.io/](https://jwt.io/)
* [https://github.com/jwtk/jjwt](https://github.com/jwtk/jjwt)
* [https://github.com/jwtk/java-cookie](https://github.com/jwtk/java-cookie)