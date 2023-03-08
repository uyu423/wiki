---
title: AWS SageMaker: creación e implementación de modelos de aprendizaje automático en la nube
description: 
published: true
date: 2023-02-03T12:17:46.616Z
tags: 
editor: markdown
dateCreated: 2023-02-03T12:17:44.967Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS SageMaker: Building and Deploying Machine Learning Models in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}


# AWS SageMaker: creación e implementación de modelos de aprendizaje automático en la nube

El aprendizaje automático es un campo de la informática en rápido crecimiento que permite que las computadoras aprendan de los datos sin ser programadas explícitamente. El aprendizaje automático ya se está utilizando en una variedad de aplicaciones, como sistemas de recomendación, reconocimiento de imágenes y detección de fraudes.

AWS SageMaker es un servicio completamente administrado que brinda a los desarrolladores y científicos de datos la capacidad de crear, entrenar e implementar modelos de aprendizaje automático en la nube. SageMaker elimina el trabajo pesado de cada paso del proceso de aprendizaje automático, lo que facilita el desarrollo de modelos de alta calidad.

## Primeros pasos con SageMaker

Para comenzar con SageMaker, primero debe crear una cuenta de AWS y registrarse en SageMaker. Una vez que tenga una cuenta, puede crear una instancia de Amazon Elastic Compute Cloud (Amazon EC2) para utilizarla como su entorno de desarrollo. SageMaker proporciona una variedad de imágenes de Amazon Machine (AMI) preconfiguradas que puede usar para lanzar su instancia EC2.

Una vez que haya lanzado su instancia EC2, puede conectarse a ella mediante SSH e instalar SageMaker Python SDK. El SDK proporciona una serie de funciones prácticas que facilitan el trabajo con SageMaker.

## Creación de un modelo de SageMaker

Hay dos formas de crear un modelo de SageMaker:

- Utilice el SDK de Python de SageMaker para definir un modelo mediante una secuencia de comandos de Python.
- Utilice la interfaz web de SageMaker para crear un modelo mediante un algoritmo de aprendizaje automático previamente entrenado.

### Creación de un modelo con SageMaker Python SDK

Para crear un modelo de SageMaker con el SDK de Python, primero debe escribir una secuencia de comandos de Python que defina el modelo. El script debe importar SageMaker Python SDK y definir una subclase de la clase SageMaker.Model.

Su clase modelo debe implementar dos métodos:

- ```train()```, que se llama cuando el modelo está entrenando. Aquí es donde debes implementar tu algoritmo de entrenamiento.
- ```predict()```, que se llama cuando se implementa el modelo y se usa para hacer predicciones. Aquí es donde debe implementar su algoritmo de predicción.

Una vez que haya definido su clase de modelo, puede instanciarla y llamar al método ```fit()``` para entrenar el modelo. El método ```fit()``` toma como entrada un SageMaker.TrainingInstance y un SageMaker.S3DataSource. TrainingInstance se usa para configurar el trabajo de entrenamiento y S3DataSource se usa para especificar la ubicación de los datos de entrenamiento.

Después de completar el trabajo de entrenamiento, puede llamar al método ```deploy()``` para implementar el modelo entrenado. El método ```deploy()``` toma como entrada un SageMaker.PredictorInstance y un SageMaker.S3DataSource. PredictorInstance se usa para configurar el punto final de predicción y S3DataSource se usa para especificar la ubicación de los artefactos del modelo.

### Creación de un modelo con la interfaz web de SageMaker

Para crear un modelo de SageMaker mediante la interfaz web, primero debe iniciar una instancia de cuaderno de SageMaker. Una instancia de notebook es una instancia de Amazon EC2 que viene con SageMaker Python SDK y Jupyter instalados.

Una vez que su instancia de cuaderno esté en funcionamiento, puede abrir el cuaderno de Jupyter y crear un nuevo modelo de SageMaker. Para hacerlo, haga clic en el enlace "Modelos de SageMaker" en la barra de navegación de la izquierda y luego haga clic en el botón "Crear modelo".

En la página "Crear modelo", deberá especificar un nombre para su modelo y seleccionar un algoritmo de aprendizaje automático. SageMaker proporciona una serie de algoritmos de aprendizaje automático preentrenados que puede usar. Para este ejemplo, usaremos el algoritmo XGBoost.

A continuación, deberá especificar la ubicación de los datos de entrenamiento. SageMaker puede usar datos almacenados en Amazon S3, por lo que deberá crear un depósito de Amazon S3 y cargar sus datos de entrenamiento en ese depósito.

Una vez que haya especificado la ubicación de los datos de entrenamiento, puede hacer clic en el botón "Crear modelo" para crear el modelo.

## Entrenamiento de un modelo de SageMaker

Una vez que haya creado un modelo de SageMaker, puede entrenarlo usando el método ```fit()```. El método ```fit()``` toma como entrada un SageMaker.TrainingInstance y un SageMaker.S3DataSource. TrainingInstance se usa para configurar el trabajo de entrenamiento y S3DataSource se usa para especificar la ubicación de los datos de entrenamiento.

 el trabajo de entrenamiento está completo, puede llamar al método ```deploy()``` para implementar el modelo entrenado. El método ```deploy()``` toma como entrada un SageMaker.PredictorInstance y un SageMaker.S3DataSource. PredictorInstance se usa para configurar el punto final de predicción y S3DataSource se usa para especificar la ubicación de los artefactos del modelo.

## Conclusión

En este artículo, hemos visto cómo utilizar AWS SageMaker para crear e implementar modelos de aprendizaje automático en la nube. SageMaker facilita la capacitación y la implementación de modelos de aprendizaje automático al proporcionar un servicio totalmente administrado que se encarga del trabajo pesado por usted.