---
title: La pila de red de Linux
description: 
published: true
date: 2023-02-11T09:32:18.974Z
tags: 
editor: markdown
dateCreated: 2023-02-11T09:32:17.392Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [The Linux Network Stack***English** document is available*](/en/Knowledge-base/Linux/the-linux-network-stack)
{.links-list}


# La pila de red de Linux

La pila de red de Linux es un conjunto de componentes de software que permiten la comunicación entre dispositivos en red. Es la base para la creación de redes en el sistema operativo Linux y lo utilizan la mayoría de las aplicaciones orientadas a la red.

La pila de red se divide en cuatro capas principales:

- La capa de enlace, que maneja la comunicación entre los propios dispositivos en red.
- La capa de red, que maneja el enrutamiento del tráfico entre dispositivos en red
- La capa de transporte, que maneja la comunicación de extremo a extremo entre aplicaciones
- La capa de aplicación, que proporciona la interfaz para que las aplicaciones accedan a la red.

Cada una de estas capas tiene una función específica que desempeñar en el funcionamiento de la pila de red.

## La capa de enlace

La capa de enlace es la capa más baja de la pila de red. Es responsable de la comunicación entre los propios dispositivos en red. Esta comunicación generalmente se realiza mediante Ethernet o Wi-Fi.

La capa de enlace es responsable de crear y mantener el enlace entre los dispositivos. Maneja la capa física de la red, que incluye la transmisión de datos a través del medio de la red.

La capa de enlace también maneja la verificación y corrección de errores. Esto es importante para garantizar que el dispositivo receptor reciba los datos correctamente.

## La capa de red

La capa de red es la segunda capa de la pila de red. Es responsable de enrutar el tráfico entre los dispositivos en red.

La capa de red es responsable de proporcionar una vista lógica de la red. Utiliza la capa de enlace para conectar físicamente los dispositivos y luego usa la capa de red para enrutar el tráfico entre ellos.

La capa de red es responsable de encontrar la mejor ruta para que los datos tomen desde el origen hasta el destino. Utiliza una variedad de algoritmos para determinar la mejor ruta.

## La capa de transporte

La capa de transporte es la tercera capa de la pila de red. Es responsable de la comunicación de extremo a extremo entre las aplicaciones.

La capa de transporte es responsable de garantizar que los datos se entreguen correctamente desde la aplicación de origen a la aplicación de destino. Lo hace mediante el uso de una variedad de protocolos, como TCP y UDP.

La capa de transporte también es responsable de proporcionar una conexión confiable entre las aplicaciones. Esto es importante para aplicaciones que requieren una conexión confiable, como transferencias de archivos y correo electrónico.

## La capa de aplicación

La capa de aplicación es la capa más alta de la pila de red. Proporciona la interfaz para que las aplicaciones accedan a la red.

La capa de aplicación es responsable de proporcionar a las aplicaciones los medios para acceder a la red. Lo hace mediante el uso de una variedad de protocolos, como HTTP y FTP.

La capa de aplicación también es responsable de proporcionar seguridad a las aplicaciones. Esto es importante para garantizar que las aplicaciones estén a salvo de ataques.

## Conclusión

La pila de red de Linux es un conjunto de componentes de software que permiten la comunicación entre dispositivos en red. Es la base para la creación de redes en el sistema operativo Linux y lo utilizan la mayoría de las aplicaciones orientadas a la red.

La pila de red se divide en cuatro capas principales: la capa de enlace, la capa de red, la capa de transporte y la capa de aplicación. Cada una de estas capas tiene una función específica que desempeñar en el funcionamiento de la pila de red.