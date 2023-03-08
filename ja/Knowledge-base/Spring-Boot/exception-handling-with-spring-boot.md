---
title: Spring Boot による例外処理
description: 
published: true
date: 2023-02-17T18:04:34.840Z
tags: 
editor: markdown
dateCreated: 2023-01-30T12:32:23.167Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Exception Handling with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exception-handling-with-spring-boot)
{.links-list}

    
    
# Spring Bootで例外を処理する

Spring Bootは例外処理のためのいくつかのユーティリティを提供します。この記事では、最も一般的に使用される技術のいくつかを見てみましょう。

## @ExceptionHandlerで例外を処理する

SpringBootで例外を処理する最も一般的な方法は、@ExceptionHandlerアノテーションを使用することです。このコメントはコントローラメソッドに適用でき、指定された型の例外がコントローラによってスローされたときにメソッドが呼び出されるようにします。

たとえば、次のメソッドを持つコントローラがあるとします。

```java
public class MyController {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

someMethod() メソッドで例外が発生すると、handleException() メソッドが呼び出されます。これは、handleException（）メソッドに@ExceptionHandlerがコメントとして追加され、Exception型の例外を処理できるためです。

@ExceptionHandler でコントローラメソッドに注釈を付け、次のように複数の例外タイプを指定することもできます。

```java
@ExceptionHandler({IOException.class, MyCustomException.class})
public void handleException(Exception e) {
    // ...
}
```

この場合、コントローラでIOExceptionまたはMyCustomExceptionが発生すると、handleException（）メソッドが呼び出されます。

## @ControllerAdviceで例外を処理する

すべてのコントローラに対してグローバルに例外を処理するには、@ControllerAdviceアノテーションを使用できます。このコメントはクラスに適用でき、コントローラで例外が発生したときにクラスのすべてのメソッドが呼び出されるようにします。

たとえば、次のメソッドを持つクラスがあるとします。

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        // ...
    }
}
```

この場合、コントローラで例外が発生するたびにhandleException（）メソッドが呼び出されます。 someMethod() メソッドも呼び出されますが、例外処理には影響しません。

## @RestControllerAdviceで例外を処理する

SpringのRESTサポートを使用している場合は、@RestControllerAdviceアノテーションを使用してすべてのRESTコントローラの例外をグローバルに処理できます。このコメントは@ControllerAdviceに似ていますが、RESTコントローラにのみ適用されます。

たとえば、次のメソッドを持つクラスがあるとします。

```java
@RestControllerAdvice
public class GlobalRestExceptionHandler {
    
    @ExceptionHandler(Exception.class)
    public void handleException(Exception e) {
        // ...
    }
    
    public void someMethod() {
        // ...
    }
}
```

この場合、RESTコントローラで例外が発生するたびにhandleException（）メソッドが呼び出されます。 someMethod() メソッドも呼び出されますが、例外処理には影響しません。

## @ResponseStatusで例外を処理する

例外を特定のHTTPステータスコードにマッピングする場合は、@ResponseStatusアノテーションを使用できます。このコメントはコントローラメソッドに適用でき、メソッドが例外をスローしたときに指定されたHTTPステータスコードが返されるようにします。

たとえば、次のメソッドを持つコントローラがあるとします。

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class MyController {
    
    public void someMethod() {
        throw new Exception("something went wrong");
    }
}
```

この場合、someMethod（）メソッドは例外をスローし、HTTPステータスコード400（無効な要求）がクライアントに返されます。

##結論

例外処理は開発の重要な部分であり、Spring Bootは例外処理のためのいくつかのユーティリティを提供します。この記事では、最も一般的に使用されているいくつかの技術について説明しました。