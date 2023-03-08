---
title: AWS CloudTrail: registro de llamadas a la API de AWS para cumplimiento y auditoría
description: 
published: true
date: 2023-02-05T07:56:03.174Z
tags: 
editor: markdown
dateCreated: 2023-02-05T07:56:01.432Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS CloudTrail: Logging AWS API Calls for Compliance and Auditing***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}


AWS CloudTrail es un servicio web que registra sus llamadas a la API de AWS y le entrega archivos de registro. CloudTrail proporciona un historial de eventos de la actividad de su cuenta de AWS, incluidas las acciones realizadas a través de la Consola de administración de AWS, los SDK de AWS, las herramientas de línea de comandos y otros servicios de AWS. Este historial de eventos simplifica el análisis de seguridad, el seguimiento de cambios de recursos y la auditoría de cumplimiento.

CloudTrail es fácil de configurar. Puede crear registros que registren datos en un depósito de Amazon S3, un grupo de registros de Amazon CloudWatch Logs, ambos o ninguno. Puede configurar varios registros para entregar datos al mismo depósito de Amazon S3 o al mismo grupo de registros de Amazon CloudWatch Logs. Cuando configura AWS CloudTrail, especifica los depósitos de Amazon S3 o los grupos de registro de Amazon CloudWatch Logs donde desea que CloudTrail entregue sus archivos de registro.

 Trails puede registrar datos para todas las regiones de AWS en su cuenta de AWS, o solo para regiones seleccionadas. Puede habilitar el registro para todas las regiones en su cuenta de AWS, o solo para las regiones seleccionadas. Cuando habilita una región para el registro de CloudTrail, CloudTrail crea un nuevo rastro en esa región.

## Configuración de CloudTrail

Para activar el registro de su cuenta de AWS, cree un registro. Un rastro habilita CloudTrail y especifica el método de entrega de sus archivos de registro de CloudTrail. Puede crear un registro que registre eventos de datos para todas las regiones en su cuenta de AWS, o solo para las regiones seleccionadas. También puede configurar si el seguimiento se aplica solo a los recursos de su cuenta de AWS o a todos los recursos de AWS. Cuando haya creado un rastro, puede ver y buscar los archivos de registro en la consola de AWS CloudTrail casi en tiempo real.

### Creación de un sendero

Utilice el siguiente procedimiento para crear un registro y especificar el depósito de Amazon S3 o el grupo de registro de Amazon CloudWatch Logs donde desea que CloudTrail entregue sus archivos de registro.

1. Abra la consola de AWS CloudTrail en https://console.aws.amazon.com/cloudtrail/.

2. Si es la primera vez que utiliza la consola de AWS CloudTrail, lea el mensaje y elija **Comenzar**.

3. Elija **Crear ruta**.

4. Para **Nombre**, ingrese un nombre para la ruta. El nombre debe ser único en la región en la que está creando la ruta. Por ejemplo, puede llamar a su sendero MyTrail.

5. Para **Aplicar ruta a todas las regiones**, realice una de las siguientes acciones:

* Para aplicar la ruta a todas las regiones, elija **Sí, aplicar la ruta a todas las regiones**.
* Para aplicar la ruta solo a las regiones seleccionadas, elija **No, aplicar la ruta solo a las regiones seleccionadas** y luego seleccione las regiones.

6. Para **S3 bucket name**, ingrese el nombre del depósito de Amazon S3 donde desea que CloudTrail entregue sus archivos de registro. El cubo debe existir en la misma región donde está creando el rastro. Si ingresa el nombre de un depósito existente, CloudTrail escribe los archivos de registro en el depósito. Si el depósito no existe, CloudTrail crea el depósito.

7. Para **Prefijo de clave S3**, ingrese un prefijo opcional para los nombres de los archivos de registro. Si no especifica un prefijo, los archivos de registro se entregan sin prefijo.

8. Para **Nombre del grupo de registros de CloudWatch Logs**, ingrese el nombre del grupo de registros de Amazon CloudWatch Logs donde desea que CloudTrail entregue sus archivos de registro. El grupo de registros debe existir en la misma región en la que está creando el registro.

9. Para **Habilitar la validación del archivo de registro**, realice una de las siguientes acciones:

* Para crear firmas digitales para todos los archivos de registro, seleccione **Sí**. CloudTrail crea firmas digitales para todos los archivos de registro.
* Para excluirse de las firmas digitales para todos los archivos de registro, seleccione **No**.

10. Elija **Crear**.

Después de crear un registro de seguimiento, debe configurar Amazon S3 para publicar eventos en el registro de seguimiento.

### Configuración de Amazon S3

Cuando crea un registro, especifica el depósito de Amazon S3 donde desea que CloudTrail entregue sus archivos de registro. CloudTrail utiliza Amazon S3 para enviar archivos de registro de cada región en su cuenta de AWS. Debe configurar Amazon S3 para publicar eventos en la ruta.

