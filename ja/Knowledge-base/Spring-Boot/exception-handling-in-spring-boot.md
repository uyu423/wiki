---
title: Spring Boot での例外処理
description: 
published: true
date: 2023-01-31T05:17:23.760Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:17:22.157Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Exception Handling in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-in-spring-boot)
{.links-list}




# Spring Bootの例外処理

Spring Bootアプリケーションを開発するときは、強力な例外処理メカニズムを持つことが重要です。これにより、アプリケーションは実行時に発生する可能性のある予期しないエラーを正常に処理できます。

Spring Bootアプリケーションで発生する可能性がある2種類のエラーがあります。
- アプリケーション自体で発生する例外です。
- 基本システムまたはフレームワークで発生する例外。

Spring Bootアプリケーションでは、両方のタイプの例外を処理することが重要です。

## アプリケーション例外の例外処理

アプリケーション例外は、アプリケーション自体で発生する例外です。これらのエラーは通常、アプリケーションが期待して適切に処理できるエラーです。

たとえば、ユーザーアカウントを作成するためのRestControllerエンドポイントを持つSpring Bootアプリケーションを考えます。アプリケーションが無効な電子メールアドレスでユーザーアカウントを作成するように要求された場合は、BadRequestExceptionが発生する必要があります。

```java
@RestController
public class UserController {

    @PostMapping("/users")
    public User createUser(@Valid @RequestBody User user) {
        // logic to create user
    }
}
```

上記の例では、リクエスト本文に提供されているメールアドレスが無効な場合、アプリケーションで BadRequestException が発生します。

 この例外を処理するには、 @ControllerAdvice と @ExceptionHandler を使用できます。 @ControllerAdviceアノテーションは、アプリケーション内のすべてのコントローラのグローバル例外ハンドラを定義するために使用されます。 @ExceptionHandlerアノテーションは、メソッドによって処理される例外の種類を指定するために使用されます。

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ExceptionHandler(BadRequestException.class)
    public void handleBadRequestException(BadRequestException e) {
        // exception handling logic
    }
}
```

上記の例では、handleBadRequestException（）メソッドは、アプリケーションのコントローラでBadRequestExceptionが発生したときに呼び出されます。このメソッドで例外処理ロジックを定義できます。

@ControllerAdviceの代わりに@RestControllerAdviceを定義することも可能です。これにより、例外ハンドラがステータスコードの代わりに応答本文を返すことができます。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ResponseBody
    @ExceptionHandler(BadRequestException.class)
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    public Map<String, String> handleBadRequestException(BadRequestException e) {
        Map<String, String> response = new HashMap<>();
        response.put("error", "Invalid email address");
        return response;
    }
}
```

上記の例では、handleBadRequestException() メソッドは、アプリケーションのコントローラで BadRequestException が発生すると、エラーメッセージとともに応答本文を返します。

## システム例外の例外処理

システム例外は、基本システムまたはフレームワークで発生する例外です。これは通常、アプリケーションで予期できない予期しないエラーです。

たとえば、JDBCデータベースを使用するSpring Bootアプリケーションを考えてみます。データベースが利用できない場合、アプリケーションはDataAccessExceptionをスローします。

この例外を処理するには、 @ControllerAdvice と @ExceptionHandler を使用できます。

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    @ExceptionHandler(DataAccessException.class)
    public void handleDataAccessException(DataAccessException e) {
        // exception handling logic
    }
}
```

上記の例では、handleDataAccessException（）メソッドは、アプリケーションのコントローラでDataAccessExceptionが発生したときに呼び出されます。このメソッドで例外処理ロジックを定義できます。

@ControllerAdviceの代わりに@RestControllerAdviceを使用することも可能です。これにより、例外ハンドラがステータスコードの代わりに応答本文を返すことができます。

```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ResponseBody
    @ExceptionHandler(DataAccessException.class)
    @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
    public Map<String, String> handleDataAccessException(DataAccessException e) {
        Map<String, String> response = new HashMap<>();
        response.put("error", "Database unavailable");
        return response;
    }
}
```

上記の例では、handleDataAccessException（）メソッドは、アプリケーションのコントローラでDataAccessExceptionが発生したときにエラーメッセージとともに応答本文を返します。