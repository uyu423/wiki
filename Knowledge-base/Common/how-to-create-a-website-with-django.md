---
title: Django로 웹 사이트를 만드는 방법
description: 
published: true
date: 2023-02-02T22:58:21.277Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:58:16.458Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Create a Website with Django***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-website-with-django)
{.links-list}


# Django로 웹사이트를 만드는 방법

Django는 Python으로 작성된 고급 웹 프레임워크로 신속한 개발과 깨끗하고 실용적인 디자인을 장려합니다. 숙련된 개발자가 구축하여 웹 개발의 번거로움을 상당 부분 처리하므로 바퀴를 다시 발명할 필요 없이 앱 작성에 집중할 수 있습니다. 무료이며 오픈 소스입니다.

Django는 최신 웹 애플리케이션을 개발하는 데 탁월한 선택입니다. 많은 일반적인 웹 개발 작업을 훨씬 쉽게 만들어주는 배터리 포함 프레임워크입니다.

## 장고란?

Django는 개발 환경 설정, 종속성 관리 등의 번거로움 없이 웹 애플리케이션을 빠르게 만들 수 있는 Python 기반 웹 프레임워크입니다.

Django에는 다음과 같은 많은 내장 기능이 포함되어 있습니다.

- 데이터베이스와 상호 작용하기 위한 ORM
- HTML 페이지 생성을 위한 템플릿 시스템
- Python 기반 웹 서버
- 양식 시스템
- 인증 시스템

Django는 또한 매우 확장 가능합니다. Django 웹 애플리케이션에 추가 기능을 추가하는 데 사용할 수 있는 많은 타사 패키지가 있습니다.

## 왜 장고를 사용하는가?

Django는 여러 가지 이유로 훌륭한 선택입니다. 많은 일반적인 웹 개발 작업을 훨씬 쉽게 만들어주는 배터리 포함 프레임워크입니다.

Django 사용의 이점 중 일부는 다음과 같습니다.

- Django는 웹 개발의 많은 번거로움을 처리하므로 앱 작성에 집중할 수 있습니다.
- Django에는 ORM, 템플릿 시스템, Python 기반 웹 서버와 같은 많은 내장 기능이 있습니다.
- Django는 매우 확장 가능합니다. Django 웹 애플리케이션에 추가 기능을 추가하는 데 사용할 수 있는 많은 타사 패키지가 있습니다.
- Django는 오픈 소스이며 무료입니다.

## Django와 다른 프레임워크 비교

Python에 사용할 수 있는 다양한 웹 프레임워크가 있습니다. 그렇다면 왜 Django를 사용해야 할까요?

다음은 Django가 좋은 선택이 될 수 있는 몇 가지 이유입니다.

- 배터리가 포함된 프레임워크를 원하는 경우: Django에는 ORM, 템플릿 시스템 및 Python 기반 웹 서버와 같은 많은 내장 기능이 포함되어 있습니다.
- 확장 가능한 프레임워크를 원하는 경우: Django는 매우 확장 가능합니다. Django 웹 애플리케이션에 추가 기능을 추가하는 데 사용할 수 있는 많은 타사 패키지가 있습니다.
- 오픈 소스이며 무료인 프레임워크를 원하는 경우: Django는 오픈 소스이며 무료입니다.

## 장고 시작하기

이제 Django가 무엇이고 왜 사용하고 싶은지 알았으니 Django 웹 애플리케이션을 설정하는 과정을 살펴보겠습니다.

### 개발 환경 설정

가장 먼저 해야 할 일은 개발 환경을 설정하는 것입니다. virtualenv를 사용하여 격리된 개발 환경을 만드는 것이 좋습니다.

virtualenv를 설치하려면 다음 명령을 실행하십시오.

```
pip install virtualenv
```

virtualenv가 설치되면 다음 명령을 실행하여 새 가상 환경을 만들 수 있습니다.

```
virtualenv myproject
```

이렇게 하면 격리된 Python 개발 환경을 포함하는 myproject라는 새 디렉터리가 생성됩니다.

가상 환경을 활성화하려면 다음 명령을 실행합니다.

```
source myproject/bin/activate
```

이제 시스템에 전체적으로 설치된 패키지에 영향을 주지 않고 가상 환경에 패키지를 설치할 수 있습니다.

