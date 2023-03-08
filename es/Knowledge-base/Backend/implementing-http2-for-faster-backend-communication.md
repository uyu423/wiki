---
title: Implementación de HTTP/2 para una comunicación back-end más rápida
description: 
published: true
date: 2023-02-15T02:17:18.075Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:17:16.213Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing HTTP/2 for Faster Backend Communication***English** document is available*](/en/Knowledge-base/Backend/implementing-http2-for-faster-backend-communication)
{.links-list}


HTTP/2 es una revisión importante del protocolo de red HTTP utilizado por la World Wide Web. Se derivó del protocolo SPDY experimental anterior, desarrollado originalmente por Google. HTTP/2 se publicó como RFC 7540 en mayo de 2015.

HTTP/2 no es compatible con versiones anteriores de HTTP/1.x y requiere HTTPS.

Los objetivos principales de HTTP/2 son reducir la latencia al permitir la multiplexación completa de solicitudes y respuestas, minimizar la sobrecarga del protocolo a través de encabezados compactos y agregar compatibilidad con la priorización de solicitudes y la inserción del servidor.

HTTP/2 es binario, en lugar de textual. Multiplexa varias solicitudes y respuestas a través de una sola conexión, en lugar de que cada solicitud espere a que finalice la anterior. Esto permite una comunicación más rápida y eficiente entre el cliente y el servidor.

HTTP/2 también utiliza la compresión de encabezados para reducir el tamaño de los encabezados, que pueden ser hasta un 80 % más pequeños que en HTTP/1.x. Esto da como resultado que se envíen menos datos a través de la red y, por lo tanto, reduce la latencia.

HTTP/2 también introduce soporte para la priorización de solicitudes, lo que permite al cliente especificar el orden en que el servidor debe procesar las solicitudes. Esto se puede usar para mejorar el rendimiento de la carga de la página, por ejemplo, cargando primero los recursos críticos.

Finalmente, HTTP/2 introduce soporte para servidor push, lo que permite que el servidor envíe proactivamente recursos al cliente que anticipa que el cliente necesitará, incluso antes de que el cliente los haya solicitado. Esto se puede utilizar para mejorar el rendimiento de la carga de la página, al eliminar la necesidad de que el cliente realice múltiples viajes de ida y vuelta al servidor para obtener todos los recursos necesarios.

 Implementando HTTP/2

Para aprovechar HTTP/2, debe asegurarse de que tanto su servidor como su cliente admitan HTTP/2.

En el lado del servidor, deberá usar un servidor web que admita HTTP/2. Por ejemplo, Apache HTTP Server es compatible con HTTP/2 desde la versión 2.4.17, lanzada en diciembre de 2015.

En el lado del cliente, deberá usar un navegador web que admita HTTP/2. Por ejemplo, todos los principales navegadores web actualmente admiten HTTP/2, incluidos Google Chrome, Mozilla Firefox, Microsoft Edge y Apple Safari.

Una vez que se haya asegurado de que tanto su servidor como su cliente admitan HTTP/2, puede comenzar a usar HTTP/2 simplemente usando el protocolo https:// en lugar de http:// al acceder a su sitio web. Su servidor negociará automáticamente HTTP/2 con el cliente y toda la comunicación se realizará a través de HTTP/2.

Si desea usar HTTP/2 sin HTTPS, puede hacerlo configurando su servidor para usar HTTP/2 a través de una conexión TCP de texto sin cifrar. Sin embargo, esto generalmente no se recomienda, ya que niega muchos de los beneficios de HTTP/2 y no es compatible con todos los clientes.

Conclusión

HTTP/2 es una revisión importante del protocolo de red HTTP que ofrece importantes mejoras de rendimiento con respecto a HTTP/1.x. Para aprovechar HTTP/2, debe asegurarse de que tanto su servidor como su cliente admitan HTTP/2. Una vez que lo haya hecho, puede comenzar a usar HTTP/2 simplemente usando el protocolo https:// en lugar de http:// al acceder a su sitio web.