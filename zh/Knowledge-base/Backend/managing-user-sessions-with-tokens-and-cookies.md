---
title: 使用令牌和 Cookie 管理用户会话
description: 
published: true
date: 2023-02-17T18:16:25.356Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:57:34.473Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Managing User Sessions with Tokens and Cookies***English** version of this document is available*](/en/Knowledge-base/Backend/managing-user-sessions-with-tokens-and-cookies)
{.links-list}



# 使用令牌和 Cookie 管理用户会话

Cookie 和令牌是用于管理用户会话的两种机制。在本文中，我们将讨论两者之间的区别以及如何在 Web 应用程序中实现它们。

## 饼干

Cookie 是存储在用户计算机上的小块数据。它们随每个请求一起发送到服务器，可用于存储有关用户会话的信息。

有两种类型的 cookie：

* **会话 cookies**：这些是临时 cookie，会在用户关闭浏览器时删除。它们通常用于存储当前会话所需的信息，例如会话 ID。

* **持久性 cookies**：这些 cookie 会在用户的计算机上存储一段时间。它们通常用于存储未来会话所需的信息，例如用户 ID。

Cookie 通常存储在 HTTP 请求的“cookie”标头中。 `Set-Cookie` 标头用于在用户计算机上设置 cookie。

## 代币

令牌是用于表示用户身份的字符串。它们通常由服务器生成并发送到存储它们的客户端。然后将它们与每个请求一起发送回服务器。

令牌可用于存储有关用户会话的信息，例如会话 ID。然而，它们不限于此。它们还可以用于存储有关用户身份的信息，例如用户 ID。

有两种类型的令牌：

* **明文令牌**：这些是未加密的令牌。它们很容易生成，但也很容易伪造。

* **加密令牌**：这些是加密的令牌。它们更难生成，但也更难伪造。

令牌通常存储在 HTTP 请求的“授权”标头中。 `Bearer` 令牌是最常见的令牌类型。

## 实施代币

有很多方法可以实现令牌。下面是一个例子：

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

在此示例中，我们使用了 [`java-jwt`](https://github.com/jwtk/jjwt) 库来生成和验证令牌。我们还使用了 [`HMAC256`](https://en.wikipedia.org/wiki/HMAC) 算法来加密令牌。

## 实施 Cookie

有许多方法可以实现 cookie。下面是一个例子：

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

在此示例中，我们使用了 [`java-cookie`](https://github.com/jwtk/jjwt) 库来生成和验证 cookie。我们还设置了 cookie 的“Secure”、“HttpOnly”和“MaxAge”属性。

## 参考

* [https://en.wikipedia.org/wiki/HTTP_cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
* [https://tools.ietf.org/html/rfc6265](https://tools.ietf.org/html/rfc6265)
* [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)
* [https://jwt.io/](https://jwt.io/)
* [https://github.com/jwtk/jjwt](https://github.com/jwtk/jjwt)
* [https://github.com/jwtk/java-cookie](https://github.com/jwtk/java-cookie)