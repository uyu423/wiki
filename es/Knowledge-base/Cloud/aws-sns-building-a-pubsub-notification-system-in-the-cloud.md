---
title: AWS SNS: creación de un sistema de notificación de Pub/Sub en la nube
description: 
published: true
date: 2023-02-11T08:55:13.912Z
tags: 
editor: markdown
dateCreated: 2023-02-11T08:55:12.292Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS SNS: Building a Pub/Sub Notification System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sns-building-a-pubsub-notification-system-in-the-cloud)
{.links-list}


# AWS SNS: Creación de un sistema de notificación Pub/Sub en la nube

En este artículo, veremos cómo configurar un sistema simple de notificación de publicación/suscripción mediante AWS SNS (Servicio de notificación simple). Cubriremos todo, desde configurar un tema de SNS hasta crear una suscripción y enviar una notificación.

## Configuración de un tema SNS

El primer paso es crear un tema SNS. Esto se puede hacer a través de la Consola de administración de AWS, la CLI de AWS o el SDK.

Crear un tema es un proceso simple:

1. Vaya a la consola SNS y haga clic en **Crear tema**.
2. Ingrese un **Nombre de tema** y un **Nombre para mostrar**.
3. Haga clic en **Crear tema**.

Ahora debería ver su nuevo tema en la lista de temas.

## Crear una suscripción

Ahora que tenemos un tema, necesitamos crear una suscripción. Esto nos permitirá especificar el punto final al que se enviarán nuestras notificaciones.

1. Vaya a la pestaña **Suscripciones** y haga clic en **Crear suscripción**.
2. Seleccione el tema que creó en el menú desplegable **ARN del tema**.
3. En el menú desplegable **Protocolo**, seleccione el protocolo que desea usar para la entrega. AWS SNS admite una variedad de protocolos, incluidos HTTP, HTTPS, correo electrónico y más.
4. Ingrese el **Punto final** para su suscripción. Esta será la URL o la dirección de correo electrónico a la que se enviarán las notificaciones.
5. Haga clic en **Crear suscripción**.

Ahora debería ver su nueva suscripción en la lista de suscripciones.

## Envío de una notificación

Ahora que tenemos un tema y una suscripción configurados, estamos listos para enviar nuestra primera notificación.

1. Vaya a la pestaña **Temas** y seleccione el tema al que desea enviar una notificación.
2. Haga clic en **Publicar en tema**.
3. Ingrese un **Asunto** y un **Mensaje** para su notificación.
4. Haga clic en **Publicar mensaje**.

Su notificación ahora se enviará al punto final especificado en su suscripción.

## Conclusión

En este artículo, vimos cómo configurar un sistema simple de notificación de publicación/suscripción mediante AWS SNS. Hemos cubierto todo, desde la creación de un tema hasta la creación de una suscripción y el envío de una notificación. Con AWS SNS, es fácil configurar un sistema de notificación que se puede usar para enviar notificaciones a una variedad de puntos finales.