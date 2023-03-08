---
title: Kotlin 및 Laravel: PHP 프레임워크로 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-18T09:32:42.342Z
tags: 
editor: markdown
dateCreated: 2023-02-18T09:32:40.966Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Laravel: Building a Web Application with a PHP Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-laravel-building-a-web-application-with-a-php-framework)
{.links-list}


# Kotlin 및 Laravel: PHP 프레임워크로 웹 애플리케이션 구축

개발자는 항상 작업 흐름을 개선하고 삶을 더 쉽게 만드는 방법을 찾고 있습니다. Kotlin은 몇 가지 훌륭한 기능을 제공하고 Laravel 프레임워크로 웹 개발에 사용할 수 있는 새로운 프로그래밍 언어입니다.

Kotlin은 JVM, Android 및 브라우저용 정적 유형 프로그래밍 언어입니다. JetBrains에서 개발했으며 지난 몇 년 동안 인기를 얻고 있습니다. Kotlin은 Java와 100% 호환되며 기존 Java 코드와 함께 사용할 수 있습니다. 다른 프레임워크 및 라이브러리와 함께 Kotlin을 사용할 수도 있습니다.

Laravel은 웹 애플리케이션 개발에 널리 사용되는 PHP 프레임워크입니다. 무료이며 오픈 소스이며 성장하는 사용자 커뮤니티가 있습니다. Laravel은 Twitter, Facebook 및 Google을 포함한 많은 대기업에서 사용됩니다.

Kotlin과 Laravel을 함께 사용하여 웹 애플리케이션을 구축할 수 있습니다. 이 기사에서는 Kotlin 및 Laravel 개발 환경을 설정하는 방법과 Laravel 프레임워크를 사용하여 간단한 웹 애플리케이션을 만드는 방법을 살펴봅니다.

## 개발 환경 설정

Kotlin 애플리케이션을 개발하려면 IntelliJ IDEA용 Kotlin 플러그인을 설치해야 합니다. Kotlin 플러그인은 IntelliJ IDEA Ultimate 및 Community 에디션 버전 15 이상과 호환됩니다.

IntelliJ IDEA가 설치되어 있지 않은 경우 [JetBrains 웹사이트](https://www.jetbrains.com/idea/download/)에서 커뮤니티 에디션을 다운로드할 수 있습니다.

IntelliJ IDEA가 설치되면 플러그인 저장소에서 Kotlin 플러그인을 설치할 수 있습니다. 이렇게 하려면 _File_ > _Settings_ > _Plugins_로 이동하여 Kotlin 플러그인을 검색합니다. _설치_를 클릭하여 플러그인을 설치합니다.

![IntelliJ IDEA에 Kotlin 플러그인 설치](https://kotlinlang.org/assets/images/blog/2017-2/kotlin-plugin-intellij-idea.png)

Kotlin 플러그인을 설치한 후 Kotlin 컴파일러를 구성해야 합니다. 이렇게 하려면 _File_ > _Settings_ > _Build, Execution, Deployment_ > _Compiler_로 이동하여 _Kotlin Compiler_를 선택합니다.

![IntelliJ IDEA에서 Kotlin 컴파일러 구성](https://kotlinlang.org/assets/images/blog/2017-2/kotlin-compiler-intellij-idea.png)

최신 버전의 JDK(Java Development Kit)도 설치해야 합니다. Kotlin 컴파일러에는 JDK 8 이상이 필요합니다.

## Kotlin/Laravel 프로젝트 생성

이제 Kotlin/Laravel 프로젝트를 만들 준비가 되었습니다. 이렇게 하려면 IntelliJ IDEA에서 새 프로젝트를 생성하고 _Kotlin/JVM_ 및 _Laravel_ 프로젝트 템플릿을 선택해야 합니다.

![IntelliJ IDEA에서 새 Kotlin/Laravel 프로젝트 만들기](https://kotlinlang.org/assets/images/blog/2017-2/kotlin-laravel-project-intellij-idea.png)

이제 _Project_ 보기에서 프로젝트 구조를 볼 수 있습니다.

![IntelliJ IDEA에서 Kotlin/Laravel 프로젝트의 프로젝트 구조](https://kotlinlang.org/assets/images/blog/2017-2/kotlin-laravel-project-structure-intellij-idea.png)

_app_ 디렉터리에는 웹 애플리케이션용 Kotlin 소스 파일이 포함되어 있습니다. _resources_ 디렉토리에는 웹 응용 프로그램에 대한 HTML 템플릿 및 기타 리소스가 포함되어 있습니다. _public_ 디렉토리에는 CSS 및 JavaScript 파일과 같은 정적 리소스가 포함되어 있습니다.

## 웹 애플리케이션 만들기

이제 웹 애플리케이션을 만들 준비가 되었습니다. 컨트롤러를 만드는 것부터 시작하겠습니다. Kotlin에서 컨트롤러는 애플리케이션 로직을 포함하는 클래스입니다.

컨트롤러를 생성하려면 _app/Http/Controllers_ 디렉토리에 Kotlin 파일을 생성해야 합니다. 파일 이름을 _HelloController.kt_로 지정하고 다음 코드를 추가합니다.

```kotlin
package com.example.helloworld.controllers

import org.springframework.stereotype.Controller
import org.springframework.ui.Model
import org.springframework.web.bind.annotation.GetMapping

@Controller
class HelloController {

    @GetMapping("/hello")
    fun hello(model: Model): String {
        model.addAttribute("message", "Hello, World!")
        return "hello"
    }

}
```

위의 코드에서 단일 작업으로 컨트롤러를 만들었습니다. 작업에는 작업을 _GET_ HTTP 메서드에 매핑하는 _@GetMapping_ 주석이 추가됩니다. 작업은 _Model_ 개체를 매개 변수로 사용하고 여기에 메시지 특성을 추가합니다. message 속성은 hello.html 템플릿에서 사용됩니다.

컨트롤러 작업은 렌더링해야 하는 HTML 템플릿의 이름인 문자열을 반환합니다. 이 경우 템플릿은 _hello.html_이며 _resources/views_ 디렉터리에 있습니다.

이제 _hello.html_ 템플릿에 다음 코드를 추가할 수 있습니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, World!</title>
</head>
<body>
    <h1>{{ message }}</h1>
</body>
</html>
```

템플릿에서 _{{ 메시지 }}_ 표현식을 사용하여 메시지 속성의 값을 출력했습니다.

이제 웹 애플리케이션을 실행하고 _http://localhost:8080/hello_ URL로 이동하여 인사말 메시지를 볼 수 있습니다.

![인사말](https://kotlinlang.org/assets/images/blog/2017-2/kotlin-laravel-hello-world.png)

## 결론

이 기사에서는 Kotlin 및 Laravel 개발 환경을 설정하는 방법과 Laravel 프레임워크를 사용하여 간단한 웹 애플리케이션을 만드는 방법을 살펴보았습니다.

Kotlin과 Laravel을 사용하면 깔끔하고 간결한 코드로 웹 애플리케이션을 만들 수 있습니다. Kotlin은 Java와 100% 호환되므로 기존 Java 코드 및 라이브러리와 함께 Kotlin을 쉽게 사용할 수 있습니다. Laravel은 웹 애플리케이션을 쉽게 만들 수 있는 인기 있는 PHP 프레임워크입니다.

## 더 읽을거리

- [Java 개발자를 위한 Kotlin](https://kotlinlang.org/docs/reference/java-to-kotlin-converter.html)
- [PHP 개발자를 위한 Kotlin](https://kotlinlang.org/docs/reference/php-to-kotlin-converter.html)
- [Laravel 문서](https://laravel.com/docs)