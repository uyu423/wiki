---
title: Supervisión de aplicaciones back-end con CloudWatch
description: 
published: true
date: 2023-02-10T01:55:35.425Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:55:33.777Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Monitoring Backend Applications with CloudWatch***English** document is available*](/en/Knowledge-base/Backend/monitoring-backend-applications-with-cloudwatch)
{.links-list}


# Monitoreo de aplicaciones back-end con CloudWatch

CloudWatch es un servicio de monitoreo para los recursos de la nube de AWS y las aplicaciones que se ejecutan en AWS. CloudWatch recopila datos operativos y de supervisión en forma de registros, métricas y eventos, que se pueden utilizar para solucionar problemas y optimizar sus aplicaciones.

En este artículo, nos centraremos en cómo usar CloudWatch para monitorear aplicaciones de back-end. Cubriremos los siguientes temas:

- ¿Qué es CloudWatch?
- Configuración de CloudWatch
- Creación de una alarma de CloudWatch
- Visualización de registros de CloudWatch

## ¿Qué es CloudWatch?

Como se mencionó anteriormente, CloudWatch es un servicio de monitoreo para los recursos de la nube de AWS y las aplicaciones que se ejecutan en AWS. Con CloudWatch, puede recopilar y realizar un seguimiento de las métricas, establecer alarmas y reaccionar automáticamente a los cambios en sus recursos de AWS.

CloudWatch le proporciona datos e información procesable para monitorear sus aplicaciones, responder a cambios de rendimiento en todo el sistema, optimizar la utilización de recursos y obtener una vista unificada del estado operativo.

## Configuración de CloudWatch

Para utilizar CloudWatch, primero debe configurar una cuenta de AWS y crear un grupo de Amazon CloudWatch Logs.

1. Para configurar una cuenta de AWS, vaya a [https://aws.amazon.com/](https://aws.amazon.com/) y haga clic en **Crear una cuenta de AWS**.

2. Siga las instrucciones para crear su cuenta.

3. Una vez que haya creado su cuenta, vaya a la consola de Amazon CloudWatch en [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

4. En el panel de navegación izquierdo, haga clic en **Registros**.

5. Haga clic en **Crear grupo de registros**.

6. Introduzca un nombre para su grupo de registro y haga clic en **Crear grupo de registro**.

## Creación de una alarma de CloudWatch

Una alarma observa una métrica durante un período de tiempo que especifique y realiza una o más acciones en función del valor de la métrica en relación con un umbral que establezca. Las acciones pueden ser cualquier cosa, desde enviar una notificación de Amazon SNS hasta llamar a una función de AWS Lambda.

En esta sección, crearemos una alarma que envíe una notificación de Amazon SNS cuando el uso promedio de la CPU de una instancia de Amazon EC2 supere el 50 %.

1. Vaya a la consola de Amazon CloudWatch en [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

2. En el panel de navegación izquierdo, haga clic en **Alarmas**.

3. Haga clic en **Crear alarma**.

4. Seleccione la métrica **CPUUtilization** y haga clic en **Siguiente**.

5. Configure la alarma de la siguiente manera:

- Para **Estadística**, seleccione **Promedio**.
- Para **Período**, ingrese **60**.
- Para **Unidad**, seleccione **Segundos**.
- Para **Umbral**, ingrese **50**.
- Para **Período de evaluación**, ingrese **2**.
- Para **Tratar datos faltantes**, seleccione **Datos faltantes como incumplimiento**.
- Para **Acciones**, seleccione la acción **Enviar una notificación**.
- Para **Enviar una notificación a**, seleccione el tema de Amazon SNS en el que desea recibir la notificación.

6. Haga clic en **Crear alarma**.

## Ver registros de CloudWatch

CloudWatch Logs le permite monitorear, almacenar y acceder a sus archivos de registro desde instancias de Amazon EC2, Amazon CloudTrail u otras fuentes.

En esta sección, le mostraremos cómo ver los registros de CloudWatch para una instancia de Amazon EC2.

1. Vaya a la consola de Amazon CloudWatch en [https://console.aws.amazon.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/).

2. En el panel de navegación izquierdo, haga clic en **Registros**.

3. Seleccione el grupo de registros cuyos registros desea ver.

4. Seleccione el flujo de registro que desea ver.

5. El flujo de registro se mostrará en el panel derecho.

## Referencias

- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/WhatIsCloudWatch.html)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/WhatIsCloudWatchLogs.html)
- [https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/](https://aws.amazon.com/blogs/aws/new-cloudwatch-logs-agent/)
- [https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/AlarmThatSendsEmail.html)