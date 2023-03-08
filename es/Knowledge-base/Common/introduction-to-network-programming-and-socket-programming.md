---
title: Introducción a la programación de redes y la programación de sockets
description: 
published: true
date: 2023-02-12T14:55:30.404Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:55:28.738Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Introduction to Network Programming and Socket Programming***English** document is available*](/en/Knowledge-base/Common/introduction-to-network-programming-and-socket-programming)
{.links-list}


# Introducción a la programación de redes y la programación de sockets

Las computadoras se comunican entre sí utilizando una variedad de protocolos, los más comunes son el Protocolo de control de transmisión (TCP) y el Protocolo de datagramas de usuario (UDP).

#### Protocolo de control de transmisión (TCP)

TCP es un protocolo orientado a la conexión, lo que significa que dos computadoras deben establecer una conexión antes de poder comunicarse. Una vez que se establece una conexión, los datos se pueden transferir en ambas direcciones. TCP es un protocolo confiable, lo que significa que los datos se entregan en el orden en que se enviaron y que los datos perdidos o dañados se retransmiten.

#### Protocolo de datagramas de usuario (UDP)

UDP es un protocolo sin conexión, lo que significa que dos computadoras pueden comunicarse sin establecer primero una conexión. No se garantiza que los datos se entreguen en el orden en que se enviaron, y los datos perdidos o dañados no se retransmiten.

#### Enchufe

Un socket es un punto final para la comunicación entre dos computadoras. Un socket se puede asociar con un número de puerto específico, que se utiliza para identificar el socket.

#### Programación de enchufes

La programación de sockets es una forma de escribir software que puede aprovechar las características de los protocolos TCP y UDP. La programación de socket se puede utilizar para crear una variedad de aplicaciones, incluidos servidores web, aplicaciones de transferencia de archivos y aplicaciones de chat.

##### Creación de un zócalo

Para crear un socket, primero debe crear una estructura de dirección de socket. Esta estructura contiene la información necesaria para identificar un socket, incluida la familia de direcciones, el número de puerto y la dirección IP.

Una vez que haya creado la estructura de direcciones del socket, puede llamar a la función socket() para crear el socket. La función socket() toma la familia de direcciones, el tipo de socket y el protocolo como argumentos.

##### Conexión a un enchufe

Una vez que haya creado un socket, puede conectarse a un socket remoto llamando a la función connect(). La función connect() toma el socket y la estructura de dirección del socket como argumentos.

##### Vinculación de un socket

Para recibir datos de un socket remoto, primero debe vincular el socket a un puerto local. Esto se hace llamando a la función bind(). La función bind() toma el socket y la estructura de dirección del socket como argumentos.

##### Escuchando conexiones entrantes

Una vez que haya vinculado el socket a un puerto local, puede escuchar las conexiones entrantes llamando a la función listen(). La función listen() toma el socket y el backlog como argumentos. El backlog es el número máximo de conexiones pendientes que se pueden poner en cola en un momento dado.

##### Aceptar conexiones entrantes

Una vez que haya llamado a la función listen(), puede aceptar conexiones entrantes llamando a la función accept(). La función accept() toma como argumentos el socket y la dirección del cliente que se está conectando.

##### Envío y recepción de datos

Una vez que haya establecido una conexión, puede enviar y recibir datos usando las funciones send() y recv(). La función enviar () toma el socket, un puntero a los datos que se enviarán, la longitud de los datos y las banderas como argumentos. La función recv() toma el socket, un puntero al búfer para almacenar los datos, la longitud del búfer y las banderas como argumentos.

##### Cerrar una conexión

Una vez que haya terminado de enviar y recibir datos, puede cerrar la conexión llamando a la función close(). La función close() toma el socket como argumento.