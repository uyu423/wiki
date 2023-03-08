---
title: Django
description: 
published: true
date: 2023-03-02T01:32:37.508Z
tags: 
editor: markdown
dateCreated: 2023-03-02T01:32:29.956Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Django***English** document is available*](/en/Knowledge-base/Dictionary/django)
{.links-list}


# 개요
Django는 Python으로 작성된 오픈 소스 웹 애플리케이션 프레임워크입니다. 개발자가 짧은 시간에 복잡한 데이터베이스 기반 웹 사이트를 만들 수 있도록 설계되었습니다. Instagram, Pinterest 및 The Washington Post를 포함하여 세계에서 가장 인기 있는 일부 웹사이트에서 사용됩니다.

# 설명
Django는 웹 애플리케이션의 신속한 개발을 가능하게 하는 Python 기반 웹 프레임워크입니다. Adrian Holovaty와 Simon Willison이 2003년에 만들었으며 Django Software Foundation에서 관리합니다. Django는 MVC(Model-View-Controller) 프레임워크입니다. 즉, 애플리케이션을 데이터를 처리하는 모델 계층, 사용자 인터페이스 디자인을 처리하는 보기 계층 응용 프로그램의 논리를 처리하는 컨트롤러 계층입니다.

Django는 웹 개발에 적합한 다양한 기능을 제공합니다. 여기에는 개발자가 SQL 쿼리를 작성하지 않고도 데이터베이스와 상호 작용할 수 있도록 하는 ORM(개체 관계형 매퍼)이 포함됩니다. 또한 개발자가 최소한의 노력으로 HTML 템플릿을 만들 수 있는 템플릿 엔진을 제공합니다. 또한 Django에는 개발자가 사용자 계정을 관리할 수 있는 인증 시스템이 있습니다.

Django는 또한 확장성이 뛰어납니다. 여기에는 응용 프로그램에 추가 기능을 추가하는 데 사용할 수 있는 타사 패키지의 대규모 라이브러리가 포함됩니다. 또한 Django는 PostgreSQL, MySQL 및 SQLite를 비롯한 광범위한 데이터베이스를 지원합니다.

# 특징
* 객체 관계형 매퍼(ORM)
* 템플릿 엔진
* 인증 시스템
* URL 라우팅
* 국제화
* 데이터베이스 지원
* 타사 패키지
* 보안 기능

# 예
다음은 "Hello World"라는 텍스트가 있는 웹 페이지를 표시하는 Django 애플리케이션의 간단한 예입니다.

먼저 새 Django 프로젝트를 만듭니다.

```
$ django-admin startproject hello_world
```

다음으로 `hello_world/views.py` 파일에 새 보기를 만듭니다.

```
from django.http import HttpResponse

def hello_world(request):
    return HttpResponse("Hello World")
```

마지막으로 `hello_world/urls.py` 파일에 새 URL 패턴을 만듭니다.

```
from django.urls import path
from .views import hello_world

urlpatterns = [
    path('', hello_world, name='hello_world'),
]
```

# 장점과 단점

## 장점
* 배우기 쉽고 사용하기 쉽습니다.
* 높은 확장성
* 광범위한 데이터베이스 지원
* 보안 기능

## 단점
* 디버깅이 어려울 수 있음
* 모바일 장치에 대한 제한된 지원
* 고성능 애플리케이션에는 적합하지 않음