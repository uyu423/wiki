---
title: AWS Lightsail: Lanzamiento de sitios web y aplicaciones simples con una PaaS totalmente administrada
description: 
published: true
date: 2023-02-06T11:56:00.571Z
tags: 
editor: markdown
dateCreated: 2023-02-06T11:55:58.667Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [AWS Lightsail: Launching Simple Websites and Applications with a Fully Managed PaaS***English** document is available*](/en/Knowledge-base/Cloud/aws-lightsail-launching-simple-websites-and-applications-with-a-fully-managed-paas)
{.links-list}


# AWS Lightsail: Lanzamiento de sitios web y aplicaciones simples con una PaaS totalmente administrada

AWS Lightsail es una plataforma como servicio (PaaS) completamente administrada que facilita el lanzamiento de aplicaciones y sitios web simples. Lightsail incluye todo lo que necesita para lanzar su proyecto, incluido un servidor privado virtual, una base de datos administrada, administración de DNS y una dirección IP estática.

Lightsail es una excelente opción para lanzar sitios web y aplicaciones simples porque es fácil de usar y solo paga por los recursos que usa. No hay costos iniciales ni contratos a largo plazo. Puede crear una instancia de Lightsail en minutos y puede escalar sus recursos a medida que crece su proyecto.

## Introducción a Lightsail

Para comenzar con Lightsail, primero debe crear una cuenta y elegir una región. Puede crear una cuenta en https://lightsail.aws.amazon.com/.

Una vez que haya creado una cuenta, puede crear una instancia de Lightsail. Para hacer esto, haga clic en el botón "Crear instancia" y elija su tipo de instancia. Lightsail ofrece una variedad de tipos de instancias, incluidos servidores privados virtuales Linux y Windows, contenedores y direcciones IP estáticas.

Una vez que haya seleccionado su tipo de instancia, puede elegir su plan de instancia. Lightsail ofrece una variedad de planes, incluidos planes mensuales y por horas.

Una vez que haya elegido su plan de instancia, puede seleccionar el sistema operativo, las aplicaciones y los recursos adicionales para su instancia. Lightsail ofrece una variedad de sistemas operativos populares, incluidos Amazon Linux, Ubuntu y Windows Server.

También puede seleccionar las aplicaciones y los recursos adicionales para su instancia, como WordPress, Drupal, Joomla! y Magento.

Una vez que haya seleccionado el sistema operativo, las aplicaciones y los recursos adicionales para su instancia, puede elegir un nombre para su instancia y hacer clic en el botón "Crear instancia".

Ahora se creará su instancia de Lightsail y podrá acceder a ella a través de la consola de Lightsail.

## Conexión a su instancia de Lightsail

Para conectarse a su instancia de Lightsail, primero debe descargar el cliente de Lightsail. El cliente de Lightsail es una interfaz de línea de comandos (CLI) que puede usar para administrar sus recursos de Lightsail.

Puede descargar el cliente de Lightsail desde la consola de Lightsail. Para ello, haga clic en el menú "Cuenta" y seleccione "Descargar cliente".

Una vez que haya descargado el cliente de Lightsail, puede conectarse a su instancia de Lightsail con el siguiente comando:

```
lightsail-client connect --instance-name my-instance
```

Reemplace "my-instance" con el nombre de su instancia de Lightsail.

Ahora se le pedirá que ingrese su nombre de usuario y contraseña de Lightsail. Una vez que haya ingresado sus credenciales, se conectará a su instancia de Lightsail.

## Administración de su instancia de Lightsail

Una vez que esté conectado a su instancia de Lightsail, puede usar el cliente de Lightsail para administrar su instancia.

Para ver una lista de todos los comandos disponibles, puede usar el comando "ayuda":

```
lightsail-client help
```

Para ver información sobre un comando específico, puede usar el comando "ayuda" seguido del nombre del comando. Por ejemplo, para ver información sobre el comando "conectar", puede usar el siguiente comando:

```
lightsail-client help connect
```

Para ver una lista de todas las instancias de Lightsail en su cuenta, puede usar el comando "list-instances":

```
lightsail-client list-instances
```

Para ver información sobre una instancia específica de Lightsail, puede usar el comando "describir-instancia" seguido del nombre de la instancia. Por ejemplo, para ver información sobre la instancia de Lightsail "my-instance", puede usar el siguiente comando:

```
lightsail-client describe-instance --instance-name my-instance
```

Para detener una instancia de Lightsail, puede usar el comando "stop-instance" seguido del nombre de la instancia. Por ejemplo, para detener la instancia de Lightsail "my-instance", puede usar el siguiente comando:

```
lightsail-client stop-instance --instance-name my-instance
```

Para iniciar una instancia de Lightsail, puede usar el comando "start-instance" seguido del nombre de la instancia. Por ejemplo, para iniciar la instancia de Lightsail "my-instance", puede usar el siguiente comando:

```
lightsail-client start-instance --instance-name my-instance
```

Para eliminar una instancia de Lightsail, puede usar el comando "delete-instance" seguido del nombre de la instancia. Por ejemplo, para eliminar la instancia de Lightsail "my-instance", puede usar el siguiente comando:

```
lightsail-client delete-instance --instance-name my-instance
```

## Creación de una instantánea de Lightsail

Una instantánea de Lightsail es una copia de seguridad de un momento dado de su instancia de Lightsail. Puede usar instantáneas para crear nuevas instancias de Lightsail o para restaurar una instancia de Lightsail existente.

Para crear una instantánea de su instancia de Lightsail, puede usar el comando "crear instantánea" seguido del nombre de la instancia. Por ejemplo, para crear una instantánea de la instancia de Lightsail "my-instance", puede usar el siguiente comando:

```
lightsail-client create-snapshot --instance-name my-instance
```

Para ver una lista de todas las instantáneas en su cuenta, puede usar el comando "list-snapshots":

```
lightsail-client list-snapshots
```

Para ver información sobre una instantánea específica, puede usar el comando "describe-snapshot" seguido del nombre de la instantánea. Por ejemplo, para ver información sobre la instantánea "my-snapshot", puede usar el siguiente comando:

```
lightsail-client describe-snapshot --snapshot-name my-snapshot
```

Para eliminar una instantánea, puede utilizar el comando "delete-snapshot" seguido del nombre de la instantánea. Por ejemplo, para eliminar la instantánea "my-snapshot", puede usar el siguiente comando:

```
lightsail-client delete-snapshot --snapshot-name my-snapshot
```

## Creación de una instancia de Lightsail a partir de una instantánea

Para crear una instancia de Lightsail a partir de una instantánea, puede utilizar el comando "crear instancia a partir de una instantánea" seguido del nombre de la instantánea. Por ejemplo, para crear una instancia de Lightsail a partir de la instantánea "my-snapshot", puede usar el siguiente comando:

```
lightsail-client create-instance-from-snapshot --snapshot-name my-snapshot
```

## Conclusión

En este artículo, hemos analizado cómo lanzar sitios web y aplicaciones simples con AWS Lightsail. Lightsail es una excelente opción para lanzar sitios web y aplicaciones simples porque es fácil de usar y solo paga por los recursos que usa.

Si está buscando una PaaS totalmente administrada para lanzar su próximo proyecto, entonces Lightsail es una excelente opción.