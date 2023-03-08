---
title: AWS Route 53: creación de un sistema de DNS escalable y resistente en la nube
description: 
published: true
date: 2023-02-06T00:55:53.774Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:55:52.148Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Route 53: Building a Scalable and Resilient DNS System in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-route-53-building-a-scalable-and-resilient-dns-system-in-the-cloud)
{.links-list}


# AWS Route 53: creación de un sistema de DNS escalable y resistente en la nube

El DNS es una parte fundamental de cualquier infraestructura basada en la web, y Route 53 es el servicio de DNS administrado de AWS. En este artículo, veremos cómo usar Route 53 para crear un sistema de DNS escalable y resistente en la nube.

## ¿Qué es DNS?

DNS es el proceso de traducir nombres de dominio legibles por humanos (como www.example.com) en direcciones IP legibles por máquina (como 192.168.1.1). Esto es necesario porque los humanos son mucho mejores para recordar nombres que números.

El DNS es manejado por servidores DNS, que son responsables de mantener una base de datos de nombres de dominio y sus direcciones IP asociadas. Cuando un usuario escribe un nombre de dominio en su navegador, el navegador se pondrá en contacto con un servidor DNS para buscar la dirección IP. El servidor DNS responderá con la dirección IP y el navegador se conectará al servidor web en esa dirección IP.

## ¿Qué es la Ruta 53?

Route 53 es el servicio de DNS administrado de AWS. Es un servicio de DNS escalable y de alta disponibilidad que proporciona una forma rentable de enrutar a los usuarios a las aplicaciones de Internet. Route 53 es totalmente compatible con IPv6 y ofrece una serie de funciones diseñadas para que sea fácil de usar, entre ellas:

- Comprobaciones de estado: Route 53 puede comprobar periódicamente el estado de sus servidores web y desviar el tráfico de los servidores que no están disponibles.

- Enrutamiento basado en la latencia: Route 53 puede enrutar el tráfico al servidor más rápido, según la ubicación del usuario.

- Enrutamiento basado en geolocalización: Route 53 puede enrutar el tráfico a diferentes servidores según la ubicación del usuario. Esto se puede usar para enrutar a los usuarios al servidor más cercano o para enrutar a los usuarios a diferentes versiones de su sitio web según su ubicación.

- Conmutación por error: Route 53 se puede configurar para conmutar por error automáticamente a un servidor en espera si el servidor principal no está disponible.

- Enrutamiento ponderado: Route 53 se puede configurar para enrutar el tráfico a diferentes servidores en función de los pesos que especifique. Esto se puede usar para enrutar más tráfico a un nuevo servidor que está probando o para enrutar menos tráfico a un servidor que está experimentando problemas.

## Creación de una zona alojada de Route 53

Antes de que pueda comenzar a usar Route 53, debe crear una zona alojada. Una zona alojada es una colección de registros DNS para un solo dominio. Por ejemplo, si posee el dominio ejemplo.com, crearía una zona hospedada para ejemplo.com y agregaría registros DNS a la zona hospedada.

Para crear una zona alojada, puede utilizar la consola de administración de AWS, la API de Route 53 o la interfaz de línea de comandos (CLI) de AWS.

## Adición de registros DNS a una zona alojada de Route 53

Una vez que haya creado una zona hospedada, puede agregar registros DNS a la zona hospedada. Los registros DNS se utilizan para enrutar el tráfico a su sitio web o aplicación.

Hay muchos tipos diferentes de registros DNS, pero el tipo más común es un registro A. Un registro A asigna un nombre de dominio a una dirección IPv4. Por ejemplo, podría crear un registro A para el dominio ejemplo.com que apunte a la dirección IPv4 192.168.1.1.

Para agregar un registro A a una zona alojada de Route 53, puede utilizar la Consola de administración de AWS, la API de Route 53 o la Interfaz de línea de comandos (CLI) de AWS.

## Enrutamiento del tráfico a una instancia de Amazon EC2