### 장고 설치하기

개발 환경이 설정되면 Django를 설치할 수 있습니다. Django를 설치하려면 다음 명령을 실행합니다.

```
pip install django
```

이렇게 하면 Django와 필요한 모든 종속성이 설치됩니다.

### Django 프로젝트 만들기

이제 Django가 설치되었으므로 새 Django 프로젝트를 만들 수 있습니다. 이렇게 하려면 다음 명령을 실행합니다.

```
django-admin startproject myproject
```

그러면 Django 프로젝트용 파일이 포함된 myproject라는 새 디렉토리가 생성됩니다.

### Django 개발 서버 실행하기

이제 Django 프로젝트가 있으므로 Django 개발 서버를 시작할 수 있습니다. 이렇게 하려면 다음 명령을 실행합니다.

```
python manage.py runserver
```

이렇게 하면 Django 개발 서버가 시작되고 Django 프로젝트를 http://127.0.0.1:8000/에서 사용할 수 있습니다.

## 장고 URL

Django 웹 애플리케이션의 가장 중요한 부분 중 하나는 URL 구성입니다. URL 구성은 Django가 들어오는 URL과 일치시키는 데 사용할 패턴 집합입니다.

URL 구성의 각 패턴은 보기 기능에 매핑됩니다. 사용자가 패턴과 일치하는 URL을 요청하면 Django는 해당 보기 기능을 호출하고 결과를 반환합니다.

예를 들어 다음 URL 구성을 고려하십시오.

```
urlpatterns = [
    url(r'^

이 URL 구성에는 두 가지 패턴이 있습니다. 첫 번째 패턴은 빈 문자열과 일치하고 뷰 함수 myapp.views.home에 매핑합니다. 두 번째 패턴은 'about/' 문자열과 일치하고 이를 뷰 함수 myapp.views.about에 매핑합니다.

보기 함수는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

## 장고 뷰

뷰는 Django 웹 애플리케이션의 핵심입니다. 보기는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

보기 함수는 Python 함수에서 수행할 수 있는 모든 작업을 수행할 수 있습니다. 즉, 데이터베이스의 데이터에 액세스하고 계산을 수행하는 등의 작업을 수행할 수 있습니다.

유일한 규칙은 HttpResponse 개체를 반환해야 한다는 것입니다.

## 장고 템플릿

Django 웹 애플리케이션의 가장 중요한 부분 중 하나는 템플릿 시스템입니다. 템플릿 시스템은 HTML 페이지를 렌더링하는 데 사용됩니다.

Django에는 Jinja2 템플릿 엔진에서 사용되는 것과 유사한 템플릿 시스템이 내장되어 있습니다.

Django 템플릿 시스템을 사용하려면 먼저 템플릿을 생성해야 합니다. 템플릿은 Django 웹 페이지의 HTML을 포함하는 파일입니다.

다음은 'Hello, world!'라는 문자열만 포함하는 간단한 템플릿입니다.

```
{% extends 'base.html' %}

{% block content %}
Hello, world!
{% endblock %}
```

템플릿을 만든 후에는 render() 함수를 사용하여 템플릿을 렌더링할 수 있습니다. render() 함수는 템플릿 이름과 컨텍스트 데이터 사전을 사용합니다.

다음은 방금 만든 템플릿을 렌더링하는 방법의 예입니다.

```
from django.shortcuts import render

def home(request):
    return render(request, 'home.html', {})
```

## 장고 양식

Django는 HTML 양식을 쉽게 만들 수 있는 내장 양식 시스템과 함께 제공됩니다.

Django 양식 시스템을 사용하려면 먼저 양식을 만들어야 합니다. 양식은 HTML 양식 요소로 렌더링될 필드를 정의하는 Python 클래스입니다.

다음은 하나의 텍스트 필드만 있는 간단한 양식입니다.

```
from django import forms

class MyForm(forms.Form):
    myfield = forms.CharField(max_length=100)
