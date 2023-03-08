---
title: Kubernetes con gVisor: mejora de la seguridad de los contenedores con un tiempo de ejecución en espacio aislado
description: 
published: true
date: 2023-02-14T11:33:10.643Z
tags: 
editor: markdown
dateCreated: 2023-02-14T11:33:08.990Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with gVisor: Enhancing Container Security with a Sandboxed Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}


# Kubernetes con gVisor: mejora de la seguridad de los contenedores con un entorno de ejecución aislado

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores. gVisor es un espacio aislado de tiempo de ejecución que utiliza características del núcleo para aislar procesos y mejorar la seguridad.

## ¿Qué es gVisor?

gVisor es un espacio aislado de tiempo de ejecución que utiliza características del núcleo para aislar procesos y mejorar la seguridad. Está diseñado para ejecutar código no confiable en un entorno seguro. Google Cloud Platform utiliza gVisor y está disponible como código abierto.

gVisor es un programa de espacio de usuario que se ejecuta sobre el kernel de Linux. Proporciona una vista limitada del sistema operativo y los recursos subyacentes. Esto limita la cantidad de daño que puede causar un programa malicioso o con errores.

gVisor no es una máquina virtual completa. No proporciona su propio kernel o controladores de dispositivo. En su lugar, utiliza el núcleo y los controladores del sistema operativo subyacente. Esto hace que gVisor sea más liviano y más fácil de usar que una máquina virtual completa.

## ¿Cómo funciona gVisor?

gVisor utiliza funciones del kernel de Linux para aislar procesos. Estas funciones incluyen espacios de nombres, cgroups y seccomp-bpf.

Los espacios de nombres proporcionan aislamiento entre procesos. Permiten que los procesos tengan su propia vista del sistema, incluido su propio sistema de archivos y red.

Los Cgroups limitan los recursos que puede utilizar un proceso. Se pueden usar para limitar la cantidad de CPU, memoria y espacio en disco que puede usar un proceso.

Seccomp-bpf es una función de seguridad que permite aislar los procesos. Filtra las llamadas del sistema y bloquea las peligrosas.

## ¿Cómo usa Kubernetes gVisor?

Kubernetes usa gVisor para mejorar la seguridad de los contenedores. De forma predeterminada, los contenedores comparten el mismo kernel que el sistema operativo host. Esto puede ser un riesgo de seguridad porque un contenedor malicioso puede acceder al sistema operativo del host.

gVisor proporciona un tiempo de ejecución de espacio aislado para contenedores. Esto aísla los contenedores del sistema operativo host y mejora la seguridad.

## ¿Cómo uso Kubernetes con gVisor?

Puede usar Kubernetes con gVisor agregando el indicador `--runtime=runsc` al comando `kubelet`. Esto usará gVisor como tiempo de ejecución para contenedores.

También puede usar Kubernetes con gVisor agregando el indicador `--runtime-provider=runsc` al comando `kubelet`. Esto usará gVisor como proveedor de tiempo de ejecución para contenedores.

## ¿Cómo instalo Kubernetes con gVisor?

Puede instalar Kubernetes con gVisor usando un administrador de paquetes como `apt` o `yum`.

```
apt install kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum install kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## ¿Cómo actualizo Kubernetes con gVisor?

Puede actualizar Kubernetes con gVisor usando un administrador de paquetes como `apt` o `yum`.

```
apt upgrade kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum upgrade kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## ¿Cómo configuro Kubernetes con gVisor?

Puede configurar Kubernetes con gVisor agregando el indicador `--runtime=runsc` al comando `kubelet`. Esto usará gVisor como tiempo de ejecución para contenedores.

También puede usar Kubernetes con gVisor agregando el indicador `--runtime-provider=runsc` al comando `kubelet`. Esto usará gVisor como proveedor de tiempo de ejecución para contenedores.

## ¿Cómo desinstalo Kubernetes con gVisor?

Puede desinstalar Kubernetes con gVisor usando un administrador de paquetes como `apt` o `yum`.

```
apt remove kubelet runc
```

```
yum remove kubelet runc
```

## Conclusión

Kubernetes con gVisor es una forma segura de ejecutar contenedores. gVisor proporciona un tiempo de ejecución de espacio aislado para contenedores. Esto aísla los contenedores del sistema operativo host y mejora la seguridad.