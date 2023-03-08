---
title: Administración de servidor web y base de datos Linux
description: 
published: true
date: 2023-02-12T11:33:40.985Z
tags: 
editor: markdown
dateCreated: 2023-02-12T11:33:39.248Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Web Server and Database Administration***English** document is available*](/en/Knowledge-base/Linux/linux-web-server-and-database-administration)
{.links-list}


# Servidor web Linux y administración de base de datos

En este artículo, cubriremos los conceptos básicos de la administración de un servidor web y una base de datos Linux. Comenzaremos con una descripción general de las tareas más comunes y luego profundizaremos en cada una de ellas con más detalle.

## Descripción general

Las tareas más comunes al administrar un servidor web Linux son:

- Configuración del software del servidor web
- Configuración de nombres de dominio y DNS
- Gestión de cuentas de usuario.
- Asegurando el servidor
- Copia de seguridad y recuperación ante desastres
- Monitoreo del servidor

Cubriremos cada uno de estos temas con más detalle a continuación.

## Configuración del software del servidor web

La primera tarea al configurar un nuevo servidor web es instalar y configurar el software del servidor web. El software de servidor web más popular para Linux es Apache HTTP Server. Otros servidores web populares incluyen nginx y lighttpd.

El software del servidor web es responsable de manejar las solicitudes de los clientes (navegadores) y devolver la respuesta apropiada (generalmente una página web). También proporciona otras funciones, como compatibilidad con CGI, alojamiento virtual y protección con contraseña.

La configuración del software del servidor web generalmente se realiza a través de un archivo de texto llamado ```httpd.conf```. Este archivo generalmente se encuentra en el directorio ```/etc/apache2/``` en los sistemas Debian y Ubuntu, y en el directorio ```/etc/httpd/conf/``` en los sistemas Red Hat y CentOS.

El archivo ```httpd.conf``` contiene muchas directivas diferentes que se pueden usar para configurar el servidor. Algunas de las directivas más comunes son:

- ```ServerRoot```: Esta directiva especifica el directorio donde se encuentran los archivos de configuración del servidor.
- ```Listen```: Esta directiva especifica el número de puerto en el que el servidor debe escuchar. El puerto predeterminado para HTTP es 80.
- ```DocumentRoot```: Esta directiva especifica el directorio donde se encuentran los archivos web del servidor. Este suele ser el directorio ```/var/www/html/```.
- ```<Directorio>```: Esta directiva se utiliza para especificar la configuración de un directorio específico.
- ```<VirtualHost>```: Esta directiva se usa para configurar hosts virtuales. Los servidores virtuales permiten que varios sitios web se alojen en el mismo servidor.

Para obtener más información sobre el servidor Apache HTTP, consulte los siguientes recursos:

- La documentación del servidor Apache HTTP: https://httpd.apache.org/docs/
- El tutorial del servidor Apache HTTP: https://httpd.apache.org/docs/2.4/en/tutorial.html

## Configuración de nombres de dominio y DNS

La siguiente tarea es configurar nombres de dominio y DNS. Los nombres de dominio se utilizan para identificar sitios web en Internet. Suelen tener la forma de ```www.example.com```.

DNS es el sistema que se utiliza para asignar nombres de dominio a direcciones IP. Cuando escribe un nombre de dominio en su navegador, el DNS se utiliza para buscar la dirección IP del servidor que aloja el sitio web.

Hay dos partes para configurar nombres de dominio y DNS: registrar el nombre de dominio y configurar DNS.

Para registrar un nombre de dominio, debe encontrar un registrador de nombres de dominio. Esta es una empresa que vende nombres de dominio. Una vez que haya encontrado un registrador, puede buscar nombres de dominio disponibles y comprar uno.

Una vez que haya registrado un nombre de dominio, debe configurar el DNS. Esto se puede hacer usando los comandos ```dig``` y ```nslookup```. Para obtener más información, consulte los siguientes recursos:

- Cómo usar el comando Dig en Linux: https://www.howtogeek.com/427654/htg-explains-what-is-dig-and-how-to-use-it/
- Cómo usar el comando NSlookup en Linux: https://www.howtogeek.com/427950/htg-explains-what-is-nslookup-and-how-to-use-it/

## Administrar cuentas de usuario

La siguiente tarea es administrar las cuentas de usuario. En un servidor Linux, hay dos tipos de cuentas de usuario: cuentas del sistema y cuentas de usuario.

Las cuentas del sistema son utilizadas por el sistema para ejecutar ciertos servicios. Por lo general, tienen un UID numérico y no están destinados a ser utilizados por usuarios humanos.

Las cuentas de usuario son utilizadas por usuarios humanos para iniciar sesión en el sistema. Suelen tener un nombre de usuario y una contraseña.

Para administrar cuentas de usuario, puede usar los comandos ```useradd```, ```usermod``` y ```userdel```. Para obtener más información, consulte los siguientes recursos:

- Cómo agregar y eliminar usuarios en un VPS de Linux: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-a-linux-vps
- Cómo cambiar la contraseña de un usuario en Linux: https://www.digitalocean.com/community/tutorials/how-to-change-a-user-s-password-in-linux

## Asegurar el servidor

La siguiente tarea es asegurar el servidor. Hay muchas formas de asegurar un servidor Linux, pero cubriremos las más comunes.

La primera forma de asegurar un servidor es instalar un firewall. Un firewall es un dispositivo de software o hardware que filtra el tráfico que pasa a través de él. Se puede usar para bloquear el tráfico no deseado y permitir solo tráfico específico.

