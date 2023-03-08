---
title: Configuración de una red privada virtual (VPN) para una comunicación segura
description: 
published: true
date: 2023-02-04T22:55:32.925Z
tags: 
editor: markdown
dateCreated: 2023-02-04T22:55:31.247Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Setting Up a Virtual Private Network (VPN) for Secure Communication***English** document is available*](/en/Knowledge-base/Backend/setting-up-a-virtual-private-network-vpn-for-secure-communication)
{.links-list}


# Configuración de una red privada virtual (VPN) para una comunicación segura

Una red privada virtual (VPN) le permite crear una conexión segura a otra red a través de Internet. Las VPN se pueden usar para acceder a sitios web restringidos por región, proteger su actividad de navegación de miradas indiscretas en Wi-Fi público y más.

La mayoría de los usuarios de Internet no necesitan preocuparse por las VPN. Si solo está tratando de ver Netflix o encriptar sus datos de navegación, puede usar un servicio VPN gratuito como TunnelBear. Pero si busca más seguridad o desea configurar una VPN en su propio servidor, deberá usar un servidor VPN.

## ¿Qué es un servidor VPN?

Un servidor VPN es una computadora o máquina virtual que actúa como puerta de enlace entre su dispositivo e Internet. Cuando te conectas a un servidor VPN, todo tu tráfico se enruta a través de ese servidor. Esto significa que su proveedor de servicios de Internet (ISP) ya no puede ver lo que está haciendo en línea.

Los servidores VPN se pueden usar para acceder a sitios web restringidos por región, proteger su actividad de navegación de miradas indiscretas en Wi-Fi público y más.

## Cómo configurar un servidor VPN

Hay muchas formas diferentes de configurar un servidor VPN. En este artículo, le mostraremos cómo configurar un servidor VPN con Windows Server 2016.

### 1. Instalar Windows Server 2016

Si aún no tiene un servidor, deberá comprar e instalar Windows Server 2016. Puede encontrar instrucciones para hacerlo aquí.

### 2. Configurar el adaptador de red

Una vez que tenga instalado Windows Server 2016, deberá configurar el adaptador de red. Puede hacerlo yendo al Panel de control y abriendo el Centro de redes y recursos compartidos.

Haga clic en Cambiar la configuración del adaptador y luego haga clic derecho en el adaptador de red que desea configurar. Seleccione Propiedades en el menú.

En la ventana Propiedades, seleccione la opción Protocolo de Internet versión 4 (TCP/IPv4) y haga clic en el botón Propiedades.

En la ventana Propiedades de IPv4, seleccione la opción Usar la siguiente dirección IP e ingrese la dirección IP, la máscara de subred y la puerta de enlace predeterminada que desea usar.

Haga clic en el botón Aceptar para guardar los cambios.

### 3. Configurar DNS

El siguiente paso es configurar el DNS. DNS es un sistema que le permite usar nombres de dominio fáciles de recordar (como www.example.com) en lugar de direcciones IP difíciles de recordar (como 192.168.1.1).

Puede configurar DNS en su servidor yendo al Panel de control y abriendo el Administrador de DNS.

En el Administrador de DNS, haga clic con el botón derecho en el servidor DNS y seleccione la opción Propiedades del menú.

En la ventana Propiedades del servidor DNS, seleccione la pestaña Reenviadores.

Haga clic en el botón Editar e ingrese la dirección IP del servidor DNS que desea usar. Puede encontrar una lista de servidores DNS públicos aquí.

Haga clic en el botón Aceptar para guardar los cambios.

### 4. Instalar el servicio de enrutamiento y acceso remoto

El siguiente paso es instalar el Servicio de enrutamiento y acceso remoto (RRAS). RRAS es un servicio de Microsoft que le permite configurar un servidor VPN.

Puede instalar RRAS yendo al Administrador del servidor y seleccionando la opción Agregar roles y características.

