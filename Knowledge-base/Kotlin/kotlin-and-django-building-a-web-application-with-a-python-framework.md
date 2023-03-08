---
title: Kotlin 및 Django: Python 프레임워크로 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-03T13:56:31.935Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:56:30.207Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Django: Building a Web Application with a Python Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-django-building-a-web-application-with-a-python-framework)
{.links-list}


# 코틀린과 장고: 파이썬 프레임워크로 웹 애플리케이션 만들기

Django는 신속한 개발과 깨끗하고 실용적인 디자인을 장려하는 Python 웹 프레임워크입니다. Django는 무료 오픈 소스이며 웹 개발의 많은 번거로움을 처리하므로 바퀴를 다시 발명할 필요 없이 앱 작성에 집중할 수 있습니다. 배우기도 쉽고 시작하고 실행하는 데 오래 걸리지 않습니다.

Kotlin은 최신 멀티플랫폼 애플리케이션을 위한 정적으로 유형이 지정된 프로그래밍 언어입니다. Kotlin은 Java와 100% 상호 운용 가능하므로 Java에 이미 익숙하다면 Kotlin을 쉽게 시작할 수 있습니다. Kotlin은 또한 Java보다 더 간결하므로 더 적은 코드를 작성하고 더 많은 작업을 수행할 수 있습니다.

이 기사에서는 Django 웹 프레임워크와 Kotlin 프로그래밍 언어를 사용하여 웹 애플리케이션을 빌드하는 방법을 보여줍니다. 개발 환경을 설정하고 새 Django 프로젝트를 만들고 프로젝트에 간단한 페이지를 추가하는 단계를 안내합니다. 이 기사를 마치면 Django와 Kotlin으로 웹 애플리케이션을 구축하는 방법에 대한 기본적인 이해를 갖게 될 것입니다.

## 개발 환경 설정

웹 애플리케이션 구축을 시작하기 전에 개발 환경을 설정해야 합니다. Python을 처음 사용하는 경우 데이터 과학을 위한 가장 인기 있는 Python 패키지가 포함된 Python 배포판인 Anaconda를 사용하는 것이 좋습니다.

Anaconda를 사용하는 경우 다음 명령으로 Django를 설치할 수 있습니다.

```
conda install -c anaconda django
```

Anaconda를 사용하지 않는 경우 pip 패키지 관리자를 사용하여 Django를 설치할 수 있습니다.

```
pip install django
```

다음 명령을 실행하여 Django가 설치되었는지 확인할 수 있습니다.

```
django-admin --version
```

콘솔에 인쇄된 Django 버전 번호가 표시되어야 합니다.

이제 Django가 설치되었으므로 첫 번째 Django 프로젝트를 만들 준비가 되었습니다.

## 새 Django 프로젝트 생성

Django는 프로젝트 구조를 사용하여 웹 애플리케이션의 모든 파일과 코드를 구성합니다. 프로젝트는 여러 앱을 포함할 수 있으며 각 앱은 특정 용도를 가질 수 있습니다. 예를 들어 블로그 게시물 관리용 앱, 사용자 계정 관리용 앱, 댓글 관리용 앱이 있을 수 있습니다.

새 Django 프로젝트를 만들려면 터미널 창을 열고 프로젝트를 저장할 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
django-admin startproject mysite
```

"mysite"를 프로젝트 이름으로 바꿉니다. 이 명령은 다음 구조로 "mysite"라는 새 디렉토리를 생성합니다.

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

"manage.py" 파일은 Django 프로젝트를 관리하는 데 도움이 되는 스크립트입니다. "mysite" 디렉토리에는 프로젝트의 파일과 코드가 포함되어 있습니다. "settings.py" 파일에는 Django 프로젝트의 구성이 포함되어 있습니다. "urls.py" 파일에는 프로젝트의 URL 패턴이 포함되어 있습니다. "wsgi.py" 파일은 Django 프로젝트를 웹 서버에 배포하는 데 사용됩니다.

[Django 문서](https://docs.djangoproject.com/en/3.0/intro/tutorial01/)에서 Django 프로젝트 구조에 대해 자세히 알아볼 수 있습니다.

## 프로젝트에 간단한 페이지 추가하기

이제 Django 프로젝트가 있으므로 프로젝트에 앱을 추가할 수 있습니다. 앱은 특정 목적을 위한 모든 파일과 코드를 포함하는 Python 패키지입니다.

앱을 만들려면 터미널 창을 열고 "mysite" 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
django-admin startapp myapp
```

