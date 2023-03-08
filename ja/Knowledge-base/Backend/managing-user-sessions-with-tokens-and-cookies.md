---
title: トークンと Cookie を使用したユーザー セッションの管理
description: 
published: true
date: 2023-02-17T18:16:24.018Z
tags: 
editor: markdown
dateCreated: 2023-01-31T00:57:34.472Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Managing User Sessions with Tokens and Cookies***English** version of this document is available*](/en/Knowledge-base/Backend/managing-user-sessions-with-tokens-and-cookies)
{.links-list}



#トークンとCookieでユーザーセッションを管理する

Cookieとトークンは、ユーザーセッションを管理するために使用される2つのメカニズムです。この記事では、2つの違いとWebアプリケーションでそれぞれを実装する方法について説明します。

## Cookie

クッキーは、ユーザーのコンピュータに保存される小さなデータの一部です。各要求とともにサーバーに送信され、ユーザーセッションに関する情報を保存するために使用できます。

クッキーには2種類あります。

* **セッションクッキー**：ユーザーがブラウザを閉じたときに削除される一時クッキーです。通常、セッションIDなど、現在のセッションに必要な情報を格納するために使用されます。

* **永続Cookie**：一定期間にわたってユーザーのコンピュータに保存されるCookieです。通常、ユーザーIDなど、将来のセッションに必要な情報を保存するために使用されます。

クッキーは通常、HTTPリクエストの `cookie`ヘッダーに格納されます。 「Set-Cookie」ヘッダーは、ユーザーのコンピューターにCookieを設定するために使用されます。

##トークン

トークンは、ユーザーのIDを表すために使用される文字列です。通常、サーバーで作成され保存されたクライアントに送信されます。その後、各要求とともにサーバーに再送信されます。

トークンは、セッションIDなどのユーザーセッションに関する情報を格納するために使用できます。しかし、これに限定されない。また、ユーザーIDなどのユーザーIDに関する情報を保存するためにも使用できます。

トークンには2つのタイプがあります。

* **一般テキストトークン**: 暗号化されていないトークンです。作成するのは簡単ですが、偽造も簡単です。

* **暗号化されたトークン**: 暗号化されたトークンです。それらは作成するのがより難しいですが、偽造するのも難しいです。

トークンは通常、HTTPリクエストの `Authorization`ヘッダに格納されます。 「Bearer」トークンは最も一般的なタイプのトークンです。

##トークンの実装

トークンを実装する方法はいくつかあります。以下は一例です。

```java
public class TokenService {
    
    public static final String TOKEN_SECRET = "secret";
    
    public static String generateToken(String userId) {
        String token = JWT.create()
                .withSubject(userId)
                .sign（Algorithm.HMAC256（TOKEN_SECRET））;
        return token;
    }
    
    public static String validateToken(String token) {
        try{
            JWT.decode(token).getSubject();
        } catch(JWTDecodeException e) {
            return null;
        }
        return token;
    }
}
```

この例では、[`java-jwt`](https://github.com/jwtk/jjwt) ライブラリを使用してトークンを生成して検証しました。また、[`HMAC256`]（https://en.wikipedia.org/wiki/HMAC）アルゴリズムを使用してトークンを暗号化しました。

## Cookieの実装

Cookieを実装する方法はいくつかあります。以下は一例です。

```java
public class CookieService {
    
    public static void setCookie(HttpServletResponse response, String name, String value) {
        Cookie cookie = new Cookie(name, value);
        cookie.setSecure(true); // Set this to true in production
        cookie.setHttpOnly(true);
        cookie.setMaxAge（3600）; // Set this to a negative value to make the cookie session-only
        cookie.setPath("/");
        response.addCookie（cookie）;
    }
    
    public static Cookie getCookie(HttpServletRequest request, String name) {
        Cookie[] cookies = request.getCookies();
        if(cookies != null) {
            for(Cookie cookie: cookies) {
                if(cookie.getName().equals(name)) {
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
        response.addCookie（cookie）;
    }
}
```

この例では、[`java-cookie`](https://github.com/jwtk/jjwt) ライブラリを使用して Cookie を生成して検証しました。 Cookieの `Secure`、 `HttpOnly`、および `MaxAge`属性も設定しました。

##リファレンス

* [https://en.wikipedia.org/wiki/HTTP_cookie](https://en.wikipedia.org/wiki/HTTP_cookie)
* [https://tools.ietf.org/html/rfc6265](https://tools.ietf.org/html/rfc6265)
* [https://tools.ietf.org/html/rfc6750](https://tools.ietf.org/html/rfc6750)
* [https://jwt.io/](https://jwt.io/)
* [https://github.com/jwtk/jjwt](https://github.com/jwtk/jjwt)
* [https://github.com/jwtk/java-cookie](https://github.com/jwtk/java-cookie)