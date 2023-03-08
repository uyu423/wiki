---
title: Requests
description: 
published: true
date: 2023-02-08T02:18:03.235Z
tags: 
editor: markdown
dateCreated: 2023-02-08T02:18:00.933Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Requests***English** document is available*](/en/Knowledge-base/Dictionary/requests)
{.links-list}


# Descripción general

Requests es una biblioteca HTTP con licencia Apache2, escrita en Python, para seres humanos. Las solicitudes permiten a los usuarios realizar fácilmente solicitudes HTTP, como GET, POST, PUT y DELETE, a una URL específica. También admite autenticación, cookies y otras características.

# Descripción

Requests es una biblioteca popular de Python para realizar solicitudes HTTP. Está diseñado para ser simple e intuitivo para que lo usen los desarrolladores, con un enfoque en hacer que el proceso de hacer que las solicitudes HTTP sean más fáciles. Las solicitudes admiten una amplia gama de solicitudes HTTP, como GET, POST, PUT y DELETE. También proporciona soporte para autenticación, cookies y otras funciones.

Requests se basa en la popular biblioteca urllib3, que proporciona una interfaz de bajo nivel para realizar solicitudes HTTP. Requests usa urllib3 para proporcionar una API de nivel superior para realizar solicitudes HTTP, lo que facilita su uso.

Las solicitudes también proporcionan una serie de características prácticas, como la capacidad de especificar los datos que se enviarán con una solicitud y la capacidad de especificar un tiempo de espera para una solicitud.

# Historia

Requests fue creado originalmente en 2011 por Kenneth Reitz. Inicialmente se lanzó como un proyecto de código abierto en GitHub y rápidamente ganó popularidad entre los desarrolladores. Desde su lanzamiento inicial, Requests se ha convertido en una de las bibliotecas de Python más populares, con más de 10 millones de descargas.

# Características

Solicitudes proporciona una serie de funciones para facilitar a los desarrolladores la realización de solicitudes HTTP.

- Las solicitudes admiten una amplia gama de solicitudes HTTP, incluidas GET, POST, PUT y DELETE.
- Las solicitudes admiten la autenticación, lo que permite a los desarrolladores autenticarse fácilmente con un servicio web.
- Las solicitudes admiten cookies, lo que permite a los desarrolladores manejar fácilmente las cookies en sus solicitudes.
- Las solicitudes admiten datos, lo que permite a los desarrolladores especificar fácilmente los datos que se enviarán con una solicitud.
- Las solicitudes admiten tiempos de espera, lo que permite a los desarrolladores especificar un tiempo de espera para una solicitud.

# Ejemplo

Este es un ejemplo del uso de Solicitudes para realizar una solicitud GET a un servicio web:

```python
import requests

response = requests.get('http://example.com/api/v1/data')

if response.status_code == 200:
    data = response.json()
    print(data)
```

# Pros y contras

Ventajas:

- Fácil de usar: Solicitudes proporciona una API simple e intuitiva para realizar solicitudes HTTP.
- Amplia gama de solicitudes: Requests admite una amplia gama de solicitudes HTTP, como GET, POST, PUT y DELETE.
- Autenticación: las solicitudes admiten la autenticación, lo que facilita la autenticación con los servicios web.
- Cookies: Solicitudes admite cookies, lo que facilita el manejo de cookies en solicitudes.
- Datos: las solicitudes admiten datos, lo que facilita especificar los datos que se enviarán con una solicitud.
- Tiempos de espera: las solicitudes admiten tiempos de espera, lo que facilita especificar un tiempo de espera para una solicitud.

Contras:

- Soporte limitado para solicitudes que no sean HTTP: las solicitudes solo admiten solicitudes HTTP, por lo que no se puede usar para realizar solicitudes que no sean HTTP.
- No es compatible con la transmisión: Requests no admite la transmisión, por lo que no se puede usar para transmitir datos.

# Controversia

Las solicitudes han sido objeto de cierta controversia debido al uso de urllib3, que es una biblioteca de bajo nivel para realizar solicitudes HTTP. Algunos desarrolladores han argumentado que las solicitudes no deben usarse en producción debido a los posibles riesgos de seguridad que plantea urllib3.

# Tecnología relacionada

- urllib3: urllib3 es una biblioteca de bajo nivel para realizar solicitudes HTTP. Las solicitudes se basan en urllib3.
- Requests-toolbelt: Requests-toolbelt es una biblioteca para realizar solicitudes HTTP con Requests.
- Requests-mock: Requests-mock es una biblioteca para simular solicitudes HTTP con Requests.

# Digresión

Requests es una biblioteca popular para realizar solicitudes HTTP en Python. Está diseñado para ser fácil de usar y proporciona una amplia gama de funciones para facilitar la realización de solicitudes HTTP.

# Otros

Requests es un proyecto de código abierto, publicado bajo la Licencia Apache2. Se mantiene activamente y es ampliamente utilizado por los desarrolladores.