"myapp"을 앱 이름으로 바꿉니다. 이 명령은 다음 구조로 "myapp"이라는 새 디렉토리를 생성합니다.

```
mysite/
    myapp/
        __init__.py
        admin.py
        apps.py
        models.py
        tests.py
        views.py
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

"admin.py" 파일은 Django의 관리 사이트에 사용됩니다. "apps.py" 파일은 앱을 구성하는 데 사용됩니다. "models.py" 파일은 앱의 모델을 정의하는 데 사용됩니다. "tests.py" 파일은 단위 테스트에 사용됩니다. "views.py" 파일에는 앱에 대한 보기가 포함되어 있습니다.

[Django 설명서](https://docs.djangoproject.com/en/3.0/intro/tutorial02/)에서 Django 앱의 파일에 대해 자세히 알아볼 수 있습니다.

이제 앱이 있으므로 앱에 보기를 추가할 수 있습니다. 뷰는 HTTP 요청을 받아 HTTP 응답을 반환하는 Python 함수입니다.

텍스트 편집기에서 "views.py" 파일을 열고 다음 코드를 추가합니다.

```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

이 코드는 "index.html" 템플릿을 렌더링하는 "index"라는 뷰를 정의합니다.

다음으로 "index.html" 템플릿을 만들어야 합니다. Django는 [Jinja](https://jinja.palletsprojects.com/) 템플릿 언어를 사용하여 HTML 템플릿을 렌더링합니다.

"mysite" 디렉토리에 "templates"라는 새 디렉토리를 만듭니다. 그런 다음 다음 코드를 사용하여 "templates" 디렉토리에 "index.html"이라는 새 파일을 만듭니다.

```html
<!DOCTYPE html>
<html>
<head>
    <title>My Site</title>
</head>
<body>
    <h1>Hello, world!</h1>
</body>
</html>
```

이 코드는 "Hello, world!"라는 텍스트를 표시하는 간단한 HTML 페이지를 정의합니다.

다음으로 URL "/"를 "인덱스" 보기에 매핑하도록 "mysite/urls.py" 파일을 구성해야 합니다. 텍스트 편집기에서 "mysite/urls.py" 파일을 열고 다음 코드를 추가합니다.

```python
from django.contrib import admin
from django.urls import path

from myapp.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index),
]
```

이 코드는 "myapp" 앱에서 "index" 보기를 가져오고 URL "/"을 "index" 보기에 매핑합니다.

이제 보기와 URL 패턴이 있으므로 Django 개발 서버를 실행하고 웹 브라우저에서 페이지를 볼 수 있습니다.

Django 개발 서버를 실행하려면 터미널 창을 열고 "mysite" 디렉토리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
python manage.py runserver
```

다음 출력이 표시되어야 합니다.

```
Performing system checks...

System check identified no issues (0 silenced).

You have 17 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

January 01, 2020 - 00:00:00
Django version 3.0, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

Django 개발 서버는 현재 http://127.0.0.1:8000/에서 실행 중입니다. http://127.0.0.1:8000/을 방문하면 웹 브라우저에서 페이지를 볼 수 있습니다.

다음 페이지가 표시됩니다.

![장고 페이지](https://www.tutorialspoint.com/django/images/django_page.jpg)

## 축하해요!

Django 웹 프레임워크와 Kotlin 프로그래밍 언어를 사용하여 웹 애플리케이션을 성공적으로 구축했습니다. 이 기사에서는 개발 환경을 설정하고 새 Django 프로젝트를 만들고 프로젝트에 간단한 페이지를 추가하는 방법을 배웠습니다.

이 문서의 소스 코드는 [GitHub](https://github.com/tutorialspoint/kotlin-django-example)에서 찾을 수 있습니다.

## 참조

- [장고 문서](https://docs.djangoproject.com/en/3.0/)
- [코틀린 문서](https://kotlinlang.org/docs/reference/)
- [장고 튜토리얼](https://www.tutorialspoint.com/django/index.htm)
- [Kotlin 튜토리얼](https://www.tutorialspoint.com/kotlin/index.htm)