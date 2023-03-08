---
title: Kotlin y Django: creación de una aplicación web con un marco de Python
description: 
published: true
date: 2023-02-03T13:56:31.888Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:56:30.208Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Django: Building a Web Application with a Python Framework***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-django-building-a-web-application-with-a-python-framework)
{.links-list}


# Kotlin y Django: Construyendo una Aplicación Web con un Framework Python

Django es un marco web de Python que fomenta el desarrollo rápido y el diseño limpio y pragmático. Django es gratuito y de código abierto, y se encarga de gran parte de las molestias del desarrollo web, por lo que puede concentrarse en escribir su aplicación sin necesidad de reinventar la rueda. También es fácil de aprender y no lleva mucho tiempo ponerlo en marcha.

Kotlin es un lenguaje de programación tipificado estáticamente para aplicaciones multiplataforma modernas. Kotlin es 100% interoperable con Java, por lo que es fácil comenzar con Kotlin si ya está familiarizado con Java. Kotlin también es más conciso que Java, por lo que puede escribir menos código y hacer más.

En este artículo, le mostraremos cómo crear una aplicación web utilizando el marco web Django y el lenguaje de programación Kotlin. Lo guiaremos a través de los pasos para configurar un entorno de desarrollo, crear un nuevo proyecto Django y agregar una página simple al proyecto. Al final de este artículo, tendrá una comprensión básica de cómo crear una aplicación web con Django y Kotlin.

## Configuración de su entorno de desarrollo

Antes de que pueda comenzar a crear su aplicación web, deberá configurar un entorno de desarrollo. Si es nuevo en Python, le recomendamos que use Anaconda, que es una distribución de Python que incluye los paquetes de Python más populares para la ciencia de datos.

Si está utilizando Anaconda, puede instalar Django con el siguiente comando:

```
conda install -c anaconda django
```

Si no está utilizando Anaconda, puede instalar Django con el administrador de paquetes pip:

```
pip install django
```

Puede verificar que Django esté instalado ejecutando el siguiente comando:

```
django-admin --version
```

Debería ver el número de versión de Django impreso en la consola.

Ahora que tiene instalado Django, está listo para crear su primer proyecto Django.

## Creando un nuevo proyecto Django

Django usa una estructura de proyecto para organizar todos los archivos y el código de una aplicación web. Un proyecto puede contener varias aplicaciones y cada aplicación puede tener un propósito específico. Por ejemplo, puede tener una aplicación para administrar publicaciones de blog, otra aplicación para administrar cuentas de usuario y otra aplicación para administrar comentarios.

Para crear un nuevo proyecto de Django, abra una ventana de terminal y navegue hasta el directorio donde desea almacenar su proyecto. Luego, ejecuta el siguiente comando:

```
django-admin startproject mysite
```

Reemplace "misitio" con el nombre de su proyecto. Este comando creará un nuevo directorio llamado “misitio” con la siguiente estructura:

```
mysite/
    manage.py
    mysite/
        __init__.py
        settings.py
        urls.py
        wsgi.py
```

El archivo “manage.py” es un script que lo ayuda a administrar su proyecto Django. El directorio "misitio" contiene los archivos y el código de su proyecto. El archivo "settings.py" contiene las configuraciones para su proyecto Django. El archivo "urls.py" contiene los patrones de URL para su proyecto. El archivo "wsgi.py" se usa para implementar su proyecto Django en un servidor web.

Puede obtener más información sobre la estructura del proyecto Django en la [documentación de Django] (https://docs.djangoproject.com/en/3.0/intro/tutorial01/).

## Agregar una página simple al proyecto

Ahora que tiene un proyecto Django, puede agregar una aplicación al proyecto. Una aplicación es un paquete de Python que contiene todos los archivos y el código para un propósito específico.

Para crear una aplicación, abra una ventana de terminal y navegue hasta el directorio "misitio". Luego, ejecuta el siguiente comando:

```
django-admin startapp myapp
```

Reemplace "myapp" con el nombre de su aplicación. Este comando creará un nuevo directorio llamado “myapp” con la siguiente estructura:

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

El archivo “admin.py” se usa para el sitio de administración de Django. El archivo "apps.py" se utiliza para configurar su aplicación. El archivo "models.py" se usa para definir los modelos para su aplicación. El archivo "tests.py" se utiliza para pruebas unitarias. El archivo "views.py" contiene las vistas de su aplicación.

Puede obtener más información sobre los archivos en una aplicación de Django en la [documentación de Django] (https://docs.djangoproject.com/en/3.0/intro/tutorial02/).

Ahora que tiene una aplicación, puede agregar una vista a la aplicación. Una vista es una función de Python que toma una solicitud HTTP y devuelve una respuesta HTTP.

Abra el archivo "views.py" en su editor de texto y agregue el siguiente código:

```python
from django.shortcuts import render

def index(request):
    return render(request, 'index.html')
```

Este código define una vista llamada "índice" que representa la plantilla "index.html".

A continuación, deberá crear la plantilla "index.html". Django usa el lenguaje de plantillas [Jinja](https://jinja.palletsprojects.com/) para generar plantillas HTML.

Cree un nuevo directorio llamado "plantillas" en el directorio "misitio". Luego, crea un nuevo archivo llamado “index.html” en el directorio “templates” con el siguiente código:

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

Este código define una página HTML simple que muestra el texto "¡Hola, mundo!"

A continuación, deberá configurar el archivo "mysite/urls.py" para asignar la URL "/" a la vista "índice". Abra el archivo “mysite/urls.py” en su editor de texto y agregue el siguiente código:

```python
from django.contrib import admin
from django.urls import path

from myapp.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', index),
]
```

Este código importa la vista de "índice" de la aplicación "myapp" y asigna la URL "/" a la vista de "índice".

Ahora que tiene una vista y un patrón de URL, puede ejecutar el servidor de desarrollo Django y ver su página en un navegador web.

Para ejecutar el servidor de desarrollo de Django, abra una ventana de terminal y navegue hasta el directorio "misitio". Luego, ejecuta el siguiente comando:

```
python manage.py runserver
```

Debería ver el siguiente resultado:

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

El servidor de desarrollo de Django ahora se ejecuta en http://127.0.0.1:8000/. Puede ver su página en un navegador web visitando http://127.0.0.1:8000/.

Deberías ver la siguiente página:

![Página de Django](https://www.tutorialspoint.com/django/images/django_page.jpg)

## ¡Felicidades!

Ha creado con éxito una aplicación web utilizando el marco web Django y el lenguaje de programación Kotlin. En este artículo, ha aprendido cómo configurar un entorno de desarrollo, crear un nuevo proyecto Django y agregar una página simple al proyecto.

Puede encontrar el código fuente de este artículo en [GitHub](https://github.com/tutorialspoint/kotlin-django-example).

## Referencias

- [Documentación de Django](https://docs.djangoproject.com/en/3.0/)
- [Documentación de Kotlin](https://kotlinlang.org/docs/reference/)
- [Tutoriales de Django](https://www.tutorialspoint.com/django/index.htm)
- [Tutoriales de Kotlin](https://www.tutorialspoint.com/kotlin/index.htm)