En esta sección, veremos cómo enrutar el tráfico a una instancia de Amazon EC2. Amazon EC2 es un servicio web que proporciona capacidad informática redimensionable en la nube.

Para enrutar el tráfico a una instancia de Amazon EC2, debe crear un registro A que apunte a la dirección IP pública de la instancia de Amazon EC2. La dirección IP pública de una instancia de Amazon EC2 se puede encontrar en la consola de Amazon EC2.

## Enrutamiento del tráfico a un depósito de Amazon S3

En esta sección, veremos cómo enrutar el tráfico a un depósito de Amazon S3. Amazon S3 es un servicio web que proporciona almacenamiento en la nube.

Para enrutar el tráfico a un depósito de Amazon S3, debe crear un registro CNAME que apunte al depósito de Amazon S3. El depósito de Amazon S3 debe configurarse para que sea accesible desde Internet.

## Comprobaciones de estado de la ruta 53

Route 53 se puede utilizar para comprobar periódicamente el estado de sus servidores web y desviar el tráfico de los servidores que no están disponibles. Esto se conoce como control de salud.

Cuando crea una comprobación de estado, especifica el protocolo (HTTP, HTTPS o TCP), el puerto y la ruta o el dominio que desea que utilice Route 53 para comprobar el estado de su servidor web. Luego, Route 53 enviará periódicamente solicitudes a la ruta o dominio especificado y verificará el código de respuesta para determinar el estado del servidor web.

Si desea enrutar el tráfico a un servidor específico según el estado del servidor, puede crear una verificación de estado para cada servidor y luego configurar Route 53 para enrutar el tráfico a los servidores en buen estado.

## Route 53 Enrutamiento basado en latencia

Route 53 se puede utilizar para enrutar el tráfico al servidor más rápido, según la ubicación del usuario. Esto se conoce como enrutamiento basado en la latencia.

Para usar el enrutamiento basado en la latencia, debe crear un conjunto de registros de recursos de latencia para cada servidor al que desea enrutar el tráfico. Luego, Route 53 verificará periódicamente la latencia entre el usuario y cada servidor para determinar el servidor más rápido.

## Route 53 Enrutamiento basado en geolocalización

Route 53 se puede utilizar para enrutar el tráfico a diferentes servidores según la ubicación del usuario. Esto se conoce como enrutamiento basado en geolocalización.

Para utilizar el enrutamiento basado en geolocalización, debe crear un conjunto de registros de recursos de geolocalización para cada servidor al que desea enrutar el tráfico. Luego, Route 53 usará la ubicación del usuario para determinar a qué servidor enrutar el tráfico.

## Conmutación por error de la ruta 53

Route 53 se puede configurar para conmutar por error automáticamente a un servidor en espera si el servidor principal no está disponible. Esto se conoce como conmutación por error.

Para utilizar la conmutación por error, debe crear un conjunto de registros de recursos de conmutación por error para cada servidor al que desee enrutar el tráfico. Luego, Route 53 verificará periódicamente el estado del servidor principal. Si el servidor principal no está disponible, Route 53 enrutará el tráfico al servidor en espera.

## Ruta 53 Enrutamiento ponderado

Route 53 se puede configurar para enrutar el tráfico a diferentes servidores en función de los pesos que especifique. Esto se conoce como enrutamiento ponderado.

Para usar el enrutamiento ponderado, debe crear un conjunto de registros de recursos ponderados para cada servidor al que desea enrutar el tráfico. Luego, Route 53 usará los pesos que especifique para determinar a qué servidor enrutar el tráfico.

## Conclusión

En este artículo, analizamos cómo usar Route 53 para crear un sistema de DNS escalable y resistente en la nube. Hemos visto cómo crear una zona alojada de Route 53, agregar registros DNS a la zona alojada y enrutar el tráfico a las instancias de Amazon EC2 y Amazon S3. También hemos visto cómo usar las comprobaciones de estado de Route 53, el enrutamiento basado en latencia, el enrutamiento basado en geolocalización, la conmutación por error y el enrutamiento ponderado.