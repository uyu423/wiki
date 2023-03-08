---
title: Python for Backend Development: Django and Flask
description: 
published: true
date: 2023-02-18T15:07:29.395Z
tags: 
editor: markdown
dateCreated: 2023-02-18T15:07:27.887Z
---

- [백엔드 개발을 위한 Python: Django 및 Flask***Korean** document is available*](/ko/Knowledge-base/Backend/python-for-backend-development-django-and-flask)
{.links-list}


# Python for Backend Development: Django and Flask

Python is a versatile language that can be used for backend development with frameworks like Django and Flask. In this article, we will take a look at these two frameworks and see how they can be used to develop Python applications.

## Django

Django is a high-level web framework that is written in Python. It is designed to make the development process of web applications easier and faster. Django comes with a lot of features out-of-the-box, such as a user authentication system, an object-relational mapper (ORM), and a template engine.

Django is a good choice for large and complex applications. It is also suitable for projects that require a high level of security.

### Getting Started

To use Django, you need to install it first. You can do this using the `pip` package manager:

```bash
pip install django
```

Once Django is installed, you can create a new project using the `django-admin` command:

```bash
django-admin startproject myproject
```

This will create a new directory called `myproject` with the following file structure:

```
myproject/
├── manage.py
└── myproject
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

The `manage.py` file is used to manage your Django project. The other files in the `myproject` directory are settings files.

### Creating an Application

Applications are the building blocks of Django projects. A project can have multiple applications and each application can have different functionality.

To create a new application, use the `django-admin` command:

```bash
django-admin startapp myapp
```

This will create a new directory called `myapp` with the following file structure:

```
myapp/
├── __init__.py
├── admin.py
├── apps.py
├── models.py
├── tests.py
└── views.py
```

The `myapp` directory contains all the files for your application. The `models.py` file is used to define the data models for your application. The `views.py` file is used to define the views (i.e. the logic) for your application. The `urls.py` file is used to define the URLs for your application.

### Defining Models

Models are the core of Django applications. Models are used to represent the data in your application.

A model is a Python class that inherits from the `django.db.models.Model` class. Each model has a number of fields, which are used to represent the data in your application.

For example, if you were building a blog application, you might have a `Post` model with the following fields:

```python
class Post(models.Model):
    title = models.CharField(max_length=255)
    body = models.TextField()
    published_at = models.DateTimeField(auto_now_add=True)
```

The `Post` model has three fields: `title`, `body`, and `published_at`. The `title` and `body` fields are used to store the title and body of the blog post, respectively. The `published_at` field is used to store the date and time when the blog post was published.

### Registering Models

After you have defined your models, you need to register them with Django. You can do this by adding the following line to the `admin.py` file:

```python
admin.site.register(Post)
```

This will register the `Post` model with the Django admin site.

### Defining Views

Views are the logic of Django applications. They are used to handle the incoming HTTP requests and return the HTTP responses.

Views are Python functions that take an `HttpRequest` object as an argument and return an `HttpResponse` object.

For example, if you were building a blog application, you might have a view that displays a list of all the blog posts:

```python
def post_list(request):
    posts = Post.objects.all()
    return render(request, 'post_list.html', {'posts': posts})
```

The `post_list` view takes an `HttpRequest` object and returns an `HttpResponse` object. The `HttpResponse` object contains the HTML for the page that will be displayed.

The `post_list` view gets all the `Post` objects from the database and passes them to the `post_list.html` template. The `post_list.html` template renders the HTML for the page.

### Defining URLs

URLs are used to map views to specific URLs. They are defined in the `urls.py` file.

For example, if you were building a blog application, you might have the following `urls.py` file:

```python
from django.conf.urls import url
from . import views

