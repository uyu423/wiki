---
title: Scrapy
description: 
published: true
date: 2023-02-14T20:55:57.611Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:55:55.725Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Scrapy***English** document is available*](/en/Knowledge-base/Dictionary/scrapy)
{.links-list}


# Descripción general
Scrapy es un marco de rastreo web gratuito y de código abierto escrito en Python. Se utiliza para extraer datos de sitios web y se puede utilizar para una amplia gama de aplicaciones, como la extracción de datos, el procesamiento de información o el archivo histórico.

# Descripción
Scrapy es un marco de rastreo web que proporciona un conjunto de herramientas completo para extraer datos de sitios web. Está diseñado para ser rápido, simple y extensible. El marco se basa en la biblioteca de redes asíncronas Twisted y proporciona una interfaz de alto nivel para definir y ejecutar arañas web.

Las arañas Scrapy se pueden escribir en Python y usar una sintaxis simple para definir los datos que se extraerán de un sitio web. El marco proporciona un conjunto de funciones integradas, como soporte para seleccionar y extraer datos de documentos HTML y XML, así como soporte para seguir enlaces y raspar varias páginas. También incluye un servicio web para ejecutar arañas en la nube y una consola web para monitorear y administrar arañas.

Scrapy se utiliza para una variedad de aplicaciones, como la extracción de datos, el procesamiento de información o el archivo histórico. Se puede utilizar para extraer datos estructurados de sitios web, como información de contacto, listados de productos o precios. También se utiliza para automatizar tareas de web scraping, como recopilar datos de varias páginas o extraer datos de una sola página varias veces.

# Historia
Scrapy fue lanzado por primera vez en 2008 por Scrapinghub, una empresa de procesamiento de datos y web scraping. Fue creado como una alternativa de código abierto a las herramientas comerciales de web scraping y desde entonces se ha convertido en uno de los frameworks de web scraping más populares.

# Características
Scrapy proporciona una variedad de funciones para hacer que el web scraping sea más fácil y eficiente:

- Soporte para seleccionar y extraer datos de documentos HTML y XML.
- Soporte para seguir enlaces y raspar varias páginas.
- Compatibilidad integrada para extraer datos de sitios web renderizados con JavaScript.
- Un servicio web para ejecutar arañas en la nube.
- Una consola web para monitorear y administrar arañas.
- Una interfaz de línea de comandos para ejecutar arañas.
- Un sistema de complementos para ampliar el marco.

# Ejemplo
Aquí hay un ejemplo de una araña Scrapy que extrae datos de un sitio web:

```python
import scrapy

class MySpider(scrapy.Spider):
    name = "myspider"
    start_urls = ["http://example.com/"]
    
    def parse(self, response):
        for product in response.css('div.product'):
            yield {
                'name': product.css('h3.name::text').get(),
                'price': product.css('span.price::text').get(),
            }
```

# Pros y contras
Scrapy ofrece una gama de características que lo convierten en una poderosa herramienta para el web scraping. Es rápido, fácil de usar y extensible. También proporciona soporte integrado para extraer datos de sitios web renderizados con JavaScript.

Sin embargo, Scrapy no es adecuado para todas las tareas de web scraping. Se limita a extraer datos de sitios web y no admite otros tipos de fuentes de datos, como bases de datos o API.

# Tecnología relacionada
Scrapy está relacionado con otros marcos de web scraping como Beautiful Soup y Selenium. También está relacionado con servicios de web scraping como Apify y ParseHub.

# Digresión
Scrapy no solo se usa para el web scraping, sino que también se puede usar para tareas de automatización web, como completar formularios y enviar datos.

# Otros
Scrapy es un marco popular de web scraping de código abierto escrito en Python. Se utiliza para extraer datos de sitios web y se puede utilizar para una amplia gama de aplicaciones. Proporciona un conjunto de funciones para hacer que el web scraping sea más fácil y eficiente, como soporte para seleccionar y extraer datos de documentos HTML y XML, así como soporte para seguir enlaces y scraping de varias páginas.