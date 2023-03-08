---
title: Cómo crear un sitio web con Django
description: 
published: true
date: 2023-02-02T22:58:21.277Z
tags: 
editor: markdown
dateCreated: 2023-02-02T22:58:16.466Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [How to Create a Website with Django***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-website-with-django)
{.links-list}


# Cómo crear un sitio web con Django

Django es un marco web de alto nivel escrito en Python que fomenta un desarrollo rápido y un diseño limpio y pragmático. Creado por desarrolladores experimentados, se encarga de gran parte de las molestias del desarrollo web, por lo que puede concentrarse en escribir su aplicación sin necesidad de reinventar la rueda. Es gratis y de código abierto.

Django es una excelente opción para desarrollar aplicaciones web modernas. Es un marco con pilas incluidas que facilita muchas tareas comunes de desarrollo web.

## ¿Qué es Django?

Django es un marco web basado en Python que le permite crear rápidamente aplicaciones web sin la molestia de configurar un entorno de desarrollo, administrar dependencias, etc.

Django incluye muchas características integradas, como:

- Un ORM para interactuar con bases de datos.
- Un sistema de plantillas para crear páginas HTML
- Un servidor web basado en Python
- Un sistema de formularios
- Un sistema de autenticación.

Django también es muy extensible. Hay muchos paquetes de terceros que puede usar para agregar funciones adicionales a su aplicación web Django.

## ¿Por qué usar Django?

Django es una gran opción por muchas razones. Es un marco con pilas incluidas que facilita muchas tareas comunes de desarrollo web.

Algunos de los beneficios de usar Django son:

- Django se ocupa de muchas de las molestias del desarrollo web, por lo que puede concentrarse en escribir su aplicación.
- Django tiene muchas funciones integradas, como un ORM, un sistema de plantillas y un servidor web basado en Python.
- Django es muy extensible. Hay muchos paquetes de terceros que puede usar para agregar funciones adicionales a su aplicación web Django.
- Django es de código abierto y gratuito.

## Django frente a otros marcos

Hay muchos marcos web diferentes disponibles para Python. Entonces, ¿por qué deberías usar Django?

Estas son algunas de las razones por las que Django podría ser una buena opción para ti:

- Si desea un marco con baterías incluidas: Django incluye muchas funciones integradas, como un ORM, un sistema de plantillas y un servidor web basado en Python.
- Si quieres un marco que sea extensible: Django es muy extensible. Hay muchos paquetes de terceros que puede usar para agregar funciones adicionales a su aplicación web Django.
- Si desea un marco que sea de código abierto y gratuito: Django es de código abierto y gratuito.

## Primeros pasos con Django

Ahora que sabe qué es Django y por qué es posible que desee usarlo, veamos el proceso de configuración de una aplicación web de Django.

### Configuración de un entorno de desarrollo

Lo primero que deberá hacer es configurar un entorno de desarrollo. Recomiendo usar virtualenv para crear un entorno de desarrollo aislado.

Para instalar virtualenv, ejecute el siguiente comando:

```
pip install virtualenv
```

Una vez que virtualenv está instalado, puede crear un nuevo entorno virtual ejecutando el siguiente comando:

```
virtualenv myproject
```

Esto creará un nuevo directorio llamado myproject que contiene un entorno de desarrollo de Python aislado.

Para activar el entorno virtual, ejecute el siguiente comando:

```
source myproject/bin/activate
```

Ahora podrá instalar paquetes en el entorno virtual sin afectar los paquetes que están instalados globalmente en su sistema.

### Instalando Django

Una vez que haya configurado su entorno de desarrollo, puede instalar Django. Para instalar Django, ejecute el siguiente comando:

```
pip install django
```

Esto instalará Django y todas las dependencias requeridas.

### Creando un Proyecto Django

Ahora que Django está instalado, puede crear un nuevo proyecto de Django. Para hacer esto, ejecute el siguiente comando:

```
django-admin startproject myproject
```

Esto creará un nuevo directorio llamado myproject que contiene los archivos para su proyecto Django.

### Ejecutar el servidor de desarrollo de Django

Ahora que tiene un proyecto de Django, puede iniciar el servidor de desarrollo de Django. Para hacer esto, ejecute el siguiente comando:

```
python manage.py runserver
```

Esto iniciará el servidor de desarrollo de Django y hará que su proyecto Django esté disponible en http://127.0.0.1:8000/.

## URL de Django

Una de las partes más importantes de una aplicación web de Django es la configuración de URL. La configuración de URL es un conjunto de patrones que Django usará para hacer coincidir las URL entrantes.

