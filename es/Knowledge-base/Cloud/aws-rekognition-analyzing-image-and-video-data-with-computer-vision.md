---
title: AWS Rekognition: análisis de datos de imágenes y videos con visión artificial
description: 
published: true
date: 2023-02-05T17:55:21.898Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:55:20.301Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Rekognition: Analyzing Image and Video Data with Computer Vision***English** document is available*](/en/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}


# AWS Rekognition: análisis de datos de imágenes y videos con visión artificial

AWS Rekognition es un servicio basado en la nube que facilita agregar análisis visuales potentes a sus aplicaciones. Con Rekognition, puede detectar objetos, escenas y rostros en imágenes y videos, así como identificar contenido inapropiado. Rekognition también proporciona reconocimiento facial y análisis facial de alta precisión, como la detección de emociones, género y rango de edad. Puede usar estas funciones para crear aplicaciones más inteligentes que pueden moderar contenido automáticamente, personalizar experiencias para sus clientes y mejorar la seguridad.

Rekognition utiliza algoritmos de aprendizaje profundo para brindar estas capacidades. El aprendizaje profundo es un tipo de aprendizaje automático que enseña a las computadoras a aprender de los datos, sin estar programados explícitamente. El aprendizaje profundo es parte de una familia más amplia de métodos de aprendizaje automático basados en el aprendizaje de representaciones de datos, a diferencia de los algoritmos específicos de tareas.

## ¿Por qué usar reconocimiento?

Rekognition facilita la adición de análisis visuales potentes a sus aplicaciones. Con Rekognition, puede detectar objetos, rostros y escenas en imágenes y videos, así como identificar contenido inapropiado. Rekognition también proporciona reconocimiento facial y análisis facial de alta precisión. Puede usar estas funciones para crear aplicaciones más inteligentes que pueden moderar contenido automáticamente, personalizar experiencias para sus clientes y mejorar la seguridad.

## Primeros pasos con Rekognition

Para comenzar con Rekognition, primero debe crear una cuenta de AWS y registrarse en el servicio. A continuación, puede crear un proyecto de Rekognition en la Consola de administración de AWS. Un proyecto de Rekognition es un contenedor lógico para todos los recursos que necesita para usar Rekognition. Después de crear un proyecto, puede agregar imágenes y videos para analizar y configurar depósitos de Amazon Simple Storage Service (Amazon S3) para almacenar los resultados de su análisis.

## Análisis de imágenes y videos

Rekognition facilita el análisis de imágenes y videos para una amplia variedad de casos de uso, como la identificación de objetos, rostros y escenas; detectar contenido inapropiado; y el reconocimiento de celebridades y puntos de referencia.

Rekognition proporciona dos formas principales de analizar imágenes y videos:

* **DetectLabels** devuelve una lista de etiquetas (como "Perro" o "Gato") que se detectan en una imagen. Cada etiqueta también incluye una puntuación de confianza que indica qué tan seguro está Rekognition de que la etiqueta se identificó correctamente.

* **DetectModerationLabels** devuelve una lista de etiquetas que identifican contenido inseguro o inapropiado en una imagen. Por ejemplo, una etiqueta como "Lascivo" o "Violencia" indica que la imagen contiene contenido para adultos. Cada etiqueta también incluye una puntuación de confianza que indica qué tan seguro está Rekognition de que la etiqueta se identificó correctamente.

También puede usar la operación **AnalyzeFaces** para analizar caras en una imagen y obtener información sobre las caras, como las emociones que se detectan, la edad estimada de la cara, si la cara lleva gafas de sol y más.

## Reconocimiento de celebridades y puntos de referencia

Rekognition puede reconocer celebridades y puntos de referencia en las imágenes. Por ejemplo, puede usar la operación **RecognizeCelebrities** para identificar celebridades en una imagen. También puede usar la operación **Detectar etiquetas** para identificar puntos de referencia en una imagen.

## Implementando el Reconocimiento

Rekognition es un servicio web al que puede llamar utilizando los SDK de AWS. Puede llamar a Rekognition mediante la consola de administración de AWS, la interfaz de línea de comandos de AWS o mediante programación mediante uno de los SDK de AWS.

## Precios

Rekognition le cobra por la cantidad de imágenes y videos que analiza y los metadatos faciales que almacena. Rekognition no le cobra por la cantidad de imágenes y videos que almacena.

## Recursos

* [Reconocimiento de AWS](https://aws.amazon.com/rekognition/)
* [Detectar etiquetas] (https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectLabels.html)
* [Detectar etiquetas de moderación] (https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectModerationLabels.html)
* [AnalyzeFaces](https://docs.aws.amazon.com/rekognition/latest/dg/API_AnalyzeFaces.html)
* [Reconocer Celebridades](https://docs.aws.amazon.com/rekognition/latest/dg/API_RecognizeCelebrities.html)
* [SDK de AWS](https://aws.amazon.com/tools/)
* [Precio](https://aws.amazon.com/rekognition/pricing/)