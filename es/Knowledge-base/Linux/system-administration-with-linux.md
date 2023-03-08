---
title: Administración de sistemas con Linux
description: 
published: true
date: 2023-02-11T11:32:22.332Z
tags: 
editor: markdown
dateCreated: 2023-02-11T11:32:20.720Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [System Administration with Linux***English** document is available*](/en/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}


# Administración del Sistema con Linux

La administración del sistema es el proceso de administrar un sistema informático. En general, la administración del sistema incluye tareas como la instalación de software, la configuración del hardware y la gestión de cuentas de usuario.

La administración del sistema puede realizarla un usuario con los privilegios apropiados, como un usuario root. Sin embargo, en la práctica, la administración del sistema suele estar a cargo de un equipo dedicado de administradores.

## Instalación de software

Una de las tareas más comunes para un administrador de sistemas es instalar software. Esto se puede hacer usando un administrador de paquetes como apt.

Apt es una herramienta de línea de comandos que se puede utilizar para instalar, actualizar y eliminar software. Es el administrador de paquetes predeterminado para Debian y Ubuntu.

Para instalar un paquete usando apt, el administrador puede usar el siguiente comando:

```
sudo apt install {package_name}
```

## Configuración de hardware

Otra tarea común para un administrador de sistemas es configurar el hardware. Esto se puede hacer usando la herramienta de administración de hardware, hw-config.

Hw-config es una herramienta de línea de comandos que se puede utilizar para configurar dispositivos de hardware. Se puede utilizar para configurar dispositivos como tarjetas de sonido, tarjetas de red y colas de impresión.

Para configurar un dispositivo usando hw-config, el administrador puede usar el siguiente comando:

```
sudo hw-config {device_name}
```

## Gestión de cuentas de usuario

Otra tarea común para un administrador del sistema es administrar las cuentas de usuario. Esto se puede hacer usando la herramienta de administración de usuarios, usermod.

Usermod es una herramienta de línea de comandos que se puede utilizar para agregar, modificar y eliminar cuentas de usuario. También se puede utilizar para cambiar la contraseña de una cuenta de usuario.

Para agregar un usuario usando usermod, el administrador puede usar el siguiente comando:

```
sudo usermod -a -G {group_name} {username}
```

Para cambiar la contraseña de un usuario usando usermod, el administrador puede usar el siguiente comando:

```
sudo usermod -p {new_password} {username}
```

## Recursos externos

Para obtener más información sobre la administración del sistema, consulte los siguientes recursos:

- [Guía de administración del sistema](https://www.tldp.org/LDP/sag/html/)
- [Guía de administración de Debian](https://debian-handbook.info/browse/stable/)
- [Guía del servidor de Ubuntu] (https://help.ubuntu.com/lts/serverguide/index.html)