```

양식을 만든 후에는 {% form %} 태그를 사용하여 템플릿에서 렌더링할 수 있습니다.

{% form %} 태그는 양식 개체를 첫 번째 인수로 사용하고 컨텍스트 데이터 사전을 두 번째 인수로 사용합니다.

다음은 방금 만든 양식을 렌더링하는 방법의 예입니다.

```
{% form form %}
    {{ form.myfield }}
{% endform %}
```

## 장고 모델

Django는 데이터베이스의 데이터 작업을 쉽게 해주는 모델 시스템이 내장되어 있습니다.

Django 모델 시스템을 사용하려면 먼저 모델을 생성해야 합니다. 모델은 데이터 개체의 필드와 동작을 정의하는 Python 클래스입니다.

다음은 단일 필드만 있는 간단한 모델입니다.

```
from django.db import models

class MyModel(models.Model):
    myfield = models.CharField(max_length=100)
```

모델을 만든 후에는 Django 관리자를 사용하여 개체를 추가, 편집 및 삭제할 수 있습니다.

또한 Django 모델 API를 사용하여 데이터베이스를 쿼리하고 객체를 생성, 업데이트 및 삭제할 수 있습니다.

## 장고 관리자

Django에는 데이터베이스의 데이터를 쉽게 관리할 수 있는 관리 시스템이 내장되어 있습니다.

Django 관리자를 사용하려면 먼저 관리자 사용자를 생성해야 합니다. 관리자 사용자는 Django 관리자에 액세스할 수 있는 권한이 부여된 사용자입니다.

관리 사용자를 만들려면 다음 명령을 실행합니다.

```
python manage.py createsuperuser
```

관리자 사용자를 만든 후에는 http://127.0.0.1:8000/admin/으로 이동하여 Django 관리자에 로그인할 수 있습니다.

로그인하면 Django 관리 인터페이스가 표시됩니다. 여기에서 개체를 추가, 편집 및 삭제할 수 있습니다.

## 결론

Django는 최신 웹 애플리케이션을 개발하는 데 탁월한 선택입니다. 많은 일반적인 웹 개발 작업을 훨씬 쉽게 만들어주는 배터리 포함 프레임워크입니다.

Django를 처음 사용하는 경우 Django 설명서를 확인하는 것이 좋습니다. Django 프레임워크의 모든 기능에 대해 배울 수 있는 훌륭한 리소스입니다., 'myapp.views.home'),
    url(r'^about/

이 URL 구성에는 두 가지 패턴이 있습니다. 첫 번째 패턴은 빈 문자열과 일치하고 뷰 함수 myapp.views.home에 매핑합니다. 두 번째 패턴은 'about/' 문자열과 일치하고 이를 뷰 함수 myapp.views.about에 매핑합니다.

보기 함수는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
django.http 가져오기 HttpResponse에서

데프 홈(요청):
    return HttpResponse('Hello, world!')
```

## 장고 뷰

뷰는 Django 웹 애플리케이션의 핵심입니다. 보기는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
django.http 가져오기 HttpResponse에서

데프 홈(요청):
    return HttpResponse('Hello, world!')
```

보기 함수는 Python 함수에서 수행할 수 있는 모든 작업을 수행할 수 있습니다. 즉, 데이터베이스의 데이터에 액세스하고 계산을 수행하는 등의 작업을 수행할 수 있습니다.

유일한 규칙은 HttpResponse 개체를 반환해야 한다는 것입니다.

## 장고 템플릿

Django 웹 애플리케이션의 가장 중요한 부분 중 하나는 템플릿 시스템입니다. 템플릿 시스템은 HTML 페이지를 렌더링하는 데 사용됩니다.

Django에는 Jinja2 템플릿 엔진에서 사용되는 것과 유사한 템플릿 시스템이 내장되어 있습니다.

Django 템플릿 시스템을 사용하려면 먼저 템플릿을 생성해야 합니다. 템플릿은 Django 웹 페이지의 HTML을 포함하는 파일입니다.

다음은 'Hello, world!'라는 문자열만 포함하는 간단한 템플릿입니다.

```
{% 확장 'base.html' %}

{% 블록 콘텐츠 %}
안녕, 세상!
{% 엔드블록 %}
```

템플릿을 만든 후에는 render() 함수를 사용하여 템플릿을 렌더링할 수 있습니다. render() 함수는 템플릿 이름과 컨텍스트 데이터 사전을 사용합니다.

다음은 방금 만든 템플릿을 렌더링하는 방법의 예입니다.

```
django.shortcuts 가져오기 렌더링에서

