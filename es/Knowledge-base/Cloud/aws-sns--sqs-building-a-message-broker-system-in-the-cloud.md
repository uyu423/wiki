---
title: AWS SNS y SQS: creación de un sistema de intermediario de mensajes en la nube
description: 
published: true
date: 2023-02-02T03:23:55.492Z
tags: 
editor: markdown
dateCreated: 2023-02-02T03:23:53.880Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS SNS & SQS: Building a Message Broker System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns--sqs-building-a-message-broker-system-in-the-cloud)
{.links-list}


# AWS SNS y SQS: creación de un sistema de intermediario de mensajes en la nube

En este artículo, veremos cómo usar AWS SNS y SQS para crear un sistema de intermediario de mensajes en la nube. Exploraremos los beneficios de usar un intermediario de mensajes y cómo puede ayudar con el procesamiento y enrutamiento de mensajes entre diferentes servicios. También veremos algunos ejemplos de código para mostrar cómo configurar y usar SNS y SQS en sus propias aplicaciones.

## ¿Qué es un intermediario de mensajes?

Un intermediario de mensajes es un sistema que ayuda a procesar y enrutar mensajes entre diferentes aplicaciones de software. Puede proporcionar una serie de beneficios, tales como:

- rendimiento mejorado al desacoplar el envío de mensajes y el procesamiento de mensajes
- mayor flexibilidad en la forma en que se enrutan los mensajes
- la capacidad de manejar una gran cantidad de mensajes
- gestión más sencilla de las colas de mensajes

Los intermediarios de mensajes a menudo se usan en aplicaciones que necesitan procesar una gran cantidad de mensajes o donde los mensajes deben enrutarse entre diferentes servicios. Por ejemplo, se podría usar un intermediario de mensajes para procesar pedidos de un sitio web y enrutarlos al servicio de cumplimiento correcto.

## ¿Qué son SNS y SQS?

SNS y SQS son dos servicios de Amazon Web Services (AWS) que se pueden utilizar para crear un sistema de intermediación de mensajes.

SNS es un servicio de mensajería pub/sub que se puede utilizar para enviar mensajes a varios suscriptores diferentes. Se puede usar para enviar mensajes a varios suscriptores o para enviar mensajes a un suscriptor específico.

SQS es un servicio de cola de mensajes que se puede usar para almacenar mensajes hasta que se puedan procesar. Se puede usar para desacoplar el envío y el procesamiento de mensajes, o para procesar mensajes en lotes.

## Configuración de SNS y SQS

Para utilizar SNS y SQS, deberá configurar una cuenta de AWS y crear un nuevo tema de SNS y una cola de SQS.

Crear un tema de SNS es un proceso de dos pasos. Primero, debe crear el tema y luego debe suscribirse al tema. Para crear un nuevo tema de SNS, puede usar la Consola de administración de AWS o puede usar la CLI de AWS.

Para crear un nuevo tema de SNS mediante la Consola de administración de AWS, inicie sesión en la consola y navegue hasta el servicio de SNS. Haga clic en el botón "Crear tema" e ingrese un nombre y una descripción para su tema. Una vez creado el tema, puede suscribirse haciendo clic en el botón "Suscribirse al tema" e ingresando los detalles de la suscripción.

Para crear un nuevo tema de SNS mediante la AWS CLI, puede utilizar el siguiente comando:

```
aws sns create-topic --name my-topic
```

Para suscribirse al tema, puede usar el siguiente comando:

```
aws sns subscribe --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --protocol email --notification-endpoint myemail@example.com
```

La creación de una cola de SQS es un proceso de tres pasos. Primero, debe crear la cola, luego debe configurar los permisos y, finalmente, debe suscribirse a la cola. Para crear una nueva cola de SQS, puede usar la Consola de administración de AWS o puede usar la CLI de AWS.

Para crear una nueva cola de SQS mediante la consola de administración de AWS, inicie sesión en la consola y navegue hasta el servicio de SQS. Haga clic en el botón "Crear cola" e ingrese un nombre y una descripción para su cola. Una vez que se ha creado la cola, puede configurar los permisos haciendo clic en la pestaña "Permisos" y agregando un nuevo permiso. Finalmente, puede suscribirse a la cola haciendo clic en el botón "Suscribirse al tema" e ingresando los detalles de la suscripción.

Para crear una nueva cola de SQS mediante la CLI de AWS, puede utilizar el siguiente comando:

```
aws sqs create-queue --queue-name my-queue
```

Para establecer los permisos, puede usar el siguiente comando:

```
aws sqs set-queue-attributes --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --attributes '{"Policy":"{\"Version\":\"2012-10-17\",\"Id\":\"MyQueuePolicy\",\"Statement\":[{\"Sid\":\"MyQueueSid\",\"Effect\":\"Allow\",\"Principal\":{\"AWS\":\"*\"},\"Action\":\"sqs:SendMessage\",\"Resource\":\"arn:aws:sqs:us-east-1:123456789012:my-queue\",\"Condition\":{\"ArnLike\":{\"aws:SourceArn\":\"arn:aws:sns:us-east-1:123456789012:my-topic\"}}}]}"}'
```

Para suscribirse a la cola, puede usar el siguiente comando:

```
aws sqs subscribe-queue --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic
```

## Enviando mensajes

Ahora que ha configurado su tema de SNS y la cola de SQS, puede comenzar a enviar mensajes. Para enviar un mensaje, puede usar la Consola de administración de AWS o puede usar la CLI de AWS.

Para enviar un mensaje mediante la Consola de administración de AWS, inicie sesión en la consola y navegue hasta el servicio SNS. Haga clic en el botón "Crear mensaje" e ingrese los detalles del mensaje. También puede especificar el número de mensajes a enviar y el tiempo de vida del mensaje. Una vez que se ha creado el mensaje, puede hacer clic en el botón "Publicar mensaje" para enviar el mensaje.

Para enviar un mensaje mediante la AWS CLI, puede utilizar el siguiente comando:

```
aws sns publish --topic-arn arn:aws:sns:us-east-1:123456789012:my-topic --message "Hello, world!"
```

## Recibir mensajes

Una vez que haya enviado un mensaje, se almacenará en la cola de SQS. Para recibir el mensaje, puede usar la Consola de administración de AWS o puede usar la CLI de AWS.

Para recibir un mensaje mediante la Consola de administración de AWS, inicie sesión en la consola y navegue hasta el servicio SQS. Haga clic en el botón "Obtener mensajes" y seleccione la cantidad de mensajes que desea recuperar. También puede especificar el tiempo de vida del mensaje y el tiempo de espera de visibilidad. Una vez que se haya recuperado el mensaje, puede hacer clic en el botón "Eliminar mensaje" para eliminarlo de la cola.

Para recibir un mensaje mediante la AWS CLI, puede utilizar el siguiente comando:

```
aws sqs receive-message --queue-url https://sqs.us-east-1.amazonaws.com/123456789012/my-queue
```

## Conclusión

En este artículo, analizamos cómo usar AWS SNS y SQS para crear un sistema de intermediario de mensajes en la nube. Hemos visto cómo un intermediario de mensajes puede proporcionar una serie de beneficios y cómo se pueden usar SNS y SQS para enviar y recibir mensajes. También hemos visto algunos ejemplos de código para mostrar cómo configurar y usar SNS y SQS en sus propias aplicaciones.