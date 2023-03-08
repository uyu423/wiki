---
title: 如何使用 Django 创建网站
description: 
published: true
date: 2023-02-02T22:58:21.277Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:58:16.457Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Create a Website with Django***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-website-with-django)
{.links-list}


# 如何使用 Django 创建网站

Django 是一个用 Python 编写的高级 Web 框架，它鼓励快速开发和干净、实用的设计。由经验丰富的开发人员构建，它解决了 Web 开发的大部分麻烦，因此您可以专注于编写您的应用程序，而无需重新发明轮子。它是免费和开源的。

Django 是开发现代 Web 应用程序的绝佳选择。它是一个自带电池的框架，可以使许多常见的 Web 开发任务变得更加容易。

## 什么是 Django？

Django 是一个基于 Python 的 Web 框架，它允许您快速创建 Web 应用程序，而无需设置开发环境、管理依赖项等所有麻烦。

Django 包含许多内置功能，例如：

- 用于与数据库交互的 ORM
- 用于创建 HTML 页面的模板系统
- 基于 Python 的 Web 服务器
- 表格系统
- 认证系统

Django 的可扩展性也很强。有许多第三方包可用于向 Django Web 应用程序添加附加功能。

## 为什么要使用 Django？

出于多种原因，Django 是一个不错的选择。它是一个自带电池的框架，可以使许多常见的 Web 开发任务变得更加容易。

使用 Django 的一些好处是：

- Django 解决了很多 web 开发的麻烦，所以你可以专注于编写你的应用程序。
- Django 有很多内置功能，例如 ORM、模板系统和基于 Python 的 Web 服务器。
- Django 是非常可扩展的。有许多第三方包可用于向 Django Web 应用程序添加附加功能。
- Django 是开源且免费的。

## Django 与其他框架

Python 有许多不同的 Web 框架。那么，为什么要使用 Django？

以下是 Django 可能是您不错选择的一些原因：

- 如果你想要一个内置电池的框架：Django 包含许多内置功能，例如 ORM、模板系统和基于 Python 的 Web 服务器。
- 如果你想要一个可扩展的框架：Django 是非常可扩展的。有许多第三方包可用于向 Django Web 应用程序添加附加功能。
- 如果你想要一个开源且免费的框架：Django 是开源且免费的。

## 开始使用 Django

现在您知道 Django 是什么以及为什么要使用它，让我们来看看设置 Django Web 应用程序的过程。

### 设置开发环境

您需要做的第一件事是设置开发环境。我推荐使用 virtualenv 来创建一个独立的开发环境。

要安装 virtualenv，请运行以下命令：

```
pip install virtualenv
```

安装 virtualenv 后，您可以通过运行以下命令创建新的虚拟环境：

```
virtualenv myproject
```

这将创建一个名为 myproject 的新目录，其中包含一个独立的 Python 开发环境。

要激活虚拟环境，请运行以下命令：

```
source myproject/bin/activate
```

您现在可以将包安装到虚拟环境中，而不会影响系统上全局安装的包。

### 安装 Django

设置好开发环境后，就可以安装 Django 了。要安装 Django，请运行以下命令：

```
pip install django
```

这将安装 Django 和所有必需的依赖项。

### 创建 Django 项目

现在已经安装了 Django，您可以创建一个新的 Django 项目。为此，请运行以下命令：

```
django-admin startproject myproject
```

这将创建一个名为 myproject 的新目录，其中包含 Django 项目的文件。

### 运行 Django 开发服务器

现在您已经有了一个 Django 项目，您可以启动 Django 开发服务器。为此，请运行以下命令：

```
python manage.py runserver
```

这将启动 Django 开发服务器并使您的 Django 项目在 http://127.0.0.1:8000/ 可用。

## Django 网址

Django Web 应用程序最重要的部分之一是 URL 配置。 URL 配置是 Django 用来匹配传入 URL 的一组模式。

URL 配置中的每个模式都映射到一个视图函数。当用户请求匹配模式的 URL 时，Django 将调用相应的视图函数并返回结果。

例如，考虑以下 URL 配置：

```
urlpatterns = [
    url(r'^

此 URL 配置有两种模式。第一个模式匹配空字符串并将其映射到视图函数 myapp.views.home。第二个模式匹配字符串 'about/' 并将其映射到视图函数 myapp.views.about。

视图函数是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

## Django 视图

视图是 Django 网络应用程序的核心。视图是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

视图函数可以做您在 Python 函数中可以做的任何事情。这意味着他们可以访问数据库中的数据、执行计算等。

唯一的规则是它们必须返回一个 HttpResponse 对象。

## Django 模板

Django Web 应用程序最重要的部分之一是模板系统。模板系统用于呈现 HTML 页面。

Django 带有一个内置的模板系统，类似于 Jinja2 模板引擎中使用的系统。

要使用 Django 模板系统，首先需要创建一个模板。模板是包含 Django 网页 HTML 的文件。

这是一个简单的模板，只包含字符串“Hello, world!”：

```
{% extends 'base.html' %}