1. Abra la consola de Amazon S3 en https://console.aws.amazon.com/s3/.

2. En la consola de Amazon S3, elija el nombre del depósito que especificó cuando creó el rastro.

3. Elija **Propiedades**.

4. En el panel Propiedades, elija **Eventos**.

5. Elija **Agregar notificación**.

6. En el campo **Nombre**, ingrese un nombre para el evento.

7. Para **Eventos**, elija **Todos los eventos de creación de objetos**.

8. Para **Enviar a**, elija **Tema SNS**.

9. Para **ARN de tema de SNS**, ingrese el ARN para el tema de Amazon SNS que especificó cuando creó la ruta.

10. Elija **Guardar**.

Después de configurar Amazon S3 para publicar eventos en el seguimiento, CloudTrail comienza a registrar llamadas a la API de AWS para los recursos en el depósito que especificó. CloudTrail puede tardar hasta 15 minutos en enviar los archivos de registro al depósito.

## Visualización de archivos de registro

Después de crear un registro y configurar Amazon S3 para publicar eventos, puede ver y buscar los archivos de registro en la consola de AWS CloudTrail casi en tiempo real.

1. Abra la consola de AWS CloudTrail en https://console.aws.amazon.com/cloudtrail/.

2. Elige **Senderos**.

3. Elige el nombre de la ruta.

4. En la página **Configurar seguimiento**, seleccione **Ver archivos de registro**.

5. En la lista **Archivos de registro**, elija el nombre de un archivo de registro.

6. Elija **Descargar**.

7. En el cuadro de diálogo **Descargar archivo de registro**, seleccione **Guardar archivo**.

## Formato de archivo de registro de CloudTrail

Los archivos de registro de CloudTrail contienen una o más entradas de registro. Una entrada de registro representa una sola solicitud de cualquier fuente e incluye información sobre la acción solicitada, la fecha y hora de la acción, los parámetros de la solicitud, etc.

CloudTrail escribe entradas de registro en archivos de registro mediante un formato delimitado por espacios. Cada entrada de registro consta de nueve campos separados por espacios. Los campos le permiten reconstruir y comprender la secuencia de eventos que ocurrieron, incluido qué usuario o función inició el evento, cuándo ocurrió el evento, qué recursos se vieron afectados, etc.

La siguiente tabla describe los campos en una entrada de registro de CloudTrail.

| Campo | Descripción |
| --- | --- |
| **ID de evento** | Un identificador único para el evento. Por ejemplo, **eventID=55746930-A87B-4E50-95A7-12B80B6E8700**. |
| **nombre del evento** | El nombre del evento. Por ejemplo, **eventName=RunInstances**. |
| **origen del evento** | El servicio de AWS que generó el evento. Por ejemplo, **origen del evento=ec2.amazonaws.com** o **origen del evento=iam.amazonaws.com**. |
| **región de aws** | La región de AWS donde ocurrió el evento. Por ejemplo, **awsRegion=us-east-1**. |
| **dirección IP de origen** | La dirección IP del solicitante. |
| **agente de usuario** | La información del agente de usuario incluida en la solicitud, si corresponde. |
| **parámetros de solicitud** | Cualquier parámetro de solicitud incluido en el evento, si lo hay. Los parámetros de solicitud generalmente se incluyen para las acciones realizadas a través de la Consola de administración de AWS o la API de AWS. El formato de los parámetros de solicitud depende del **eventName**. |
| **Elementos de respuesta** | Los elementos de respuesta devueltos por el servicio de AWS, si los hay. Los elementos de respuesta generalmente se incluyen para las acciones realizadas a través de la Consola de administración de AWS. El formato de los elementos de respuesta depende del **eventName**. |
| **datos adicionales del evento** | Información adicional sobre el evento. |
| **ID de solicitud** | Un valor que identifica la solicitud. |
| **Tipo de evento** | El tipo de evento. Los valores válidos son **AwsApiCall**, **AwsServiceEvent** y **AwsSdkCall**. |
| **recipientAccountId** | El ID de la cuenta de AWS que recibe eventos de otra cuenta de AWS. Por ejemplo, los eventos de una cuenta de miembro en una organización se entregan a la cuenta maestra. Este campo solo se completa para eventos entre cuentas. |
| **Id. de evento compartido** | El **eventID** del evento en la cuenta maestra. Este campo solo se completa para eventos entre cuentas. |

## Ejemplo de archivo de registro de CloudTrail

El siguiente es un ejemplo de un archivo de registro de CloudTrail.

```
55746930-A87B-4E50-95A7-12B80B6E8700 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Mozilla/5.0 aws-cli/1.7.28 Python/2.7.9 Windows/2012server botocore/1.3.22
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 Usuario