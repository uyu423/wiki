---
title: AWS CloudWatch: Monitoreo y depuración de aplicaciones en la nube
description: 
published: true
date: 2023-02-09T16:55:41.912Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:55:35.631Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS CloudWatch: Monitoring and Debugging Cloud Applications***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudwatch-monitoring-and-debugging-cloud-applications)
{.links-list}


# AWS CloudWatch: Monitoreo y depuración de aplicaciones en la nube

## Introducción

CloudWatch es un servicio de monitoreo para los recursos de la nube de AWS y las aplicaciones que se ejecutan en AWS. CloudWatch proporciona datos e información útil para monitorear aplicaciones, comprender y responder a cambios de rendimiento en todo el sistema, optimizar la utilización de recursos y obtener una vista unificada del estado operativo. CloudWatch se puede utilizar para recopilar y realizar un seguimiento de las métricas, establecer alarmas y reaccionar automáticamente a los cambios en sus recursos de AWS.

En este artículo, veremos cómo funciona CloudWatch y cómo se puede usar para monitorear y depurar aplicaciones en la nube.

## Cómo funciona CloudWatch

CloudWatch recopila datos de recursos de AWS, como instancias de Amazon EC2, tablas de Amazon DynamoDB e instancias de base de datos de Amazon RDS. Estos datos luego se usan para generar métricas que se pueden usar para monitorear el rendimiento de sus recursos y aplicaciones.

CloudWatch también se puede utilizar para recopilar datos de registro de sus recursos y aplicaciones. Estos datos se pueden utilizar para solucionar problemas e identificar tendencias.

## Monitoreo con CloudWatch

CloudWatch se puede utilizar para monitorear sus recursos y aplicaciones de dos maneras:

- **Métricas**: las métricas de CloudWatch son puntos de datos estadísticos que se pueden usar para monitorear el rendimiento de sus recursos y aplicaciones. Las métricas se generan a partir de los datos recopilados por CloudWatch.

- **Registros**: los registros de CloudWatch son registros de la actividad de sus recursos y aplicaciones. Los registros se pueden utilizar para solucionar problemas e identificar tendencias.

## Configuración de CloudWatch

Para usar CloudWatch, primero debe crear un grupo de Amazon CloudWatch Logs y una transmisión de Amazon CloudWatch Logs.

A continuación, debe instalar el agente de CloudWatch Logs en sus instancias EC2. El agente de CloudWatch Logs es un programa de software que se ejecuta en sus instancias EC2 y envía datos de registro a CloudWatch.

Una vez que el agente de CloudWatch Logs está instalado y ejecutándose en sus instancias EC2, puede comenzar a enviar datos de registro a CloudWatch.

## Recopilación de métricas con CloudWatch

Los datos de métricas de CloudWatch se recopilan en intervalos de cinco minutos y se almacenan durante dos semanas.

Para recopilar métricas con CloudWatch, primero debe crear un filtro de métricas. Un filtro de métrica coincide con un patrón en sus datos de registro y extrae los datos de métrica de la entrada de registro.

A continuación, debe crear una alarma métrica. Una alarma de métrica observa una métrica y activa una acción cuando la métrica supera un umbral.

## Recopilación de registros con CloudWatch

Los datos de registro de CloudWatch se recopilan en intervalos de un minuto y se almacenan durante 14 días.

Para recopilar registros con CloudWatch, primero debe crear un grupo de registros. Un grupo de registros es una colección de registros con el mismo período de retención.

A continuación, debe crear un flujo de registro. Un flujo de registro es una secuencia de eventos de registro de una sola fuente.

Una vez que haya creado un grupo de registro y un flujo de registro, puede comenzar a enviar datos de registro a CloudWatch.

## Envío de notificaciones con CloudWatch

CloudWatch se puede utilizar para enviar notificaciones cuando se activa una alarma de métrica. Las notificaciones se pueden enviar a través de Amazon SNS, Amazon SQS o correo electrónico.

Para enviar notificaciones con CloudWatch, primero debe crear un tema de Amazon SNS. Un tema de Amazon SNS es un punto de acceso lógico para permitir que los destinatarios se suscriban a sus mensajes de Amazon SNS.

A continuación, debe crear una cola de Amazon SQS. Una cola de Amazon SQS es un búfer que almacena mensajes hasta que los procesa un consumidor.

Una vez que haya creado un tema de Amazon SNS y una cola de Amazon SQS, puede configurar su alarma de métrica para enviarles notificaciones.

## Conclusión

En este artículo, hemos analizado cómo funciona CloudWatch y cómo se puede usar para monitorear y depurar aplicaciones en la nube. También hemos visto cómo configurar CloudWatch y cómo recopilar métricas y registros con CloudWatch. Finalmente, hemos visto cómo enviar notificaciones con CloudWatch.