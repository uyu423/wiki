---
title: 008: Thymeleaf로 템플릿 생성 및 사용
description: 
published: true
date: 2023-02-03T08:17:34.749Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:17:33.076Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [008: Creating and using templates with Thymeleaf***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}


# 소개

이 게시물에서는 Thymeleaf로 템플릿을 만들고 사용하는 방법에 대해 설명합니다.

Thymeleaf는 잘 구성되고 구조화된 방식으로 HTML, XML 및 기타 마크업 언어를 생성할 수 있게 해주는 최신 서버 측 Java 템플릿 엔진입니다.

Apache License 2.0에 따라 라이센스가 부여된 오픈 소스 프로젝트입니다.

# 템플릿이란?

템플릿은 웹 사이트 또는 애플리케이션의 정적 부분과 동적 콘텐츠에 대한 자리 표시자 변수를 포함하는 파일입니다.

템플릿 엔진은 정적 템플릿 파일을 가져오고 자리 표시자 변수를 실제 값으로 대체하여 사용자에게 제공할 수 있는 파일을 생성하는 도구입니다.

# 템플릿을 사용하는 이유

템플릿은 웹 사이트 또는 애플리케이션의 정적 부분을 동적 부분에서 분리하는 좋은 방법입니다.

이렇게 분리하면 동적 콘텐츠에 영향을 주지 않고 사이트의 정적 부분을 변경할 수 있을 뿐만 아니라 코드를 더 쉽게 관리할 수 있습니다.

또한 사이트의 정적 부분을 더 쉽게 캐시하여 성능을 향상시킬 수 있습니다.

# 타임리프란?

Thymeleaf는 Java용 템플릿 엔진입니다.

Apache License 2.0에 따라 라이센스가 부여된 오픈 소스 프로젝트입니다.

Thymeleaf를 사용하면 잘 구성되고 구조화된 방식으로 HTML, XML 및 기타 마크업 언어를 만들 수 있습니다.

또한 국제화(i18n) 및 지역화(l10n)에 대한 탁월한 지원을 제공합니다.

Thymeleaf는 Spring MVC, Spring Boot 및 Vaadin과 같은 널리 사용되는 많은 Java 웹 프레임워크에서 사용됩니다.

# 타임리프 구문

Thymeleaf에는 표준 및 OGNL의 두 가지 유형의 구문이 있습니다.

표준 구문은 기본 구문 모드이며 잘 구성되고 구조화된 HTML, XML 및 기타 마크업 언어를 만드는 데 사용됩니다.

OGNL 구문은 표준 구문의 확장이며 Thymeleaf 컨텍스트에서 객체에 액세스하는 데 사용됩니다.

# 템플릿 만들기

모든 텍스트 편집기에서 Thymeleaf 템플릿을 만들 수 있습니다.

이 예에서는 src/main/resources/templates 디렉토리에 "hello.html"이라는 템플릿을 만듭니다.

안녕하세요.html

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello, World!</title>
</head>
<body>
    <p th:text="${message}">Hello, World!</p>
</body>
</html>
```

위의 템플릿에는 템플릿이 처리될 때 값으로 대체될 "message"라는 변수가 있습니다.

# 템플릿 렌더링

ThymeleafTemplateEngine 클래스를 사용하여 Java 애플리케이션에서 Thymeleaf 템플릿을 렌더링할 수 있습니다.

먼저 ThymeleafTemplateEngine 인스턴스를 생성해야 합니다.

```java
ThymeleafTemplateEngine templateEngine = new ThymeleafTemplateEngine();
```

그런 다음 템플릿 이름과 변수 맵을 renderTemplate() 메서드에 전달하여 템플릿을 렌더링할 수 있습니다.

```java
String result = templateEngine.renderTemplate("hello.html", ImmutableMap.of("message", "Hello, World!"));
```

# 결론

이번 포스트에서는 Thymeleaf로 템플릿을 생성하고 사용하는 방법에 대해 알아보았습니다.

또한 Thymeleaf가 지원하는 다양한 유형의 구문에 대해서도 배웠습니다.

Thymeleaf에 대해 자세히 알아보려면 다음 리소스를 확인하십시오.

- 타임리프 홈페이지: https://www.thymeleaf.org/
- Thymeleaf GitHub 리포지토리: https://github.com/thymeleaf/thymeleaf
- Thymeleaf 사용자 가이드: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html