Cada patrón en la configuración de URL se asigna a una función de visualización. Cuando un usuario solicita una URL que coincide con un patrón, Django llamará a la función de vista correspondiente y devolverá el resultado.

Por ejemplo, considere la siguiente configuración de URL:

```
urlpatterns = [
    url(r'^

Esta configuración de URL tiene dos patrones. El primer patrón coincide con la cadena vacía y la asigna a la función de vista myapp.views.home. El segundo patrón coincide con la cadena 'acerca de/' y la asigna a la función de vista myapp.views.about.

Las funciones de vista son funciones de Python que toman un objeto HttpRequest como su primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

## Vistas de Django

Las vistas son el corazón de una aplicación web de Django. Las vistas son funciones de Python que toman un objeto HttpRequest como primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
from django.http import HttpResponse

def home(request):
    return HttpResponse('Hello, world!')
```

Las funciones de visualización pueden hacer cualquier cosa que pueda hacer en una función de Python. Esto significa que pueden acceder a los datos de la base de datos, realizar cálculos, etc.

La única regla es que deben devolver un objeto HttpResponse.

## Plantillas Django

Una de las partes más importantes de una aplicación web de Django es el sistema de plantillas. El sistema de plantillas se utiliza para representar páginas HTML.

Django viene con un sistema de plantillas incorporado que es similar al que se usa en el motor de plantillas Jinja2.

Para usar el sistema de plantillas de Django, primero debe crear una plantilla. Una plantilla es un archivo que contiene el HTML de una página web de Django.

Aquí hay una plantilla simple que solo contiene la cadena '¡Hola, mundo!':

```
{% extends 'base.html' %}

{% block content %}
Hello, world!
{% endblock %}
```

Una vez que haya creado una plantilla, puede renderizarla utilizando la función render(). La función render() toma el nombre de la plantilla y un diccionario de datos de contexto.

Aquí hay un ejemplo de cómo renderizar la plantilla que acabamos de crear:

```
from django.shortcuts import render

def home(request):
    return render(request, 'home.html', {})
```

## Formularios de Django

Django viene con un sistema de formularios incorporado que facilita la creación de formularios HTML.

Para usar el sistema de formularios de Django, primero debe crear un formulario. Un formulario es una clase de Python que define los campos que se representarán como elementos de formulario HTML.

Aquí hay un formulario simple que solo tiene un solo campo de texto:

```
from django import forms

class MyForm(forms.Form):
    myfield = forms.CharField(max_length=100)
```

Una vez que haya creado un formulario, puede representarlo en una plantilla usando la etiqueta {% form %}.

La etiqueta {% form %} toma el objeto de formulario como primer argumento y un diccionario de datos de contexto como segundo argumento.

Aquí hay un ejemplo de cómo representar el formulario que acabamos de crear:

```
{% form form %}
    {{ form.myfield }}
{% endform %}
```

## Modelos Django

Django viene con un sistema de modelo incorporado que facilita el trabajo con datos en una base de datos.

Para usar el sistema de modelos de Django, primero debe crear un modelo. Un modelo es una clase de Python que define los campos y el comportamiento de un objeto de datos.

Aquí hay un modelo simple que solo tiene un solo campo:

```
from django.db import models

class MyModel(models.Model):
    myfield = models.CharField(max_length=100)
```

Una vez que haya creado un modelo, puede usar el administrador de Django para agregar, editar y eliminar objetos.

También puede usar la API modelo de Django para consultar la base de datos y crear, actualizar y eliminar objetos.

## Administrador de Django

Django viene con un sistema de administración incorporado que facilita la administración de datos en una base de datos.

Para usar el administrador de Django, primero debe crear un usuario administrador. Un usuario administrador es un usuario al que se le ha otorgado permiso para acceder al administrador de Django.

Para crear un usuario administrador, ejecute el siguiente comando:

```
python manage.py createsuperuser
```

Una vez que haya creado un usuario administrador, puede iniciar sesión en el administrador de Django yendo a http://127.0.0.1:8000/admin/.

Una vez que haya iniciado sesión, verá la interfaz de administración de Django. Desde aquí, puede agregar, editar y eliminar objetos.

## Conclusión

Django es una excelente opción para desarrollar aplicaciones web modernas. Es un marco con pilas incluidas que facilita muchas tareas comunes de desarrollo web.

