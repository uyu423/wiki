---
title: 백엔드 개발을 위한 Python: Django 및 Flask
description: 
published: true
date: 2023-02-18T15:07:34.973Z
tags: 
editor: markdown
dateCreated: 2023-02-18T15:07:27.885Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Python for Backend Development: Django and Flask***English** document is available*](/en/Knowledge-base/Backend/python-for-backend-development-django-and-flask)
{.links-list}


# 백엔드 개발을 위한 Python: Django 및 Flask

Python은 Django 및 Flask와 같은 프레임워크를 사용하여 백엔드 개발에 사용할 수 있는 다재다능한 언어입니다. 이 기사에서는 이 두 가지 프레임워크를 살펴보고 Python 애플리케이션을 개발하는 데 어떻게 사용할 수 있는지 알아봅니다.

## 장고

Django는 Python으로 작성된 고급 웹 프레임워크입니다. 웹 애플리케이션의 개발 프로세스를 보다 쉽고 빠르게 할 수 있도록 설계되었습니다. Django에는 사용자 인증 시스템, ORM(개체 관계형 매퍼) 및 템플릿 엔진과 같은 기본 제공 기능이 많이 있습니다.

Django는 크고 복잡한 애플리케이션에 적합한 선택입니다. 또한 높은 수준의 보안이 필요한 프로젝트에도 적합합니다.

### 시작하기

Django를 사용하려면 먼저 Django를 설치해야 합니다. `pip` 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```bash
pip install django
```

Django가 설치되면 `django-admin` 명령을 사용하여 새 프로젝트를 만들 수 있습니다.

```bash
django-admin startproject myproject
```

그러면 다음 파일 구조로 `myproject`라는 새 디렉토리가 생성됩니다.

```
myproject/
├── manage.py
└── myproject
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

`manage.py` 파일은 Django 프로젝트를 관리하는 데 사용됩니다. `myproject` 디렉토리의 다른 파일은 설정 파일입니다.

### 애플리케이션 만들기

애플리케이션은 Django 프로젝트의 빌딩 블록입니다. 프로젝트는 여러 응용 프로그램을 가질 수 있으며 각 응용 프로그램은 다른 기능을 가질 수 있습니다.

새 애플리케이션을 만들려면 `django-admin` 명령을 사용합니다.

```bash
django-admin startapp myapp
```

그러면 다음 파일 구조로 `myapp`이라는 새 디렉토리가 생성됩니다.

```
myapp/
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
└── views.py
```

`myapp` 디렉토리에는 애플리케이션의 모든 파일이 들어 있습니다. `models.py` 파일은 애플리케이션의 데이터 모델을 정의하는 데 사용됩니다. `views.py` 파일은 애플리케이션의 보기(즉, 논리)를 정의하는 데 사용됩니다. `urls.py` 파일은 애플리케이션의 URL을 정의하는 데 사용됩니다.

### 모델 정의

모델은 Django 애플리케이션의 핵심입니다. 모델은 애플리케이션의 데이터를 나타내는 데 사용됩니다.

모델은 `django.db.models.Model` 클래스에서 상속되는 Python 클래스입니다. 각 모델에는 애플리케이션의 데이터를 나타내는 데 사용되는 여러 필드가 있습니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 다음 필드가 있는 `Post` 모델이 있을 수 있습니다.

```python
class Post(models.Model):
    title = models.CharField(max_length=255)
    body = models.TextField()
    published_at = models.DateTimeField(auto_now_add=True)