urlpatterns = [
    url(r'^$', views.post_list, name='post_list'),
]
```

The `urlpatterns` variable is a list of URL patterns. Each URL pattern is a tuple of the following:

-   A regular expression that is used to match the URL
-   The view function that is called
-   The name of the URL

The `^$` regular expression matches the empty string. This URL pattern will match the `/` URL.

When the `/` URL is requested, the `post_list` view function will be called. The `post_list` view function will return the HTML for the page.

The name of the URL is used to identify the URL. This is useful for reversing URLs (i.e. generating URLs from view functions).

### Rendering Templates

Templates are used to render the HTML for Django views. Django comes with a built-in template engine, called the Django template engine.

The Django template engine takes a template and a context (a Python dictionary) and renders the template with the context data.

The template is rendered with the `render` function:

```python
def post_list(request):
    posts = Post.objects.all()
    return render(request, 'post_list.html', {'posts': posts})
```

The `render` function takes the `request` object, the name of the template, and the context data. The `render` function returns the HTML for the page.

The `post_list.html` template might look like this:

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

The `post_list.html` template loops through the `posts` variable and displays the `title` and `body` of each `Post`.

## Flask

Flask is a microframework for Python. It is designed to make the development process of web applications easier and faster. Flask comes with a few features out-of-the-box, such as a development server and a basic template engine.

Flask is a good choice for small and simple applications. It is also suitable for projects that require a high level of flexibility.

### Getting Started

To use Flask, you need to install it first. You can do this using the `pip` package manager:

```bash
pip install flask
```

Once Flask is installed, you can create a new file called `app.py` with the following code:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'Hello, World!'

if __name__ == '__main__':
    app.run()
```

This code will create a new Flask application. The `@app.route` decorator is used to map URLs to view functions. The `index` view function returns the string `Hello, World!`.

The `if __name__ == '__main__':` block is used to run the application. The `app.run` function will start a development server.

You can run the application using the `python` command:

```bash
python app.py
```

You can access the application at http://localhost:5000/.

### Creating an Application

Applications are the building blocks of Flask projects. A project can have multiple applications and each application can have different functionality.

To create a new application, create a new file called `app.py` with the following code:

```python
from flask import Flask

app = Flask(__name__)
```

This code will create a new Flask application.

### Defining Views

Views are the logic of Flask applications. They are used to handle the incoming HTTP requests and return the HTTP responses.

Views are Python functions that take an `HttpRequest` object as an argument and return an `HttpResponse` object.

For example, if you were building a blog application, you might have a view that displays a list of all the blog posts:

```python
@app.route('/')
def post_list():
    posts = Post.objects.all()
    return render_template('post_list.html', {'posts': posts})
```

The `post_list` view takes an `HttpRequest` object and returns an `HttpResponse` object. The `HttpResponse` object contains the HTML for the page that will be displayed.

The `post_list` view gets all the `Post` objects from the database and passes them to the `post_list.html` template. The `post_list.html` template renders the HTML for the page.

### Defining URLs

URLs are used to map views to specific URLs. They are defined in the `app.py` file.

For example, if you were building a blog application, you might have the following `app.py` file:

```python
@app.route('/')
def post_list():
    ...

@app.route('/posts/<int:post_id>')
def post_detail(post_id):
    ...
```

The `@app.route` decorator is used to map URLs to view functions. The `post_list` view function will be called when the `/` URL is requested. The `post_detail` view function will be called when the `/posts/<int:post_id>` URL is requested.

### Rendering Templates

Templates are used to render the HTML for Flask views. Flask comes with a built-in template engine, called the Jinja2 template engine.

The Jinja2 template engine takes a template and a context (a Python dictionary) and renders the template with the context data.

The template is rendered with the `render_template` function:

```python
@app.route('/')
def post_list():
    posts = Post.objects.all()
    return render_template('post_list.html', {'posts': posts})
```

The `render_template` function takes the name of the template and the context data. The `render_template` function returns the HTML for the page.

The `post_list.html` template might look like this:

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

The `post_list.html` template loops through the `posts` variable and displays the `title` and `body` of each `Post`.

## Conclusion

In this article, we have looked at two Python frameworks for backend development: Django and Flask. We have seen how to get started with each framework and how to create a basic application.