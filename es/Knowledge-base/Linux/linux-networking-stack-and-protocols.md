---
title: Protocolos y pila de red de Linux
description: 
published: true
date: 2023-02-11T22:32:17.047Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:32:15.422Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Networking Stack and Protocols***English** document is available*](/en/Knowledge-base/Linux/linux-networking-stack-and-protocols)
{.links-list}


Las redes de Linux son un tema amplio y complejo. En este artículo, nos centraremos en la pila y los protocolos de red.

## La pila de redes de Linux

La pila de red de Linux se compone de varios componentes, cada uno con su propia función que desempeñar.

### El núcleo

En el corazón de la pila de redes de Linux se encuentra el kernel. El núcleo es responsable de administrar todos los recursos de hardware, incluidos los dispositivos de red. También implementa los principales protocolos de red, como TCP/IP.

### La cáscara

Encima del núcleo está la cáscara. El shell es una interfaz de usuario que le permite interactuar con el kernel. Proporciona una forma de ejecutar comandos y ejecutar programas.

### Los archivos de configuración

El shell usa archivos de configuración para controlar el comportamiento del núcleo y los programas que se ejecutan sobre él. Los archivos de configuración más importantes para redes son el archivo /etc/hosts, que asigna nombres de host a direcciones IP, y el archivo /etc/resolv.conf, que define los servidores DNS que se utilizarán para resolver nombres de host.

### Las utilidades

Hay muchas utilidades que se utilizan para configurar y solucionar problemas de red. Algunos de los más importantes son ifconfig, que se usa para configurar las interfaces de red, y ping, que se usa para probar la conectividad.

## La pila de protocolos TCP/IP

La pila de protocolos TCP/IP es el conjunto de protocolos que se utilizan para implementar la funcionalidad principal de Internet. Está formado por cuatro capas:

- La capa de aplicación, que es la capa en la que las aplicaciones se comunican entre sí.
- La capa de transporte, que es responsable de la comunicación de extremo a extremo entre hosts.
- La capa de red, que se encarga de enrutar el tráfico entre hosts.
- La capa de enlace, que se encarga de proporcionar conectividad entre los hosts de una misma red.

La pila TCP/IP se implementa en el kernel y el shell proporciona utilidades para configurarlo y solucionar problemas.

## Referencias

- https://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/c1022.htm
- https://www.thegeekstuff.com/2012/03/linux-networking-stack/
- https://www.redhat.com/en/blog/introduction-linux-networking-stack-part-1