```

`Post` 모델에는 `title`, `body` 및 `published_at`의 세 가지 필드가 있습니다. `제목` 및 `본문` 필드는 각각 블로그 게시물의 제목과 본문을 저장하는 데 사용됩니다. `published_at` 필드는 블로그 게시물이 게시된 날짜와 시간을 저장하는 데 사용됩니다.

### 모델 등록

모델을 정의한 후 Django에 모델을 등록해야 합니다. `admin.py` 파일에 다음 행을 추가하여 이를 수행할 수 있습니다.

```python
admin.site.register(Post)
```

이렇게 하면 Django 관리 사이트에 `Post` 모델이 등록됩니다.

### 보기 정의

뷰는 Django 애플리케이션의 논리입니다. 들어오는 HTTP 요청을 처리하고 HTTP 응답을 반환하는 데 사용됩니다.

보기는 `HttpRequest` 개체를 인수로 사용하고 `HttpResponse` 개체를 반환하는 Python 함수입니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 모든 블로그 게시물 목록을 표시하는 보기가 있을 수 있습니다.

```python
def post_list(request):
    posts = Post.objects.all()
    return render(request, 'post_list.html', {'posts': posts})
```

`post_list` 보기는 `HttpRequest` 개체를 사용하고 `HttpResponse` 개체를 반환합니다. `HttpResponse` 개체에는 표시될 페이지의 HTML이 포함되어 있습니다.

`post_list` 보기는 데이터베이스에서 모든 `Post` 개체를 가져와서 `post_list.html` 템플릿에 전달합니다. `post_list.html` 템플릿은 페이지의 HTML을 렌더링합니다.

### URL 정의

URL은 보기를 특정 URL에 매핑하는 데 사용됩니다. 그것들은 `urls.py` 파일에 정의되어 있습니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 다음과 같은 `urls.py` 파일이 있을 수 있습니다.

```python
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^

`urlpatterns` 변수는 URL 패턴 목록입니다. 각 URL 패턴은 다음의 튜플입니다.

- URL 일치에 사용되는 정규식
- 호출되는 보기 기능
- URL의 이름

`^$` 정규식은 빈 문자열과 일치합니다. 이 URL 패턴은 `/` URL과 일치합니다.

`/` URL이 요청되면 `post_list` 보기 기능이 호출됩니다. `post_list` 보기 기능은 페이지의 HTML을 반환합니다.

URL의 이름은 URL을 식별하는 데 사용됩니다. 이는 URL을 반전(예: 보기 기능에서 URL 생성)하는 데 유용합니다.

### 렌더링 템플릿

템플릿은 Django 보기용 HTML을 렌더링하는 데 사용됩니다. Django는 Django 템플릿 엔진이라고 하는 내장 템플릿 엔진과 함께 제공됩니다.

Django 템플릿 엔진은 템플릿과 컨텍스트(Python 사전)를 가져와 컨텍스트 데이터로 템플릿을 렌더링합니다.

템플릿은 `render` 함수로 렌더링됩니다.

```python
def post_list(request):
    posts = Post.objects.all()
    return render(request, 'post_list.html', {'posts': posts})
```

`render` 함수는 `request` 개체, 템플릿 이름 및 컨텍스트 데이터를 사용합니다. `render` 함수는 페이지의 HTML을 반환합니다.

`post_list.html` 템플릿은 다음과 같습니다.

```html
<html>
<head>
    <title>My Blog</title>
</head>
<body>
    {% for post in posts %}
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    {% endfor %}
</body>
</html>
```

`post_list.html` 템플릿은 `posts` 변수를 반복하고 각 `Post`의 `title`과 `body`를 표시합니다.

## 플라스크

Flask는 Python용 마이크로프레임워크입니다. 웹 애플리케이션의 개발 프로세스를 보다 쉽고 빠르게 할 수 있도록 설계되었습니다. Flask는 개발 서버 및 기본 템플릿 엔진과 같은 몇 가지 기본 기능을 제공합니다.

Flask는 작고 간단한 응용 프로그램에 적합한 선택입니다. 또한 높은 수준의 유연성이 필요한 프로젝트에도 적합합니다.

### 시작하기

Flask를 사용하려면 먼저 Flask를 설치해야 합니다. `pip` 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```bash
pip install flask
```