El software de firewall más común para Linux es iptables. Otros firewalls populares incluyen firewalld y ufw.

La segunda forma de proteger un servidor es cifrar las comunicaciones. La forma más común de hacer esto es usar SSL/TLS. SSL/TLS es un protocolo que se utiliza para cifrar la comunicación entre un servidor y un cliente.

Para cifrar las comunicaciones, debe generar un certificado. Un certificado es un archivo que contiene información sobre el servidor y la clave de cifrado. A continuación, el servidor y el cliente utilizan el certificado para cifrar y descifrar la comunicación.

Para generar un certificado, puede utilizar el comando ```openssl```. Para obtener más información, consulte los siguientes recursos:

- Cómo instalar un certificado SSL/TLS en Apache: https://www.digitalocean.com/community/tutorials/how-to-install-an-ssl-certificate-from-a-commercial-certificate-authority
- Cómo crear un certificado SSL autofirmado para Apache en CentOS 7: https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache- en-centos-7

La tercera forma de asegurar un servidor es usar un escáner de seguridad. Un escáner de seguridad es una herramienta que se utiliza para escanear un sistema en busca de vulnerabilidades de seguridad. El escáner de seguridad más popular para Linux es Nessus.

Para obtener más información sobre cómo proteger un servidor Linux, consulte los siguientes recursos:

- Cómo proteger un servidor con reglas de firewall: https://www.digitalocean.com/community/tutorials/how-to-secure-a-server-with-firewall-rules-ufw
- Cómo configurar un cortafuegos con UFW en un servidor en la nube Ubuntu y Debian: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-an -ubuntu-y-debian-servidor en la nube
- Cómo endurecer SSH en un Ubuntu VPS: https://www.digitalocean.com/community/tutorials/how-to-harden-ssh-on-an-ubuntu-vps

## Copia de seguridad y recuperación ante desastres

La siguiente tarea es configurar un plan de copia de seguridad y recuperación ante desastres. Hay muchas maneras diferentes de hacer esto, pero cubriremos las más comunes.

La primera forma de configurar una copia de seguridad es usar una herramienta llamada ```rsync```. ```rsync``` es una herramienta que se puede utilizar para copiar archivos de una ubicación a otra. Se puede utilizar para crear copias de seguridad de archivos y directorios.

La segunda forma de configurar una copia de seguridad es usar una herramienta llamada ```tar```. ```tar``` es una herramienta que se puede utilizar para crear archivos de archivos y directorios. Los archivos se pueden usar para comprimir archivos y hacer copias de seguridad.

La tercera forma de configurar una copia de seguridad es usar una herramienta llamada ```dd```. ```dd``` es una herramienta que se puede utilizar para crear imágenes de disco. Las imágenes de disco se pueden utilizar para realizar copias de seguridad de particiones o discos completos.

Para obtener más información sobre la copia de seguridad de un servidor Linux, consulte los siguientes recursos:

- Cómo hacer una copia de seguridad de los archivos de su servidor usando ```rsync```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-files-using-rsync
- Cómo hacer una copia de seguridad de su servidor usando ```tar```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-tar
- Cómo hacer una copia de seguridad de su servidor usando ```dd```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-dd

La segunda parte de la configuración de un plan de copia de seguridad y recuperación ante desastres es crear un plan de recuperación ante desastres. Este plan debe describir cómo recuperarse de un desastre importante, como una falla del servidor.

El primer paso para crear un plan de recuperación ante desastres es identificar los componentes críticos del sistema. Esto incluye el software del servidor web, el software de la base de datos y los datos.

El segundo paso es identificar los métodos de copia de seguridad que se utilizarán. Esto incluye las herramientas que se utilizarán para crear las copias de seguridad, la frecuencia de las copias de seguridad y la ubicación de las copias de seguridad.

El tercer paso es identificar los métodos de recuperación que se utilizarán. Esto incluye las herramientas que se utilizarán para restaurar las copias de seguridad, el orden en que se recuperarán los componentes y la ubicación de las copias de seguridad.

Para obtener más información sobre cómo crear un plan de recuperación ante desastres, consulte los siguientes recursos:

- Cómo crear un plan de recuperación ante desastres para un sitio web: https://www.digitalocean.com/community/tutorials/how-to-create-a-website-disaster-recovery-plan
- Cómo prepararse para la migración de un servidor: https://www.digitalocean.com/community/tutorials/how-to-prepare-for-a-server-migration

## Monitoreando el servidor

La tarea final es monitorear el servidor. Esto incluye la supervisión de los recursos del servidor, como la CPU, la memoria y el uso del disco, y la supervisión de los servicios del servidor, como el servidor web y el servidor de la base de datos.

Hay muchas herramientas que se pueden usar para monitorear un servidor. Algunas de las herramientas más populares son:

- arriba
- arriba
- iotop
-vmstat
- netstat

Para obtener más información sobre cómo monitorear un servidor Linux, consulte los siguientes recursos:

- Cómo monitorear las métricas del sistema con ```netdata``` en Ubuntu 16.04: https://www.digitalocean.com/community/tutorials/how-to-monitor-system-metrics-with-netdata-on-ubuntu- 16-04
- Cómo monitorear los recursos de su servidor con ```miradas``` en Ubuntu 16.04: https://www.digitalocean.com/community/tutorials/how-to-monitor-your-server-resources-with-glances-on -ubuntu-16-04

## Recursos externos

- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-web-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-database-administration