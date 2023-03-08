---
title: Kotlin 和 Django：使用 Python 框架构建 Web 应用程序
description: 
published: true
date: 2023-02-03T13:56:31.878Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:56:30.200Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Kotlin and Django: Building a Web Application with a Python Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-django-building-a-web-application-with-a-python-framework)
{.links-list}


# Kotlin 和 Django：使用 Python 框架构建 Web 应用程序

Django 是一个 Python Web 框架，它鼓励快速开发和干净、实用的设计。 Django 是免费和开源的，解决了 Web 开发的大部分麻烦，因此您可以专注于编写您的应用程序，而无需重新发明轮子。它也很容易学习，不需要很长时间即可启动和运行。

Kotlin 是一种用于现代多平台应用程序的静态类型编程语言。 Kotlin 与 Java 是 100% 互操作的，因此如果您已经熟悉 Java，则很容易开始使用 Kotlin。 Kotlin 也比 Java 更简洁，因此您可以编写更少的代码并完成更多的工作。

在本文中，我们将向您展示如何使用 Django Web 框架和 Kotlin 编程语言构建 Web 应用程序。我们将引导您完成设置开发环境、创建新的 Django 项目以及向项目添加简单页面的步骤。到本文结束时，您将基本了解如何使用 Django 和 Kotlin 构建 Web 应用程序。

## 设置你的开发环境

在开始构建 Web 应用程序之前，您需要设置一个开发环境。如果您是 Python 的新手，我们建议您使用 Anaconda，它是 Python 的一个发行版，其中包含最流行的数据科学 Python 包。

如果您使用的是 Anaconda，则可以使用以下命令安装 Django：

```
conda install -c anaconda django
```

如果你不使用 Anaconda，你可以使用 pip 包管理器安装 Django：

```
pip install django
```

您可以通过运行以下命令来验证 Django 是否已安装：

```
django-admin --version
```

您应该看到 Django 版本号打印到控制台。

现在你已经安装了 Django，你已经准备好创建你的第一个 Django 项目了。

## 创建一个新的 Django 项目

Django 使用项目结构来组织 Web 应用程序的所有文件和代码。一个项目可以包含多个应用程序，每个应用程序都可以有特定的用途。例如，您可能有一个用于管理博客文章的应用程序、另一个用于管理用户帐户的应用程序以及另一个用于管理评论的应用程序。

要创建一个新的 Django 项目，请打开一个终端窗口并导航到您要存储项目的目录。然后，运行以下命令：

```
django-admin startproject mysite
```

将“mysite”替换为您的项目名称。此命令将创建一个名为“mysite”的新目录，其结构如下：

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

“manage.py”文件是帮助您管理 Django 项目的脚本。 “mysite”目录包含项目的文件和代码。 “settings.py”文件包含 Django 项目的配置。 “urls.py”文件包含项目的 URL 模式。 “wsgi.py”文件用于将 Django 项目部署到 Web 服务器。

您可以在 [Django 文档](https://docs.djangoproject.com/en/3.0/intro/tutorial01/) 中了解有关 Django 项目结构的更多信息。

## 添加一个简单的页面到项目中

现在您有了一个 Django 项目，您可以向该项目添加一个应用程序。应用程序是一个 Python 包，其中包含用于特定目的的所有文件和代码。

要创建应用程序，请打开终端窗口并导航到“mysite”目录。然后，运行以下命令：

```
django-admin startapp myapp
```

将“myapp”替换为您的应用名称。此命令将创建一个名为“myapp”的新目录，其结构如下：

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

“admin.py”文件用于 Django 的管理站点。 “apps.py”文件用于配置您的应用程序。 “models.py”文件用于为您的应用程序定义模型。 “tests.py”文件用于单元测试。 “views.py”文件包含您的应用程序的视图。

您可以在 [Django 文档](https://docs.djangoproject.com/en/3.0/intro/tutorial02/) 中了解有关 Django 应用程序中文件的更多信息。

现在您有了一个应用程序，您可以向该应用程序添加一个视图。视图是一个 Python 函数，它接受 HTTP 请求并返回 HTTP 响应。

在文本编辑器中打开“views.py”文件并添加以下代码：

```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

此代码定义了一个名为“index”的视图，它呈现“index.html”模板。

接下来，您需要创建“index.html”模板。 Django 使用 [Jinja](https://jinja.palletsprojects.com/) 模板语言呈现 HTML 模板。

在“mysite”目录中创建一个名为“templates”的新目录。然后，使用以下代码在“templates”目录中创建一个名为“index.html”的新文件：

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

此代码定义了一个简单的 HTML 页面，该页面显示文本“Hello, world!”

接下来，您需要配置“mysite/urls.py”文件以将 URL“/”映射到“index”视图。在文本编辑器中打开“mysite/urls.py”文件并添加以下代码：

```python
from django.contrib import admin
from django.urls import path

from myapp.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index),
]
```

此代码从“myapp”应用导入“index”视图，并将 URL“/”映射到“index”视图。

现在您有了一个视图和一个 URL 模式，您可以运行 Django 开发服务器并在 Web 浏览器中查看您的页面。

要运行 Django 开发服务器，请打开一个终端窗口并导航到“mysite”目录。然后，运行以下命令：

```
python manage.py runserver
```

您应该看到以下输出：

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

Django 开发服务器现在运行在 http://127.0.0.1:8000/ 上。您可以通过访问 http://127.0.0.1:8000/ 在 Web 浏览器中查看您的页面。

您应该会看到以下页面：

![Django 页面](https://www.tutorialspoint.com/django/images/django_page.jpg)

## 恭喜！

您已经使用 Django Web 框架和 Kotlin 编程语言成功构建了一个 Web 应用程序。在本文中，您学习了如何设置开发环境、创建新的 Django 项目以及向项目添加简单页面。

您可以在 [GitHub](https://github.com/tutorialspoint/kotlin-django-example) 上找到本文的源代码。

## 参考

- [Django 文档](https://docs.djangoproject.com/en/3.0/)
- [Kotlin 文档](https://kotlinlang.org/docs/reference/)
- [Django 教程](https://www.tutorialspoint.com/django/index.htm)
- [Kotlin 教程](https://www.tutorialspoint.com/kotlin/index.htm)