Flask가 설치되면 다음 코드를 사용하여 `app.py`라는 새 파일을 만들 수 있습니다.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

이 코드는 새로운 Flask 애플리케이션을 생성합니다. `@app.route` 데코레이터는 URL을 뷰 함수에 매핑하는 데 사용됩니다. `인덱스` 뷰 함수는 문자열 `Hello, World!`를 반환합니다.

`if __name__ == '__main__':` 블록은 애플리케이션을 실행하는 데 사용됩니다. `app.run` 함수는 개발 서버를 시작합니다.

`python` 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```bash
python app.py
```

http://localhost:5000/에서 애플리케이션에 액세스할 수 있습니다.

### 애플리케이션 만들기

애플리케이션은 Flask 프로젝트의 빌딩 블록입니다. 프로젝트는 여러 응용 프로그램을 가질 수 있으며 각 응용 프로그램은 다른 기능을 가질 수 있습니다.

새 애플리케이션을 만들려면 다음 코드를 사용하여 `app.py`라는 새 파일을 만듭니다.

```python
from flask import Flask

app = Flask(__name__)
```

이 코드는 새로운 Flask 애플리케이션을 생성합니다.

### 보기 정의

뷰는 Flask 애플리케이션의 논리입니다. 들어오는 HTTP 요청을 처리하고 HTTP 응답을 반환하는 데 사용됩니다.

보기는 `HttpRequest` 개체를 인수로 사용하고 `HttpResponse` 개체를 반환하는 Python 함수입니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 모든 블로그 게시물 목록을 표시하는 보기가 있을 수 있습니다.

```python
@app.route('/')
def post_list():
    posts = Post.objects.all()
    return render_template('post_list.html', {'posts': posts})
```

`post_list` 보기는 `HttpRequest` 개체를 사용하고 `HttpResponse` 개체를 반환합니다. `HttpResponse` 개체에는 표시될 페이지의 HTML이 포함되어 있습니다.

`post_list` 보기는 데이터베이스에서 모든 `Post` 개체를 가져와서 `post_list.html` 템플릿에 전달합니다. `post_list.html` 템플릿은 페이지의 HTML을 렌더링합니다.

### URL 정의

URL은 보기를 특정 URL에 매핑하는 데 사용됩니다. 그것들은 `app.py` 파일에 정의되어 있습니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 다음과 같은 `app.py` 파일이 있을 수 있습니다.

```python
@app.route('/')
def post_list():
    ...

@app.route('/posts/<int:post_id>')
def post_detail(post_id):
    ...
```

`@app.route` 데코레이터는 URL을 뷰 함수에 매핑하는 데 사용됩니다. `/` URL이 요청되면 `post_list` 보기 기능이 호출됩니다. `/posts/<int:post_id>` URL이 요청되면 `post_detail` 보기 기능이 호출됩니다.

### 렌더링 템플릿

템플릿은 Flask 보기용 HTML을 렌더링하는 데 사용됩니다. Flask는 Jinja2 템플릿 엔진이라는 내장 템플릿 엔진과 함께 제공됩니다.

Jinja2 템플릿 엔진은 템플릿과 컨텍스트(Python 사전)를 가져와 컨텍스트 데이터로 템플릿을 렌더링합니다.

템플릿은 `render_template` 함수로 렌더링됩니다.

```python
@app.route('/')
def post_list():
    posts = Post.objects.all()
    return render_template('post_list.html', {'posts': posts})
```

`render_template` 함수는 템플릿의 이름과 컨텍스트 데이터를 사용합니다. `render_template` 함수는 페이지의 HTML을 반환합니다.

`post_list.html` 템플릿은 다음과 같습니다.

```html
<html>
<head>
    <title>My Blog</title>
</head>
<body>
    {% for post in posts %}
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    {% endfor %}
</body>
</html>
```

`post_list.html` 템플릿은 `posts` 변수를 반복하고 각 `Post`의 `title`과 `body`를 표시합니다.

