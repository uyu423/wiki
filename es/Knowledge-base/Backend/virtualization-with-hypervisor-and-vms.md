---
title: Virtualización con Hypervisor y VMs
description: 
published: true
date: 2023-02-08T14:17:34.480Z
tags: 
editor: markdown
dateCreated: 2023-02-08T14:17:32.875Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Virtualization with Hypervisor and VMs***English** document is available*](/en/Knowledge-base/Backend/virtualization-with-hypervisor-and-vms)
{.links-list}


# Virtualización con Hypervisor y VMs

Con la demanda cada vez mayor de potencia informática, junto con la tendencia a la miniaturización en la industria del hardware, no sorprende que la virtualización se haya convertido en un tema tan popular en los últimos años. La virtualización permite la creación de máquinas virtuales (VM) que pueden ejecutarse en una máquina física, compartiendo los recursos de hardware subyacentes.

Hay dos tipos principales de virtualización:

1. **Virtualización completa**: el sistema operativo invitado tiene acceso completo a los recursos de hardware subyacentes. Esto permite que los sistemas operativos invitados no modificados se ejecuten en el host.

2. **Paravirtualización**: el sistema operativo invitado no tiene acceso completo a los recursos de hardware subyacentes. En su lugar, recibe una versión modificada del hardware que está optimizada para ejecutarse en un entorno virtual.

También hay dos tipos principales de plataformas de virtualización:

1. **Bare metal**: el hipervisor se instala directamente en la máquina física. Esto proporciona el mejor rendimiento pero requiere hardware dedicado.

2. **Alojado**: el hipervisor se instala sobre un sistema operativo host. Esto requiere menos recursos, pero puede resultar en una disminución del rendimiento.

## Configuración de una máquina virtual

Hay algunas cosas que necesitará para configurar una máquina virtual:

1. Una máquina física con suficientes recursos para admitir la máquina virtual.

2. Un hipervisor. Esto puede ser completo o alojado.

3. Un sistema operativo invitado. Esto puede ser virtualización completa o paravirtualización.

4. Software de máquina virtual. Esto le permitirá crear y administrar sus máquinas virtuales.

Una vez que tenga todas estas cosas, puede comenzar a configurar su máquina virtual. Lo primero que deberá hacer es crear un disco virtual. Esto se usará para almacenar el sistema operativo invitado y cualquier dato que desee conservar en la máquina virtual.

Una vez que tenga un disco virtual, puede instalar el sistema operativo invitado en él. Si está utilizando la virtualización completa, puede instalar el sistema operativo como lo haría en una máquina física. Si usa paravirtualización, deberá usar una versión modificada del sistema operativo que esté optimizada para entornos virtuales.

Una vez que el sistema operativo está instalado, puede comenzar a configurar la máquina virtual. Esto incluirá cosas como la configuración de redes, la instalación de aplicaciones, etc.

## Ejecutando una Máquina Virtual

Una vez que haya configurado una máquina virtual, puede comenzar a usarla. Para hacer esto, deberá iniciar la máquina virtual. Esto se puede hacer desde el hipervisor o desde el sistema operativo invitado.

Si está arrancando desde el hipervisor, deberá seleccionar la VM que desea arrancar y luego seleccionar la opción "arranque". Esto iniciará la máquina virtual y lo llevará al sistema operativo invitado.

Si está arrancando desde el sistema operativo invitado, deberá seleccionar la opción de "arranque" desde el sistema operativo. Esto iniciará la máquina virtual y lo llevará al sistema operativo invitado.

Una vez que se inicia la VM, puede usarla como lo haría con cualquier otra computadora. Puede instalar aplicaciones, navegar por Internet, etc.

## Apagar una máquina virtual

Cuando haya terminado de usar una máquina virtual, deberá apagarla. Esto se puede hacer desde el hipervisor o desde el sistema operativo invitado.

Si está cerrando desde el hipervisor, deberá seleccionar la VM que desea apagar y luego seleccionar la opción "apagar". Esto apagará la máquina virtual y lo llevará de vuelta al hipervisor.

Si está cerrando desde el sistema operativo invitado, deberá seleccionar la opción "apagar" desde el sistema operativo. Esto apagará la máquina virtual y lo llevará de vuelta al hipervisor.

Una vez que se apaga la máquina virtual, puede apagar la máquina o dejarla en funcionamiento. Si apaga la máquina, la máquina virtual se apagará y no podrá utilizarse hasta que vuelva a encender la máquina. Si deja la máquina en funcionamiento, la VM se apagará pero permanecerá disponible para su uso.

## Conclusión

La virtualización es una excelente manera de aumentar la potencia informática de una máquina física. Permite la creación de máquinas virtuales que pueden compartir los recursos de hardware subyacentes. Hay dos tipos principales de virtualización: virtualización completa y paravirtualización. También hay dos tipos principales de plataformas de virtualización: bare metal y alojadas.

Para configurar una máquina virtual, necesitará una máquina física con suficientes recursos para admitir la máquina virtual, un hipervisor, un sistema operativo invitado y software de máquina virtual. Una vez que tenga todas estas cosas, puede comenzar a configurar su VM.

Una vez que su VM esté configurada, puede comenzar a usarla. Para hacer esto, deberá iniciar la máquina virtual. Esto se puede hacer desde el hipervisor o desde el sistema operativo invitado. Una vez que se inicia la VM, puede usarla como lo haría con cualquier otra computadora.

Cuando haya terminado de usar una máquina virtual, deberá apagarla. Esto se puede hacer desde el hipervisor o desde el sistema operativo invitado. Una vez que se apaga la máquina virtual, puede apagar la máquina o dejarla en funcionamiento.