Si eres nuevo en Django, te recomiendo consultar la documentación de Django. Es un gran recurso para aprender sobre todas las características del framework Django., 'myapp.views.home'),
    url(r'^about/

Esta configuración de URL tiene dos patrones. El primer patrón coincide con la cadena vacía y la asigna a la función de vista myapp.views.home. El segundo patrón coincide con la cadena 'acerca de/' y la asigna a la función de vista myapp.views.about.

Las funciones de vista son funciones de Python que toman un objeto HttpRequest como su primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
de django.http importar HttpResponse

def casa (solicitud):
    return HttpResponse('¡Hola, mundo!')
```

## Vistas de Django

Las vistas son el corazón de una aplicación web de Django. Las vistas son funciones de Python que toman un objeto HttpRequest como primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
de django.http importar HttpResponse

def casa (solicitud):
    return HttpResponse('¡Hola, mundo!')
```

Las funciones de visualización pueden hacer cualquier cosa que pueda hacer en una función de Python. Esto significa que pueden acceder a los datos de la base de datos, realizar cálculos, etc.

La única regla es que deben devolver un objeto HttpResponse.

## Plantillas Django

Una de las partes más importantes de una aplicación web de Django es el sistema de plantillas. El sistema de plantillas se utiliza para representar páginas HTML.

Django viene con un sistema de plantillas incorporado que es similar al que se usa en el motor de plantillas Jinja2.

Para usar el sistema de plantillas de Django, primero debe crear una plantilla. Una plantilla es un archivo que contiene el HTML de una página web de Django.

Aquí hay una plantilla simple que solo contiene la cadena '¡Hola, mundo!':

```
{% extiende 'base.html' %}

{% contenido del bloque %}
¡Hola Mundo!
{% bloque final %}
```

Una vez que haya creado una plantilla, puede renderizarla utilizando la función render(). La función render() toma el nombre de la plantilla y un diccionario de datos de contexto.

Aquí hay un ejemplo de cómo renderizar la plantilla que acabamos de crear:

```
desde django.shortcuts importación render

def casa (solicitud):
    volver render (solicitud, 'home.html', {})
```

## Formularios de Django

Django viene con un sistema de formularios incorporado que facilita la creación de formularios HTML.

Para usar el sistema de formularios de Django, primero debe crear un formulario. Un formulario es una clase de Python que define los campos que se representarán como elementos de formulario HTML.

Aquí hay un formulario simple que solo tiene un solo campo de texto:

```
desde formularios de importación de django

clase MiFormulario(formularios.Formulario):
    micampo = formularios.CharField(max_length=100)
```

Una vez que haya creado un formulario, puede representarlo en una plantilla usando la etiqueta {% form %}.

La etiqueta {% form %} toma el objeto de formulario como primer argumento y un diccionario de datos de contexto como segundo argumento.

Aquí hay un ejemplo de cómo representar el formulario que acabamos de crear:

```
{% formulario formulario%}
    {{ formulario.micampo }}
{% endform %}
```

## Modelos Django

Django viene con un sistema de modelo incorporado que facilita el trabajo con datos en una base de datos.

Para usar el sistema de modelos de Django, primero debe crear un modelo. Un modelo es una clase de Python que define los campos y el comportamiento de un objeto de datos.

Aquí hay un modelo simple que solo tiene un solo campo:

```
desde modelos de importación django.db

clase MiModelo(modelos.Modelo):
    micampo = modelos.CharField(max_length=100)
```

Una vez que haya creado un modelo, puede usar el administrador de Django para agregar, editar y eliminar objetos.

También puede usar la API modelo de Django para consultar la base de datos y crear, actualizar y eliminar objetos.

## Administrador de Django

Django viene con un sistema de administración incorporado que facilita la administración de datos en una base de datos.

Para usar el administrador de Django, primero debe crear un usuario administrador. Un usuario administrador es un usuario al que se le ha otorgado permiso para acceder al administrador de Django.

Para crear un usuario administrador, ejecute el siguiente comando:

```
python manage.py crear superusuario
```

Una vez que haya creado un usuario administrador, puede iniciar sesión en el administrador de Django yendo a http://127.0.0.1:8000/admin/.

Una vez que haya iniciado sesión, verá la interfaz de administración de Django. Desde aquí, puede agregar, editar y eliminar objetos.

## Conclusión

Django es una excelente opción para desarrollar aplicaciones web modernas. Es un marco con pilas incluidas que facilita muchas tareas comunes de desarrollo web.

Si eres nuevo en Django, te recomiendo consultar la documentación de Django. Es un gran recurso para aprender sobre todas las características del framework Django., 'myapp.views.about'),
]
```

Esta configuración de URL tiene dos patrones. El primer patrón coincide con la cadena vacía y la asigna a la función de vista myapp.views.home. El segundo patrón coincide con la cadena 'acerca de/' y la asigna a la función de vista myapp.views.about.

Las funciones de vista son funciones de Python que toman un objeto HttpRequest como su primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
de django.http importar HttpResponse

def casa (solicitud):
    return HttpResponse('¡Hola, mundo!')
```