## 결론

이 기사에서는 백엔드 개발을 위한 두 가지 Python 프레임워크인 Django와 Flask를 살펴보았습니다. 각 프레임워크를 시작하는 방법과 기본 애플리케이션을 만드는 방법을 살펴보았습니다., views.post_list, name='post_list'),
]
```

`urlpatterns` 변수는 URL 패턴 목록입니다. 각 URL 패턴은 다음의 튜플입니다.

- URL 일치에 사용되는 정규식
- 호출되는 보기 기능
- URL의 이름

`^$` 정규식은 빈 문자열과 일치합니다. 이 URL 패턴은 `/` URL과 일치합니다.

`/` URL이 요청되면 `post_list` 보기 기능이 호출됩니다. `post_list` 보기 기능은 페이지의 HTML을 반환합니다.

URL의 이름은 URL을 식별하는 데 사용됩니다. 이는 URL을 반전(예: 보기 기능에서 URL 생성)하는 데 유용합니다.

### 렌더링 템플릿

템플릿은 Django 보기용 HTML을 렌더링하는 데 사용됩니다. Django는 Django 템플릿 엔진이라고 하는 내장 템플릿 엔진과 함께 제공됩니다.

Django 템플릿 엔진은 템플릿과 컨텍스트(Python 사전)를 가져와 컨텍스트 데이터로 템플릿을 렌더링합니다.

템플릿은 `render` 함수로 렌더링됩니다.

```파이썬
def post_list(요청):
    게시물 = Post.objects.all()
    렌더링 반환(요청, 'post_list.html', {'posts': posts})
```

`render` 함수는 `request` 개체, 템플릿 이름 및 컨텍스트 데이터를 사용합니다. `render` 함수는 페이지의 HTML을 반환합니다.

`post_list.html` 템플릿은 다음과 같습니다.

```html
<html>
<헤드>
    <title>내 블로그</title>
</헤드>
<몸>
    {게시물의 게시물 %}
    <h1>{{ 포스트.제목 }}</h1>
    <p>{{ 포스트.본문 }}</p>
    {% endfor %}
</body>
</html>
```

`post_list.html` 템플릿은 `posts` 변수를 반복하고 각 `Post`의 `title`과 `body`를 표시합니다.

## 플라스크

Flask는 Python용 마이크로프레임워크입니다. 웹 애플리케이션의 개발 프로세스를 보다 쉽고 빠르게 할 수 있도록 설계되었습니다. Flask는 개발 서버 및 기본 템플릿 엔진과 같은 몇 가지 기본 기능을 제공합니다.

Flask는 작고 간단한 응용 프로그램에 적합한 선택입니다. 또한 높은 수준의 유연성이 필요한 프로젝트에도 적합합니다.

### 시작하기

Flask를 사용하려면 먼저 Flask를 설치해야 합니다. `pip` 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```강타
핍 설치 플라스크
```

Flask가 설치되면 다음 코드를 사용하여 `app.py`라는 새 파일을 만들 수 있습니다.

```파이썬
플라스크에서 플라스크 가져오기

앱 = 플라스크(__name__)

@app.route('/')
데프 인덱스():
    'Hello, World!'를 반환합니다.

__name__ == '__main__'인 경우:
    앱.런()
```

이 코드는 새로운 Flask 애플리케이션을 생성합니다. `@app.route` 데코레이터는 URL을 뷰 함수에 매핑하는 데 사용됩니다. `인덱스` 뷰 함수는 문자열 `Hello, World!`를 반환합니다.

`if __name__ == '__main__':` 블록은 애플리케이션을 실행하는 데 사용됩니다. `app.run` 함수는 개발 서버를 시작합니다.

`python` 명령을 사용하여 애플리케이션을 실행할 수 있습니다.

```강타
파이썬 앱.py
```

http://localhost:5000/에서 애플리케이션에 액세스할 수 있습니다.

### 애플리케이션 만들기

애플리케이션은 Flask 프로젝트의 빌딩 블록입니다. 프로젝트는 여러 응용 프로그램을 가질 수 있으며 각 응용 프로그램은 다른 기능을 가질 수 있습니다.

새 애플리케이션을 만들려면 다음 코드를 사용하여 `app.py`라는 새 파일을 만듭니다.

```파이썬
플라스크에서 플라스크 가져오기