데프 홈(요청):
    렌더링 반환(요청, 'home.html', {})
```

## 장고 양식

Django는 HTML 양식을 쉽게 만들 수 있는 내장 양식 시스템과 함께 제공됩니다.

Django 양식 시스템을 사용하려면 먼저 양식을 만들어야 합니다. 양식은 HTML 양식 요소로 렌더링될 필드를 정의하는 Python 클래스입니다.

다음은 하나의 텍스트 필드만 있는 간단한 양식입니다.

```
django 가져오기 양식에서

클래스 MyForm(forms.Form):
    myfield = forms.CharField(max_length=100)
```

양식을 만든 후에는 {% form %} 태그를 사용하여 템플릿에서 렌더링할 수 있습니다.

{% form %} 태그는 양식 개체를 첫 번째 인수로 사용하고 컨텍스트 데이터 사전을 두 번째 인수로 사용합니다.

다음은 방금 만든 양식을 렌더링하는 방법의 예입니다.

```
{% 양식 양식 %}
    {{ form.myfield }}
{% 엔드폼 %}
```

## 장고 모델

Django는 데이터베이스의 데이터 작업을 쉽게 해주는 모델 시스템이 내장되어 있습니다.

Django 모델 시스템을 사용하려면 먼저 모델을 생성해야 합니다. 모델은 데이터 개체의 필드와 동작을 정의하는 Python 클래스입니다.

다음은 단일 필드만 있는 간단한 모델입니다.

```
django.db 가져오기 모델에서

클래스 MyModel(모델.모델):
    myfield = models.CharField(max_length=100)
```

모델을 만든 후에는 Django 관리자를 사용하여 개체를 추가, 편집 및 삭제할 수 있습니다.

또한 Django 모델 API를 사용하여 데이터베이스를 쿼리하고 객체를 생성, 업데이트 및 삭제할 수 있습니다.

## 장고 관리자

Django에는 데이터베이스의 데이터를 쉽게 관리할 수 있는 관리 시스템이 내장되어 있습니다.

Django 관리자를 사용하려면 먼저 관리자 사용자를 생성해야 합니다. 관리자 사용자는 Django 관리자에 액세스할 수 있는 권한이 부여된 사용자입니다.

관리 사용자를 만들려면 다음 명령을 실행합니다.

```
python manage.py createsuperuser
```

관리자 사용자를 만든 후에는 http://127.0.0.1:8000/admin/으로 이동하여 Django 관리자에 로그인할 수 있습니다.

로그인하면 Django 관리 인터페이스가 표시됩니다. 여기에서 개체를 추가, 편집 및 삭제할 수 있습니다.

## 결론

Django는 최신 웹 애플리케이션을 개발하는 데 탁월한 선택입니다. 많은 일반적인 웹 개발 작업을 훨씬 쉽게 만들어주는 배터리 포함 프레임워크입니다.

Django를 처음 사용하는 경우 Django 설명서를 확인하는 것이 좋습니다. Django 프레임워크의 모든 기능에 대해 배울 수 있는 훌륭한 리소스입니다., 'myapp.views.about'),
]
```

이 URL 구성에는 두 가지 패턴이 있습니다. 첫 번째 패턴은 빈 문자열과 일치하고 뷰 함수 myapp.views.home에 매핑합니다. 두 번째 패턴은 'about/' 문자열과 일치하고 이를 뷰 함수 myapp.views.about에 매핑합니다.

보기 함수는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
django.http 가져오기 HttpResponse에서

데프 홈(요청):
    return HttpResponse('Hello, world!')
```

## 장고 뷰

뷰는 Django 웹 애플리케이션의 핵심입니다. 보기는 HttpRequest 개체를 첫 번째 인수로 사용하고 HttpResponse 개체를 반환하는 Python 함수입니다.

다음은 'Hello, world!'라는 문자열이 포함된 HttpResponse 객체를 반환하는 간단한 보기 함수입니다.

```
django.http 가져오기 HttpResponse에서

데프 홈(요청):
    return HttpResponse('Hello, world!')
