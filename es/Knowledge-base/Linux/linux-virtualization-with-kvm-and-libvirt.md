---
title: Virtualización de Linux con KVM y libvirt
description: 
published: true
date: 2023-02-12T04:32:38.260Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:32:36.474Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Virtualization with KVM and libvirt***English** document is available*](/en/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}


# Virtualización de Linux con KVM y libvirt

## Introducción

La virtualización es el proceso de crear una versión virtual de algo, como un sistema operativo, un servidor, un dispositivo de almacenamiento o recursos de red. Es una tecnología poderosa que tiene muchos usos, incluida la consolidación de varios servidores en un solo servidor físico, la creación de entornos de prueba y desarrollo, y más.

Linux ha sido durante mucho tiempo un líder en virtualización con muchas tecnologías de virtualización diferentes disponibles. En este artículo, nos centraremos en dos de los más populares: KVM y libvirt.

## ¿Qué es KVM?

KVM (máquina virtual basada en el kernel) es una solución de virtualización completa para Linux que se incluye en el kernel principal de Linux desde la versión 2.6.20. Para usar KVM, su CPU debe tener extensiones de virtualización de hardware, como Intel VT-x o AMD-V.

KVM es un hipervisor que se ejecuta sobre un kernel de Linux y proporciona capacidades de virtualización mediante extensiones de virtualización de hardware. KVM está incluido en el núcleo principal de Linux y muchas distribuciones de Linux lo utilizan como su solución de virtualización predeterminada.

## ¿Qué es libvirt?

libvirt es un conjunto de herramientas que proporciona una API unificada para administrar plataformas de virtualización, como KVM, Xen y otras. Lo utilizan muchas herramientas de administración de virtualización, como virt-manager, y también está disponible como una herramienta de línea de comandos.

libvirt proporciona una API poderosa y fácil de usar para administrar máquinas virtuales y otros recursos de virtualización, como almacenamiento y redes. Está disponible como herramienta de línea de comandos y como biblioteca que pueden utilizar otros programas.

## Primeros pasos con KVM y libvirt

Para usar KVM y libvirt, necesita un sistema Linux con extensiones de virtualización de hardware y una versión reciente del kernel de Linux. KVM está incluido en el kernel principal de Linux, por lo que no debería tener problemas para obtenerlo si está utilizando una versión reciente del kernel de su distribución.

Una vez que tenga un sistema Linux con extensiones de virtualización de hardware y un kernel reciente, puede instalar KVM y libvirt con el administrador de paquetes de su distribución. Por ejemplo, en los sistemas Debian y Ubuntu, puede instalarlos con el siguiente comando:

```
sudo apt-get install kvm libvirt-bin
```

Una vez que KVM y libvirt están instalados, puede usar la herramienta virt-manager para administrar sus máquinas virtuales. virt-manager es una herramienta gráfica que facilita la creación y administración de máquinas virtuales.

## Creación de una máquina virtual

 virt-manager es una herramienta gráfica para administrar máquinas virtuales. Para ejecutarlo, escriba el siguiente comando:

```
virt-manager
```

Verá la ventana de virt-manager que se muestra en la Figura 1.


Figura 1. La ventana de virt-manager

Para crear una nueva máquina virtual, haga clic en el menú Archivo y seleccione Nueva máquina virtual. Verá la ventana New VM Wizard que se muestra en la Figura 2.


Figura 2. La ventana del Asistente para nueva máquina virtual

En la primera página del asistente, seleccione la opción Medios de instalación local y haga clic en Reenviar. En la página siguiente, seleccione la opción de imagen ISO y haga clic en Adelante. En la página siguiente, seleccione el botón Examinar y busque la ubicación de su imagen ISO. Luego, seleccione el botón Reenviar.

En la página siguiente, verá una lista de los sistemas operativos disponibles. Seleccione el sistema operativo que desea instalar y haga clic en Adelante. En la página siguiente, ingrese un nombre para su máquina virtual y haga clic en Reenviar.

En la página siguiente, verá una lista de dispositivos de almacenamiento disponibles. Seleccione el dispositivo de almacenamiento que desea usar y haga clic en Reenviar. En la página siguiente, verá una lista de dispositivos de red disponibles. Seleccione el dispositivo de red que desea usar y haga clic en Reenviar.

En la página siguiente, verá una lista de modelos de CPU disponibles. Seleccione el modelo de CPU que desea usar y haga clic en Adelante. En la página siguiente, verá una lista de los tamaños de memoria disponibles. Seleccione el tamaño de memoria que desea usar y haga clic en Adelante.

En la página siguiente, verá una lista de dispositivos de video disponibles. Seleccione el dispositivo de video que desea usar y haga clic en Reenviar. En la página final, revise sus selecciones y haga clic en Finalizar.

