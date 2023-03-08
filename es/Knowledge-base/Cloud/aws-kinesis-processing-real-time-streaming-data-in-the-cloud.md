---
title: AWS Kinesis: procesamiento de datos de transmisión en tiempo real en la nube
description: 
published: true
date: 2023-02-14T04:55:38.282Z
tags: 
editor: markdown
dateCreated: 2023-02-14T04:55:36.662Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Kinesis: Processing Real-Time Streaming Data in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-kinesis-processing-real-time-streaming-data-in-the-cloud)
{.links-list}

      

# AWS Kinesis: procesamiento de datos de transmisión en tiempo real en la nube

El procesamiento de datos en tiempo real es una tarea compleja y desafiante para cualquier organización. Requiere la ingestión de datos de múltiples fuentes, la transformación de esos datos en información útil y la entrega de esa información a las personas correctas en el momento correcto. Todo esto debe hacerse de forma rápida y precisa, al mismo tiempo que se garantiza que los datos no se pierdan ni se corrompan en el proceso.

AWS Kinesis es una plataforma basada en la nube que facilita el procesamiento de datos de transmisión en tiempo real a escala. Kinesis puede ingerir datos de varias fuentes simultáneamente y procesarlos utilizando varias instancias de Amazon EC2 en paralelo. Esto permite un procesamiento rápido y preciso de grandes cantidades de datos.

Kinesis es un servicio administrado, lo que significa que AWS se encarga de la infraestructura y el escalado por usted. Esto facilita comenzar con Kinesis y elimina la necesidad de aprovisionar y mantener sus propios servidores. Kinesis también es sin servidor, por lo que solo paga por los recursos que utiliza.

## Primeros pasos con AWS Kinesis

Para comenzar con AWS Kinesis, primero debe crear una transmisión. Una secuencia es una entidad lógica que representa un grupo de fragmentos. Un fragmento es una unidad de almacenamiento de datos que se puede utilizar para almacenar y procesar datos.

Puede crear una transmisión mediante la consola de administración de AWS, la interfaz de línea de comandos (CLI) de AWS o el SDK de AWS.

Una vez que haya creado una transmisión, puede comenzar a ingerir datos en ella. Los datos se pueden ingerir de múltiples fuentes, como archivos de registro, eventos de aplicaciones, transmisiones de redes sociales y datos de sensores.

Kinesis Data Streams puede ingerir datos a una velocidad de hasta 1 MB por segundo por fragmento. Si necesita ingerir datos a una velocidad mayor, puede aumentar la cantidad de fragmentos en su transmisión.

Una vez que los datos se han ingerido en una secuencia, se pueden procesar con Kinesis Data Analytics, Kinesis Data Firehose o una aplicación personalizada.

Kinesis Data Analytics es un servicio completamente administrado que facilita el análisis de transmisión de datos en tiempo real. Kinesis Data Analytics se puede utilizar para realizar transformaciones complejas en los datos, como agregaciones, filtrado y uniones.

Kinesis Data Firehose es un servicio completamente administrado que facilita la carga de datos de transmisión en almacenes de datos de AWS, como Amazon S3, Amazon Redshift y Amazon Elasticsearch Service.

También puede procesar datos en un flujo mediante una aplicación personalizada. Una aplicación personalizada se puede escribir en cualquier lenguaje de programación y se puede implementar en Amazon EC2, Amazon ECS o AWS Lambda.

## Procesamiento de datos en un flujo

Kinesis Data Streams utiliza un concepto llamado fragmentos para brindar escalabilidad y rendimiento. Un fragmento es una unidad de almacenamiento de datos que se puede utilizar para almacenar y procesar datos.

Kinesis Data Streams está diseñado para escalar horizontalmente, lo que significa que puede aumentar la cantidad de fragmentos en una secuencia para aumentar su rendimiento.

Los datos en un flujo se procesan en paralelo por varias instancias de Amazon EC2. Cada instancia procesa datos de uno o más fragmentos en la secuencia.

Kinesis Data Streams usa una clave de partición para distribuir los datos de manera uniforme en todos los fragmentos de una secuencia. La clave de partición es un atributo del registro de datos que se utiliza para determinar a qué fragmento se asignará el registro de datos.

Cuando se transfieren datos a una transmisión, Kinesis Data Streams usa la clave de partición para determinar en qué fragmento se ingresan los datos. Kinesis Data Streams también utilizará la clave de partición para determinar qué instancia procesará el registro de datos.

Los registros de datos en un flujo se procesan en el orden en que se reciben. Sin embargo, dado que los datos se distribuyen en varios fragmentos, no se garantiza el orden en que se procesan los registros de datos.

Si necesita procesar registros de datos en un orden específico, puede usar el atributo de número de secuencia de un registro de datos. Kinesis Data Streams asigna el número de secuencia cuando un registro de datos se ingiere en una transmisión.

Los registros de datos con la misma clave de partición se procesarán en orden según su número de secuencia. Sin embargo, los registros de datos con diferentes claves de partición pueden procesarse fuera de servicio.

## Conclusión

AWS Kinesis es una plataforma poderosa para procesar datos de transmisión en tiempo real a escala. Kinesis puede ingerir datos de varias fuentes simultáneamente y procesarlos utilizando varias instancias de Amazon EC2 en paralelo. Esto permite un procesamiento rápido y preciso de grandes cantidades de datos.

Kinesis es un servicio administrado, lo que significa que AWS se encarga de la infraestructura y el escalado por usted. Esto facilita comenzar con Kinesis y elimina la necesidad de aprovisionar y mantener sus propios servidores. Kinesis también es sin servidor, por lo que solo paga por los recursos que utiliza.

## Otras lecturas

- [Guía para desarrolladores de AWS Kinesis Data Streams](https://docs.aws.amazon.com/kinesis/latest/datastreams/developer-guide.html)
- [Guía para desarrolladores de AWS Kinesis Data Analytics](https://docs.aws.amazon.com/kinesisanalytics/latest/java/getting-started.html)
- [Guía para desarrolladores de AWS Kinesis Data Firehose](https://docs.aws.amazon.com/firehose/latest/dev/what-is-this-service.html)