```

보기 함수는 Python 함수에서 수행할 수 있는 모든 작업을 수행할 수 있습니다. 즉, 데이터베이스의 데이터에 액세스하고 계산을 수행하는 등의 작업을 수행할 수 있습니다.

유일한 규칙은 HttpResponse 개체를 반환해야 한다는 것입니다.

## 장고 템플릿

Django 웹 애플리케이션의 가장 중요한 부분 중 하나는 템플릿 시스템입니다. 템플릿 시스템은 HTML 페이지를 렌더링하는 데 사용됩니다.

Django에는 Jinja2 템플릿 엔진에서 사용되는 것과 유사한 템플릿 시스템이 내장되어 있습니다.

Django 템플릿 시스템을 사용하려면 먼저 템플릿을 생성해야 합니다. 템플릿은 Django 웹 페이지의 HTML을 포함하는 파일입니다.

다음은 'Hello, world!'라는 문자열만 포함하는 간단한 템플릿입니다.

```
{% 확장 'base.html' %}

{% 블록 콘텐츠 %}
안녕, 세상!
{% 엔드블록 %}
```

템플릿을 만든 후에는 render() 함수를 사용하여 템플릿을 렌더링할 수 있습니다. render() 함수는 템플릿 이름과 컨텍스트 데이터 사전을 사용합니다.

다음은 방금 만든 템플릿을 렌더링하는 방법의 예입니다.

```
django.shortcuts 가져오기 렌더링에서

데프 홈(요청):
    렌더링 반환(요청, 'home.html', {})
```

## 장고 양식

Django는 HTML 양식을 쉽게 만들 수 있는 내장 양식 시스템과 함께 제공됩니다.

Django 양식 시스템을 사용하려면 먼저 양식을 만들어야 합니다. 양식은 HTML 양식 요소로 렌더링될 필드를 정의하는 Python 클래스입니다.

다음은 하나의 텍스트 필드만 있는 간단한 양식입니다.

```
django 가져오기 양식에서

클래스 MyForm(forms.Form):
    myfield = forms.CharField(max_length=100)
```

양식을 만든 후에는 {% form %} 태그를 사용하여 템플릿에서 렌더링할 수 있습니다.

{% form %} 태그는 양식 개체를 첫 번째 인수로 사용하고 컨텍스트 데이터 사전을 두 번째 인수로 사용합니다.

다음은 방금 만든 양식을 렌더링하는 방법의 예입니다.

```
{% 양식 양식 %}
    {{ form.myfield }}
{% 엔드폼 %}
```

## 장고 모델

Django는 데이터베이스의 데이터 작업을 쉽게 해주는 모델 시스템이 내장되어 있습니다.

Django 모델 시스템을 사용하려면 먼저 모델을 생성해야 합니다. 모델은 데이터 개체의 필드와 동작을 정의하는 Python 클래스입니다.

다음은 단일 필드만 있는 간단한 모델입니다.

```
django.db 가져오기 모델에서

클래스 MyModel(모델.모델):
    myfield = models.CharField(max_length=100)
```

모델을 만든 후에는 Django 관리자를 사용하여 개체를 추가, 편집 및 삭제할 수 있습니다.

또한 Django 모델 API를 사용하여 데이터베이스를 쿼리하고 객체를 생성, 업데이트 및 삭제할 수 있습니다.

## 장고 관리자

Django에는 데이터베이스의 데이터를 쉽게 관리할 수 있는 관리 시스템이 내장되어 있습니다.

Django 관리자를 사용하려면 먼저 관리자 사용자를 생성해야 합니다. 관리자 사용자는 Django 관리자에 액세스할 수 있는 권한이 부여된 사용자입니다.

관리 사용자를 만들려면 다음 명령을 실행합니다.

```
python manage.py createsuperuser
```

관리자 사용자를 만든 후에는 http://127.0.0.1:8000/admin/으로 이동하여 Django 관리자에 로그인할 수 있습니다.

로그인하면 Django 관리 인터페이스가 표시됩니다. 여기에서 개체를 추가, 편집 및 삭제할 수 있습니다.

## 결론

Django는 최신 웹 애플리케이션을 개발하는 데 탁월한 선택입니다. 많은 일반적인 웹 개발 작업을 훨씬 쉽게 만들어주는 배터리 포함 프레임워크입니다.

Django를 처음 사용하는 경우 Django 설명서를 확인하는 것이 좋습니다. Django 프레임워크의 모든 기능에 대해 배울 수 있는 훌륭한 리소스입니다.