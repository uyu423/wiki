---
title: Gestión de paquetes de Linux con apt y yum
description: 
published: true
date: 2023-02-12T09:32:25.387Z
tags: 
editor: markdown
dateCreated: 2023-02-12T09:32:18.638Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Package Management with apt and yum***English** document is available*](/en/Knowledge-base/Linux/linux-package-management-with-apt-and-yum)
{.links-list}



# Gestión de paquetes Linux con apt y yum

La gestión de paquetes es una parte importante de cualquier distribución de Linux. Le permite instalar, actualizar y eliminar paquetes de software de su sistema. En este artículo, veremos dos de las herramientas de administración de paquetes más populares: apt y yum.

## apto

apt (Advanced Package Tool) es el administrador de paquetes predeterminado para los sistemas Debian y Ubuntu. Es una poderosa herramienta que se puede usar para instalar, actualizar y eliminar paquetes de software de su sistema. apt también es capaz de resolver dependencias, por lo que no tiene que preocuparse por instalar manualmente todas las dependencias requeridas para un paquete de software en particular.

Para instalar un paquete de software usando apt, puede usar el siguiente comando:

```
sudo apt install {package-name}
```

Por ejemplo, para instalar el editor de texto "vim", usaría el siguiente comando:

```
sudo apt install vim
```

Si desea actualizar todos los paquetes de software en su sistema, puede usar el siguiente comando:

```
sudo apt update
```

Para actualizar todos los paquetes de software en su sistema a sus últimas versiones, puede usar el siguiente comando:

```
sudo apt upgrade
```

Si desea eliminar un paquete de software de su sistema, puede usar el siguiente comando:

```
sudo apt remove {package-name}
```

Por ejemplo, para eliminar el editor de texto "vim", usaría el siguiente comando:

```
sudo apt remove vim
```

## ñam

yum (Yellowdog Updater Modified) es el administrador de paquetes predeterminado para los sistemas Red Hat y CentOS. Es una poderosa herramienta que se puede usar para instalar, actualizar y eliminar paquetes de software de su sistema. yum también es capaz de resolver dependencias, por lo que no tiene que preocuparse por instalar manualmente todas las dependencias requeridas para un paquete de software en particular.

Para instalar un paquete de software usando yum, puede usar el siguiente comando:

```
sudo yum install {package-name}
```

Por ejemplo, para instalar el editor de texto "vim", usaría el siguiente comando:

```
sudo yum install vim
```

Si desea actualizar todos los paquetes de software en su sistema, puede usar el siguiente comando:

```
sudo yum update
```

Para actualizar todos los paquetes de software en su sistema a sus últimas versiones, puede usar el siguiente comando:

```
sudo yum upgrade
```

Si desea eliminar un paquete de software de su sistema, puede usar el siguiente comando:

```
sudo yum remove {package-name}
```

Por ejemplo, para eliminar el editor de texto "vim", usaría el siguiente comando:

```
sudo yum remove vim
```

## Conclusión

En este artículo, hemos analizado dos de las herramientas de administración de paquetes más populares: apt y yum. Ambas herramientas son poderosas y se pueden usar para administrar los paquetes de software en su sistema.