{% block content %}
Hello, world!
{% endblock %}
```

创建模板后，您可以使用 render() 函数渲染它。 render() 函数采用模板名称和上下文数据字典。

下面是如何呈现我们刚刚创建的模板的示例：

```
from django.shortcuts import render

def home(request):
    return render(request, 'home.html', {})
```

## Django 表单

Django 带有一个内置的表单系统，可以很容易地创建 HTML 表单。

要使用 Django 表单系统，首先需要创建一个表单。表单是一个 Python 类，它定义了将呈现为 HTML 表单元素的字段。

这是一个只有一个文本字段的简单表单：

```
from django import forms

class MyForm(forms.Form):
    myfield = forms.CharField(max_length=100)
```

创建表单后，您可以使用 {% form %} 标记在模板中呈现它。

{% form %} 标签将表单对象作为第一个参数，将上下文数据字典作为第二个参数。

下面是如何呈现我们刚刚创建的表单的示例：

```
{% form form %}
    {{ form.myfield }}
{% endform %}
```

## Django 模型

Django 带有一个内置的模型系统，可以很容易地处理数据库中的数据。

要使用 Django 模型系统，首先需要创建一个模型。模型是一个 Python 类，它定义了数据对象的字段和行为。

这是一个只有一个字段的简单模型：

```
from django.db import models

class MyModel(models.Model):
    myfield = models.CharField(max_length=100)
```

创建模型后，您可以使用 Django 管理器添加、编辑和删除对象。

您还可以使用 Django 模型 API 查询数据库以及创建、更新和删除对象。

## Django 管理员

Django 带有内置管理系统，可以轻松管理数据库中的数据。

要使用 Django 管理员，您首先需要创建一个管理员用户。管理员用户是已被授予访问 Django 管理员权限的用户。

要创建管理员用户，请运行以下命令：

```
python manage.py createsuperuser
```

创建管理员用户后，您可以通过访问 http://127.0.0.1:8000/admin/ 登录到 Django 管理员。

登录后，您将看到 Django 管理界面。从这里，您可以添加、编辑和删除对象。

## 结论

Django 是开发现代 Web 应用程序的绝佳选择。它是一个自带电池的框架，可以使许多常见的 Web 开发任务变得更加容易。

如果您是 Django 的新手，我建议您查看 Django 文档。它是了解 Django 框架所有功能的绝佳资源。, 'myapp.views.home'),
    url(r'^about/

此 URL 配置有两种模式。第一个模式匹配空字符串并将其映射到视图函数 myapp.views.home。第二个模式匹配字符串 'about/' 并将其映射到视图函数 myapp.views.about。

视图函数是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
从 django.http 导入 HttpResponse

定义主页（请求）：
    返回 HttpResponse('你好，世界！')
```

## Django 视图

视图是 Django 网络应用程序的核心。视图是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
从 django.http 导入 HttpResponse

定义主页（请求）：
    返回 HttpResponse('你好，世界！')
```

视图函数可以做您在 Python 函数中可以做的任何事情。这意味着他们可以访问数据库中的数据、执行计算等。

唯一的规则是它们必须返回一个 HttpResponse 对象。

## Django 模板

Django Web 应用程序最重要的部分之一是模板系统。模板系统用于呈现 HTML 页面。

Django 带有一个内置的模板系统，类似于 Jinja2 模板引擎中使用的系统。

要使用 Django 模板系统，首先需要创建一个模板。模板是包含 Django 网页 HTML 的文件。

这是一个简单的模板，只包含字符串“Hello, world!”：

```
{% 扩展 'base.html' %}

{% 块内容 %}
你好世界！
{% 端块 %}
```

创建模板后，您可以使用 render() 函数渲染它。 render() 函数采用模板名称和上下文数据字典。

下面是如何呈现我们刚刚创建的模板的示例：

```
从 django.shortcuts 导入渲染

定义主页（请求）：
    返回渲染（请求，'home.html'，{}）
```

## Django 表单

Django 带有一个内置的表单系统，可以很容易地创建 HTML 表单。

要使用 Django 表单系统，首先需要创建一个表单。表单是一个 Python 类，它定义了将呈现为 HTML 表单元素的字段。

这是一个只有一个文本字段的简单表单：

```
从 django 导入表单

MyForm 类（表单.Form）：
    myfield = forms.CharField(max_length=100)
```

创建表单后，您可以使用 {% form %} 标记在模板中呈现它。

{% form %} 标签将表单对象作为第一个参数，将上下文数据字典作为第二个参数。

下面是如何呈现我们刚刚创建的表单的示例：

```
{% 表格表格 %}
    {{ 表单.myfield }}
{% 最终形式 %}
```

## Django 模型

Django 带有一个内置的模型系统，可以很容易地处理数据库中的数据。

要使用 Django 模型系统，首先需要创建一个模型。模型是一个 Python 类，它定义了数据对象的字段和行为。

这是一个只有一个字段的简单模型：

```
从 django.db 导入模型