## Vistas de Django

Las vistas son el corazón de una aplicación web de Django. Las vistas son funciones de Python que toman un objeto HttpRequest como primer argumento y devuelven un objeto HttpResponse.

Aquí hay una función de vista simple que devuelve un objeto HttpResponse con la cadena '¡Hola, mundo!':

```
de django.http importar HttpResponse

def casa (solicitud):
    return HttpResponse('¡Hola, mundo!')
```

Las funciones de visualización pueden hacer cualquier cosa que pueda hacer en una función de Python. Esto significa que pueden acceder a los datos de la base de datos, realizar cálculos, etc.

La única regla es que deben devolver un objeto HttpResponse.

## Plantillas Django

Una de las partes más importantes de una aplicación web de Django es el sistema de plantillas. El sistema de plantillas se utiliza para representar páginas HTML.

Django viene con un sistema de plantillas incorporado que es similar al que se usa en el motor de plantillas Jinja2.

Para usar el sistema de plantillas de Django, primero debe crear una plantilla. Una plantilla es un archivo que contiene el HTML de una página web de Django.

Aquí hay una plantilla simple que solo contiene la cadena '¡Hola, mundo!':

```
{% extiende 'base.html' %}

{% contenido del bloque %}
¡Hola Mundo!
{% bloque final %}
```

Una vez que haya creado una plantilla, puede renderizarla utilizando la función render(). La función render() toma el nombre de la plantilla y un diccionario de datos de contexto.

Aquí hay un ejemplo de cómo renderizar la plantilla que acabamos de crear:

```
desde django.shortcuts importación render

def casa (solicitud):
    volver render (solicitud, 'home.html', {})
```

## Formularios de Django

Django viene con un sistema de formularios incorporado que facilita la creación de formularios HTML.

Para usar el sistema de formularios de Django, primero debe crear un formulario. Un formulario es una clase de Python que define los campos que se representarán como elementos de formulario HTML.

Aquí hay un formulario simple que solo tiene un solo campo de texto:

```
desde formularios de importación de django

clase MiFormulario(formularios.Formulario):
    micampo = formularios.CharField(max_length=100)
```

Una vez que haya creado un formulario, puede representarlo en una plantilla usando la etiqueta {% form %}.

La etiqueta {% form %} toma el objeto de formulario como primer argumento y un diccionario de datos de contexto como segundo argumento.

Aquí hay un ejemplo de cómo representar el formulario que acabamos de crear:

```
{% formulario formulario%}
    {{ formulario.micampo }}
{% endform %}
```

## Modelos Django

Django viene con un sistema de modelo incorporado que facilita el trabajo con datos en una base de datos.

Para usar el sistema de modelos de Django, primero debe crear un modelo. Un modelo es una clase de Python que define los campos y el comportamiento de un objeto de datos.

Aquí hay un modelo simple que solo tiene un solo campo:

```
desde modelos de importación django.db

clase MiModelo(modelos.Modelo):
    micampo = modelos.CharField(max_length=100)
```

Una vez que haya creado un modelo, puede usar el administrador de Django para agregar, editar y eliminar objetos.

También puede usar la API modelo de Django para consultar la base de datos y crear, actualizar y eliminar objetos.

## Administrador de Django

Django viene con un sistema de administración incorporado que facilita la administración de datos en una base de datos.

Para usar el administrador de Django, primero debe crear un usuario administrador. Un usuario administrador es un usuario al que se le ha otorgado permiso para acceder al administrador de Django.

Para crear un usuario administrador, ejecute el siguiente comando:

```
python manage.py crear superusuario
```

Una vez que haya creado un usuario administrador, puede iniciar sesión en el administrador de Django yendo a http://127.0.0.1:8000/admin/.

Una vez que haya iniciado sesión, verá la interfaz de administración de Django. Desde aquí, puede agregar, editar y eliminar objetos.

## Conclusión

Django es una excelente opción para desarrollar aplicaciones web modernas. Es un marco con pilas incluidas que facilita muchas tareas comunes de desarrollo web.

Si eres nuevo en Django, te recomiendo consultar la documentación de Django. Es un gran recurso para aprender sobre todas las características del framework Django.