La herramienta virt-manager ahora creará su máquina virtual y la iniciará desde la imagen ISO que seleccionó. La máquina virtual estará en estado de pausa, por lo que deberá hacer clic en el botón Reanudar para iniciarla.

## Conexión a una máquina virtual

Una vez que su máquina virtual esté funcionando, puede conectarse a ella usando la herramienta virt-manager. Para ello, seleccione su máquina virtual en la ventana de virt-manager y haga clic en el botón Conectar. Verá la ventana Conectar a VM que se muestra en la Figura 3.


Figura 3. La ventana Conectar a VM

En la primera página del asistente, seleccione la opción VNC y haga clic en Adelante. En la página siguiente, verá una lista de visores VNC disponibles. Seleccione el visor que desea usar y haga clic en Adelante. En la página final, revise sus selecciones y haga clic en Finalizar.

La herramienta virt-manager ahora iniciará su visor VNC y se conectará a su máquina virtual. Verá la pantalla de inicio de sesión para su máquina virtual.

## Gestión de máquinas virtuales con virsh

Además de la herramienta virt-manager, también puede usar la herramienta virsh para administrar sus máquinas virtuales. virsh es una herramienta de línea de comandos que proporciona un poderoso conjunto de comandos para administrar máquinas virtuales.

Para enumerar todos los comandos virsh disponibles, escriba el siguiente comando:

```
virsh
```

Para obtener ayuda para un comando virsh específico, escriba el siguiente comando:

```
virsh help {command}
```

Para enumerar todas las máquinas virtuales disponibles, escriba el siguiente comando:

```
virsh list
```

Para obtener información sobre una máquina virtual específica, escriba el siguiente comando:

```
virsh dominfo {domain}
```

Para iniciar una máquina virtual, escriba el siguiente comando:

```
virsh start {domain}
```

Para apagar una máquina virtual, escriba el siguiente comando:

```
virsh shutdown {domain}
```

Para destruir una máquina virtual, escriba el siguiente comando:

```
virsh destroy {domain}
```

Para suspender una máquina virtual, escriba el siguiente comando:

```
virsh suspend {domain}
```

Para reanudar una máquina virtual, escriba el siguiente comando:

```
virsh resume {domain}
```

Para conectarse a una máquina virtual, escriba el siguiente comando:

```
virsh console {domain}
```

## Gestión del almacenamiento con virt-manager

Además de administrar máquinas virtuales, la herramienta virt-manager también se puede usar para administrar el almacenamiento. Para iniciar el administrador de almacenamiento, escriba el siguiente comando:

```
virt-manager --storage
```

Verá la ventana Almacenamiento de virt-manager que se muestra en la Figura 4.


Figura 4. La ventana de almacenamiento de virt-manager

Para crear un nuevo grupo de almacenamiento, haga clic en el menú Archivo y seleccione Nuevo grupo de almacenamiento. Verá la ventana Nuevo grupo de almacenamiento que se muestra en la Figura 5.


Figura 5. La ventana Nuevo grupo de almacenamiento

En la primera página del asistente, seleccione el tipo de grupo de almacenamiento que desea crear y haga clic en Adelante. En la página siguiente, seleccione el origen del grupo de almacenamiento y haga clic en Reenviar. En la página siguiente, seleccione el destino del grupo de almacenamiento y haga clic en Reenviar.

En la página siguiente, verá una lista de dispositivos de almacenamiento disponibles. Seleccione los dispositivos de almacenamiento que desea usar y haga clic en Reenviar. En la página siguiente, verá una lista de formatos de almacenamiento disponibles. Seleccione el formato de almacenamiento que desea usar y haga clic en Reenviar.

En la página siguiente, verá una lista de las estrategias de asignación disponibles. Seleccione la estrategia de asignación que desee utilizar y haga clic en Reenviar. En la página siguiente, verá una lista de los modos de caché disponibles. Seleccione el modo de caché que desea usar y haga clic en Adelante.

En la página siguiente, verá una lista de programadores de E/S disponibles. Seleccione el programador de E/S que desee utilizar y haga clic en Adelante. En la página siguiente, verá una lista de tamaños de bloque disponibles. Seleccione el tamaño de bloque que desea usar y haga clic en Adelante.

En la página final, revise sus selecciones y haga clic en Finalizar. La herramienta virt-manager ahora creará su grupo de almacenamiento.

## Conclusión

En este artículo, hemos cubierto los conceptos básicos de la virtualización de Linux con KVM y libvirt. Hemos visto cómo instalar KVM y libvirt, cómo crear y administrar máquinas virtuales y cómo administrar el almacenamiento.

Con este conocimiento, debería poder comenzar a usar KVM y libvirt para virtualizar su propio entorno Linux.