类 MyModel（模型。模型）：
    myfield = models.CharField(max_length=100)
```

创建模型后，您可以使用 Django 管理器添加、编辑和删除对象。

您还可以使用 Django 模型 API 查询数据库以及创建、更新和删除对象。

## Django 管理员

Django 带有内置管理系统，可以轻松管理数据库中的数据。

要使用 Django 管理员，您首先需要创建一个管理员用户。管理员用户是已被授予访问 Django 管理员权限的用户。

要创建管理员用户，请运行以下命令：

```
python manage.py 创建超级用户
```

创建管理员用户后，您可以通过访问 http://127.0.0.1:8000/admin/ 登录到 Django 管理员。

登录后，您将看到 Django 管理界面。从这里，您可以添加、编辑和删除对象。

## 结论

Django 是开发现代 Web 应用程序的绝佳选择。它是一个自带电池的框架，可以使许多常见的 Web 开发任务变得更加容易。

如果您是 Django 的新手，我建议您查看 Django 文档。它是了解 Django 框架所有功能的绝佳资源。, 'myapp.views.about'),
]
```

此 URL 配置有两种模式。第一个模式匹配空字符串并将其映射到视图函数 myapp.views.home。第二个模式匹配字符串 'about/' 并将其映射到视图函数 myapp.views.about。

视图函数是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
从 django.http 导入 HttpResponse

定义主页（请求）：
    返回 HttpResponse('你好，世界！')
```

## Django 视图

视图是 Django 网络应用程序的核心。视图是将 HttpRequest 对象作为第一个参数并返回 HttpResponse 对象的 Python 函数。

这是一个简单的视图函数，它返回一个带有字符串“Hello, world!”的 HttpResponse 对象：

```
从 django.http 导入 HttpResponse

定义主页（请求）：
    返回 HttpResponse('你好，世界！')
```

视图函数可以做您在 Python 函数中可以做的任何事情。这意味着他们可以访问数据库中的数据、执行计算等。

唯一的规则是它们必须返回一个 HttpResponse 对象。

## Django 模板

Django Web 应用程序最重要的部分之一是模板系统。模板系统用于呈现 HTML 页面。

Django 带有一个内置的模板系统，类似于 Jinja2 模板引擎中使用的系统。

要使用 Django 模板系统，首先需要创建一个模板。模板是包含 Django 网页 HTML 的文件。

这是一个简单的模板，只包含字符串“Hello, world!”：

```
{% 扩展 'base.html' %}

{% 块内容 %}
你好世界！
{% 端块 %}
```

创建模板后，您可以使用 render() 函数渲染它。 render() 函数采用模板名称和上下文数据字典。

下面是如何呈现我们刚刚创建的模板的示例：

```
从 django.shortcuts 导入渲染

定义主页（请求）：
    返回渲染（请求，'home.html'，{}）
```

## Django 表单

Django 带有一个内置的表单系统，可以很容易地创建 HTML 表单。

要使用 Django 表单系统，首先需要创建一个表单。表单是一个 Python 类，它定义了将呈现为 HTML 表单元素的字段。

这是一个只有一个文本字段的简单表单：

```
从 django 导入表单

MyForm 类（表单.Form）：
    myfield = forms.CharField(max_length=100)
```

创建表单后，您可以使用 {% form %} 标记在模板中呈现它。

{% form %} 标签将表单对象作为第一个参数，将上下文数据字典作为第二个参数。

下面是如何呈现我们刚刚创建的表单的示例：

```
{% 表格表格 %}
    {{ 表单.myfield }}
{% 最终形式 %}
```

## Django 模型

Django 带有一个内置的模型系统，可以很容易地处理数据库中的数据。

要使用 Django 模型系统，首先需要创建一个模型。模型是一个 Python 类，它定义了数据对象的字段和行为。

这是一个只有一个字段的简单模型：

```
从 django.db 导入模型

类 MyModel（模型。模型）：
    myfield = models.CharField(max_length=100)
```

创建模型后，您可以使用 Django 管理器添加、编辑和删除对象。

您还可以使用 Django 模型 API 查询数据库以及创建、更新和删除对象。

## Django 管理员

Django 带有内置管理系统，可以轻松管理数据库中的数据。

要使用 Django 管理员，您首先需要创建一个管理员用户。管理员用户是已被授予访问 Django 管理员权限的用户。

要创建管理员用户，请运行以下命令：

```
python manage.py 创建超级用户
```

创建管理员用户后，您可以通过访问 http://127.0.0.1:8000/admin/ 登录到 Django 管理员。

登录后，您将看到 Django 管理界面。从这里，您可以添加、编辑和删除对象。

## 结论

Django 是开发现代 Web 应用程序的绝佳选择。它是一个自带电池的框架，可以使许多常见的 Web 开发任务变得更加容易。

如果您是 Django 的新手，我建议您查看 Django 文档。它是了解 Django 框架所有功能的绝佳资源。