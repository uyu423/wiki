---
title: 070: Thymeleaf를 사용한 Spring Boot: 동적 템플릿 생성
description: 
published: true
date: 2023-02-05T04:32:34.709Z
tags: 
editor: markdown
dateCreated: 2023-02-05T04:32:32.921Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [070: Spring Boot with Thymeleaf: Creating Dynamic Templates***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}


# 070: Thymeleaf를 사용한 Spring Boot: 동적 템플릿 생성

이 게시물에서는 Spring Boot와 함께 Thymeleaf 템플릿 엔진을 사용하여 동적 HTML 페이지를 만드는 방법을 살펴보겠습니다.

Thymeleaf는 Spring MVC와 함께 사용하여 우아하고 동적인 웹 애플리케이션을 생성할 수 있는 인기 있는 템플릿 엔진입니다. Thymeleaf의 주요 목표는 개발 환경에 자연스러운 템플릿을 가져오는 것입니다.

## 타임리프란?

Thymeleaf는 XML 및 HTML 작업을 위한 일련의 도구를 제공하는 Java 기반 라이브러리입니다. Thymeleaf의 주요 목표는 개발 환경에 자연스러운 템플릿을 가져오는 것입니다.

템플릿에 대한 Thymeleaf의 접근 방식은 다른 템플릿 엔진에서 취하는 전통적인 접근 방식과 다릅니다. Thymeleaf를 사용하면 템플릿이 단순히 데이터로 "채워지는" 것이 아닙니다. 대신 Thymeleaf 템플릿이 처리되어 유효한 HTML 문서로 변환됩니다.

이는 Thymeleaf 템플릿을 웹 애플리케이션 UI의 시작점으로 사용할 수 있고 애플리케이션의 백엔드와 쉽게 통합할 수 있음을 의미합니다.

## 시작하기

Thymeleaf를 시작하려면 프로젝트의 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf</artifactId>
    <version>3.0.9.RELEASE</version>
</dependency>
```

## 안녕하세요, 타임리프님!

이제 Thymeleaf를 설정했으므로 간단한 템플릿을 만들어 실제로 작동하는지 살펴보겠습니다.

`src/main/resources/templates` 디렉토리에 `hello.html`이라는 새 파일을 만들고 다음 콘텐츠를 추가합니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, Thymeleaf!</title>
</head>
<body>
    <h1>Hello, Thymeleaf!</h1>
</body>
</html>
```

이 템플릿에는 "Hello, Thymeleaf!"라는 간단한 `<h1>` 요소가 포함되어 있습니다.

다음으로 이 템플릿을 렌더링할 Spring Boot 애플리케이션을 만들어 보겠습니다.

`src/main/java` 디렉토리에 `Application.java`라는 새 파일을 만들고 다음 내용을 추가합니다.

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

이것은 기본 Spring Boot 애플리케이션입니다. `@SpringBootApplication` 주석은 애플리케이션 클래스를 Spring Boot 애플리케이션으로 표시하는 데 사용됩니다.

다음으로 `hello.html` 템플릿을 렌더링할 컨트롤러를 생성해 보겠습니다.

`src/main/java` 디렉토리에 `HelloController.java`라는 새 파일을 만들고 다음 내용을 추가합니다.

```java
@Controller
public class HelloController {

    @RequestMapping("/")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, Thymeleaf!");
        return "hello";
    }

}
```

이 컨트롤러에는 단일 `@RequestMapping` 주석 메서드가 있습니다. 이 메서드는 `/` URL을 `hello` 템플릿에 매핑합니다.

`hello` 템플릿은 모델에 `message` 속성이 있어야 합니다. 이 속성은 `hello` 메소드에 의해 모델에 추가됩니다.

이제 컨트롤러와 템플릿이 설정되었으므로 애플리케이션을 실행하고 결과를 확인하겠습니다.

Java 애플리케이션으로 `Application` 클래스를 실행하고 브라우저에서 http://localhost:8080으로 이동합니다. 다음 출력이 표시되어야 합니다.

![안녕, 타임리프!](https://i.imgur.com/ePcUg9x.png)

보시다시피 템플릿이 렌더링되었고 `message` 속성이 `<h1>` 요소를 채우는 데 사용되었습니다.

## 템플릿에 데이터 전달

이전 섹션에서는 `Model` 개체를 사용하여 템플릿에 데이터를 전달하는 방법을 살펴보았습니다.

`Model` 개체는 템플릿에 전달해야 하는 데이터를 저장하는 데 사용할 수 있는 지도와 유사한 구조입니다.

Thymeleaf는 `Model` 객체 외에도 `Context` 객체도 제공합니다. `Context` 객체는 유형 안전성 및 국제화 지원과 같은 추가 기능을 제공하는 `Model` 객체의 보다 강력한 버전입니다.

다음 섹션에서 `Context` 개체를 사용하는 방법을 살펴보겠습니다.

## 컨텍스트 개체 사용

이전 섹션에서 본 것처럼 `Model` 개체는 템플릿에 전달해야 하는 데이터를 저장하는 데 사용할 수 있는 지도와 같은 구조입니다.

`Context` 객체는 유형 안전성 및 국제화 지원과 같은 추가 기능을 제공하는 `Model` 객체의 보다 강력한 버전입니다.

`Context` 개체를 사용하려면 프로젝트의 pom.xml 파일에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
    <version>3.0.4.RELEASE</version>
</dependency>
```

이 종속성은 `Context` 개체에 대한 지원을 제공합니다.

다음으로 `Context` 개체를 사용하는 템플릿을 만들어 보겠습니다.

`src/main/resources/templates` 디렉토리에 `context.html`이라는 새 파일을 만들고 다음 콘텐츠를 추가합니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Context Example</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

이 템플릿에는 `Context` 객체의 `message` 속성을 사용하는 `<h1>` 요소가 포함되어 있습니다.

다음으로 이 템플릿을 렌더링할 컨트롤러를 만들어 보겠습니다.

`src/main/java` 디렉토리에 `ContextController.java`라는 새 파일을 만들고 다음 콘텐츠를 추가합니다.

```java
@Controller
public class ContextController {

    @RequestMapping("/")
    public String context(Context context) {
        context.setVariable("message", "Hello, Thymeleaf!");
        return "context";
    }

}
```

이 컨트롤러에는 단일 `@RequestMapping` 주석 메서드가 있습니다. 이 메소드는 `/` URL을 `context` 템플릿에 매핑합니다.

`context` 템플릿은 `Context` 객체에 `message` 속성이 있어야 합니다. 이 속성은 `context` 메서드에 의해 `Context` 개체에 추가됩니다.

이제 컨트롤러와 템플릿이 설정되었으므로 애플리케이션을 실행하고 결과를 확인하겠습니다.

Java 애플리케이션으로 `Application` 클래스를 실행하고 브라우저에서 http://localhost:8080으로 이동합니다. 다음 출력이 표시되어야 합니다.

![안녕, 타임리프!](https://i.imgur.com/ePcUg9x.png)

보시다시피 템플릿이 렌더링되었고 `message` 속성이 `<h1>` 요소를 채우는 데 사용되었습니다.

## 결론

이 게시물에서는 Spring Boot와 함께 Thymeleaf 템플릿 엔진을 사용하여 동적 HTML 페이지를 만드는 방법을 살펴보았습니다.

또한 `Model` 및 `Context` 개체를 사용하여 데이터를 템플릿에 전달하는 방법도 살펴보았습니다.

Thymeleaf는 동적이고 정교한 웹 애플리케이션을 만드는 데 사용할 수 있는 강력한 템플릿 엔진입니다.