En el asistente Agregar roles y características, seleccione la opción de instalación basada en roles o características y haga clic en el botón Siguiente.

En la página Seleccionar funciones, seleccione la casilla de verificación Acceso remoto y haga clic en el botón Siguiente.

En la página Confirmar selecciones de instalación, haga clic en el botón Instalar.

Una vez completada la instalación, haga clic en el botón Cerrar.

### 5. Configurar RRAS

Ahora que RRAS está instalado, deberá configurarlo. Puede hacerlo yendo al Administrador del servidor y seleccionando la opción Herramientas.

En el menú Herramientas, seleccione la opción Enrutamiento y acceso remoto.

En la consola de Enrutamiento y acceso remoto, haga clic con el botón derecho en el servidor y seleccione la opción Configurar y habilitar enrutamiento y acceso remoto.

En el Asistente de configuración, seleccione la opción Configuración personalizada y haga clic en el botón Siguiente.

En la página Configuración personalizada, seleccione las casillas de verificación Acceso VPN, NAT y Enrutamiento LAN y haga clic en el botón Siguiente.

En la página Resumen, haga clic en el botón Finalizar.

### 6. Crear un usuario VPN

El siguiente paso es crear un usuario al que se le permitirá conectarse al servidor VPN. Puede hacerlo yendo al Administrador del servidor y seleccionando la opción Herramientas.

En el menú Herramientas, seleccione la opción Usuarios y equipos de Active Directory.

En la consola Usuarios y equipos de Active Directory, haga clic con el botón derecho en la carpeta Usuarios y seleccione la opción Nuevo usuario del menú.

En la ventana Nuevo usuario, ingrese el Nombre de usuario, el Nombre completo y la Descripción del usuario.

Haga clic en el botón Siguiente.

En la página Contraseña, ingrese la contraseña del usuario y haga clic en el botón Siguiente.

En la página Confirmar contraseña, haga clic en el botón Finalizar.

### 7. Configurar el acceso VPN

El siguiente paso es configurar el acceso VPN para el usuario. Puede hacerlo yendo al Administrador del servidor y seleccionando la opción Herramientas.

En el menú Herramientas, seleccione la opción Enrutamiento y acceso remoto.

En la consola de Enrutamiento y acceso remoto, expanda el servidor y haga clic en la opción Políticas de acceso remoto.

En la ventana Políticas de acceso remoto, haga clic con el botón derecho en Conexiones al servidor de enrutamiento y acceso remoto de Microsoft y seleccione la opción Propiedades del menú.

En la ventana Propiedades de Conexiones al servidor de enrutamiento y acceso remoto de Microsoft, seleccione la pestaña Usuarios.

Haga clic en el botón Agregar y seleccione el usuario al que desea permitir que se conecte al servidor VPN.

Haga clic en el botón Aceptar para guardar los cambios.

### 8. Configurar cliente VPN

El paso final es configurar el cliente VPN en el dispositivo que desea conectar al servidor VPN.

Hay muchos clientes VPN diferentes disponibles, pero usaremos el cliente VPN de Windows integrado.

Para configurar el cliente VPN, vaya al Panel de control y abra el Centro de redes y recursos compartidos.

Haga clic en la opción Configurar una nueva conexión o red.

En la ventana Configurar una conexión o red, seleccione la opción Conectarse manualmente a una red y haga clic en el botón Siguiente.

En la página Propiedades de la conexión, ingrese la información de la conexión VPN. Esto incluye el tipo de VPN (IKEv2), la dirección del servidor VPN, el nombre de usuario VPN y la contraseña VPN.

Haga clic en el botón Crear.

La conexión VPN aparecerá ahora en el Centro de redes y recursos compartidos.

Para conectarse al servidor VPN, haga clic derecho en la conexión y seleccione la opción Conectar del menú.

Ingrese el nombre de usuario y la contraseña de VPN cuando se le solicite y haga clic en el botón Conectar.

Ahora debería estar conectado al servidor VPN.