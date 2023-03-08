---
title: AWS Comprehend: análisis de datos de texto con procesamiento de lenguaje natural
description: 
published: true
date: 2023-02-14T21:17:26.018Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:17:18.357Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Comprehend: Analyzing Text Data with Natural Language Processing***English** document is available*](/en/Knowledge-base/Cloud/aws-comprehend-analyzing-text-data-with-natural-language-processing)
{.links-list}



# AWS Comprehend: análisis de datos de texto con procesamiento de lenguaje natural

Los datos de texto están en todas partes. Está en los libros que leemos, las noticias que consumimos, las publicaciones en las redes sociales que compartimos y las reseñas de los clientes en las que confiamos al tomar decisiones de compra. Estos datos pueden ser increíblemente valiosos, pero solo si podemos extraer el significado de ellos.

El procesamiento del lenguaje natural (NLP) es un campo de la informática y la inteligencia artificial que se ocupa de las interacciones entre las computadoras y los lenguajes humanos (naturales). NLP se utiliza para crear aplicaciones que pueden interpretar y extraer automáticamente el significado de los datos de texto.

AWS Comprehend es un servicio de NLP completamente administrado que facilita la extracción del significado de los datos de texto. En este artículo, veremos cómo usar AWS Comprehend para analizar datos de texto.

## Primeros pasos con AWS Comprehend

Antes de que podamos comenzar a utilizar AWS Comprehend, debemos configurar una cuenta de AWS y crear un usuario de IAM con permisos para acceder al servicio.

Una vez que tenga una cuenta de AWS, puede crear un usuario de IAM con la siguiente política:

```{language} {code}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "comprehend:*"
            ],
            "Resource": "*"
        }
    ]
}
```

Con el usuario de IAM en su lugar, ahora podemos crear un recurso de AWS Comprehend. Para hacer esto, debemos iniciar sesión en la consola de administración de AWS y navegar hasta el servicio AWS Comprehend.

Una vez que estemos en la consola de AWS Comprehend, podemos crear un nuevo recurso. Tendremos que proporcionar un nombre para el recurso, seleccionar la región y elegir el rol de IAM que creamos anteriormente.

Con el recurso creado, ahora estamos listos para comenzar a usar AWS Comprehend.

## Análisis de datos de texto

AWS Comprehend nos proporciona varias formas diferentes de analizar datos de texto. En esta sección, echaremos un vistazo a algunas de las funciones más utilizadas.

### Análisis de los sentimientos

El análisis de opinión es una forma de extraer automáticamente la opinión (positiva, negativa o neutral) de un texto. Esto puede ser útil para una variedad de aplicaciones, como determinar el sentimiento general de una revisión de un cliente o comprender el sentimiento de las publicaciones en las redes sociales.

Para realizar un análisis de opinión con AWS Comprehend, necesitaremos proporcionar el texto que queremos analizar. Podemos hacer esto ingresando directamente el texto o proporcionando una URL donde se encuentra el texto.

Una vez que hayamos proporcionado el texto, AWS Comprehend lo analizará y nos proporcionará la opinión del texto.

### Extracción de frases clave

La extracción de frases clave es una forma de identificar automáticamente las frases clave en un texto. Esto puede ser útil para una variedad de aplicaciones, como identificar los temas de una revisión de un cliente o comprender los temas de las publicaciones en las redes sociales.

Para realizar la extracción de frases clave con AWS Comprehend, necesitaremos proporcionar el texto que queremos analizar. Podemos hacer esto ingresando directamente el texto o proporcionando una URL donde se encuentra el texto.

Una vez que hayamos proporcionado el texto, AWS Comprehend lo analizará y nos proporcionará las frases clave que ha extraído.

### Detección de idioma

La detección de idioma es una forma de identificar automáticamente el idioma de un texto. Esto puede ser útil para una variedad de aplicaciones, como identificar el idioma de la reseña de un cliente o comprender el idioma de las publicaciones en las redes sociales.

Para realizar la detección de idioma con AWS Comprehend, necesitaremos proporcionar el texto que queremos analizar. Podemos hacer esto ingresando directamente el texto o proporcionando una URL donde se encuentra el texto.

Una vez que hayamos proporcionado el texto, AWS Comprehend lo analizará y nos proporcionará el idioma que ha detectado.

## Conclusión

En este artículo, analizamos cómo utilizar AWS Comprehend para analizar datos de texto. Hemos visto cómo utilizar AWS Comprehend para realizar análisis de opiniones, extracción de frases clave y detección de idiomas.

Si bien solo hemos arañado la superficie de lo que es posible con AWS Comprehend, esto debería ser suficiente para comenzar.