---
title: Configuración de red y firewall de Linux
description: 
published: true
date: 2023-02-11T23:32:29.231Z
tags: 
editor: markdown
dateCreated: 2023-02-11T23:32:27.475Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Networking and Firewall Configuration***English** document is available*](/en/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}


# Configuración de red y firewall de Linux

Dado que la gran mayoría de las amenazas provienen de Internet, una buena configuración de firewall es fundamental para cualquier servidor Linux. Esta guía presentará los conceptos básicos para configurar un firewall con la popular herramienta iptables.

## Tabla de contenido

- [¿Qué es un cortafuegos?](# qué-es-un-cortafuegos)
- [iptables](# iptables)
  - [Instalando iptables](# instalando-iptables)
  - [Configurando iptables](# configurando-iptables)
- [Conclusión](# conclusión)
- [Recursos](# recursos)

## ¿Qué es un cortafuegos?

En informática, un firewall es un sistema de seguridad de red que supervisa y controla el tráfico de red entrante y saliente en función de reglas de seguridad predeterminadas. Un firewall generalmente establece una barrera entre una red interna confiable y una red externa que no es confiable, como Internet.

## iptables

Iptables es una popular herramienta de firewall incluida con la mayoría de las distribuciones de Linux. Utiliza un conjunto de reglas para determinar qué tráfico permitir o bloquear.

### Instalación de iptables

Iptables se incluye con la mayoría de las distribuciones de Linux y se puede instalar con el administrador de paquetes. Por ejemplo, en sistemas basados en Debian:

```
$ sudo apt-get install iptables
```

### Configurando iptables

Iptables usa un conjunto de cadenas para determinar qué hacer con un paquete. Un paquete puede descartarse, rechazarse o aceptarse. Las cadenas predeterminadas son `INPUT`, `FORWARD` y `OUTPUT`.

#### Normas

Una regla en iptables consta de una serie de criterios de coincidencia y un objetivo. Los criterios de coincidencia pueden ser cosas como el protocolo (por ejemplo, TCP, UDP), las direcciones IP de origen y destino y los números de puerto de origen y destino. El destino puede ser `DROP`, `REJECT` o `ACCEPT`.

##### Agregar una regla

Las reglas se pueden agregar con el comando `iptables`. Por ejemplo, para descartar todo el tráfico entrante:

```
$ iptables -A INPUT -j DROP
```

Esta regla se agregará a la cadena 'INPUT' y tendrá el destino 'DROP', que descartará el paquete.

##### Eliminar una regla

Las reglas se pueden eliminar con el comando `iptables`. Por ejemplo, para eliminar la regla anterior:

```
$ iptables -D INPUT 1
```

Esto eliminará la primera regla en la cadena `INPUT`.

##### Reglas de guardado

Las reglas se pueden guardar con el comando `iptables-save`. Por ejemplo:

```
$ iptables-save > /etc/iptables.rules
```

Esto guardará las reglas en el archivo `/etc/iptables.rules`.

##### Reglas de carga

Las reglas se pueden cargar con el comando `iptables-restore`. Por ejemplo:

```
$ iptables-restore < /etc/iptables.rules
```

Esto cargará las reglas del archivo `/etc/iptables.rules`.

## Conclusión

Esta guía ha introducido los conceptos básicos para configurar un firewall con iptables. Para obtener más información, consulte los recursos a continuación.

## Recursos

- [Tutorial de Iptables](https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture)
- [Cómo configurar un cortafuegos con UFW en un servidor en la nube Ubuntu y Debian](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an- ubuntu-y-debian-servidor-en-la-nube)
- [Cómo proteger su servidor con CSF Firewall en CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-secure-your-server-with-csf-firewall-on-centos-7 )