앱 = 플라스크(__name__)
```

이 코드는 새로운 Flask 애플리케이션을 생성합니다.

### 보기 정의

뷰는 Flask 애플리케이션의 논리입니다. 들어오는 HTTP 요청을 처리하고 HTTP 응답을 반환하는 데 사용됩니다.

보기는 `HttpRequest` 개체를 인수로 사용하고 `HttpResponse` 개체를 반환하는 Python 함수입니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 모든 블로그 게시물 목록을 표시하는 보기가 있을 수 있습니다.

```파이썬
@app.route('/')
def post_list():
    게시물 = Post.objects.all()
    return render_template('post_list.html', {'posts': 게시물})
```

`post_list` 보기는 `HttpRequest` 개체를 사용하고 `HttpResponse` 개체를 반환합니다. `HttpResponse` 개체에는 표시될 페이지의 HTML이 포함되어 있습니다.

`post_list` 보기는 데이터베이스에서 모든 `Post` 개체를 가져와서 `post_list.html` 템플릿에 전달합니다. `post_list.html` 템플릿은 페이지의 HTML을 렌더링합니다.

### URL 정의

URL은 보기를 특정 URL에 매핑하는 데 사용됩니다. 그것들은 `app.py` 파일에 정의되어 있습니다.

예를 들어 블로그 애플리케이션을 빌드하는 경우 다음과 같은 `app.py` 파일이 있을 수 있습니다.

```파이썬
@app.route('/')
def post_list():
    ...

@app.route('/posts/<int:post_id>')
def post_detail(post_id):
    ...
```

`@app.route` 데코레이터는 URL을 뷰 함수에 매핑하는 데 사용됩니다. `/` URL이 요청되면 `post_list` 보기 기능이 호출됩니다. `/posts/<int:post_id>` URL이 요청되면 `post_detail` 보기 기능이 호출됩니다.

### 렌더링 템플릿

템플릿은 Flask 보기용 HTML을 렌더링하는 데 사용됩니다. Flask는 Jinja2 템플릿 엔진이라는 내장 템플릿 엔진과 함께 제공됩니다.

Jinja2 템플릿 엔진은 템플릿과 컨텍스트(Python 사전)를 가져와 컨텍스트 데이터로 템플릿을 렌더링합니다.

템플릿은 `render_template` 함수로 렌더링됩니다.

```파이썬
@app.route('/')
def post_list():
    게시물 = Post.objects.all()
    return render_template('post_list.html', {'posts': 게시물})
```

`render_template` 함수는 템플릿의 이름과 컨텍스트 데이터를 사용합니다. `render_template` 함수는 페이지의 HTML을 반환합니다.

`post_list.html` 템플릿은 다음과 같습니다.

```html
<html>
<헤드>
    <title>내 블로그</title>
</헤드>
<몸>
    {게시물의 게시물 %}
    <h1>{{ 포스트.제목 }}</h1>
    <p>{{ 포스트.본문 }}</p>
    {% endfor %}
</body>
</html>
```

`post_list.html` 템플릿은 `posts` 변수를 반복하고 각 `Post`의 `title`과 `body`를 표시합니다.

## 결론

이 기사에서는 백엔드 개발을 위한 두 가지 Python 프레임워크인 Django와 Flask를 살펴보았습니다. 각 프레임워크를 시작하는 방법과 기본 애플리케이션을 만드는 방법을 살펴보았습니다.