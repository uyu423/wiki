---
title: Kubernetes con CNI: configuración de redes para sus clústeres
description: 
published: true
date: 2023-02-05T14:17:33.180Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:17:26.761Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with CNI: Configuring Networking for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}


# Kubernetes con CNI: configuración de redes para sus clústeres

Kubernetes es un potente sistema de gestión de contenedores que permite a los desarrolladores implementar y gestionar aplicaciones escalables en un entorno nativo de la nube. Para ejecutar clústeres de Kubernetes, los desarrolladores deben configurar las redes para sus aplicaciones. Esto se puede hacer usando la Interfaz de red de contenedores (CNI).

CNI es una biblioteca que proporciona API para simplificar la configuración de interfaces de red para contenedores. Está diseñado para usarse con tiempos de ejecución de contenedores, como Kubernetes, para proporcionar una experiencia de configuración de red coherente para los desarrolladores. CNI proporciona una solución de configuración de red portátil y extensible que se puede usar con cualquier tiempo de ejecución de contenedor.

En este artículo, le mostraremos cómo configurar redes para clústeres de Kubernetes mediante CNI. Cubriremos los siguientes temas:

- ¿Qué es CNI?
- ¿Cómo funciona el CNI?
- ¿Cómo configurar la red para Kubernetes usando CNI?

## ¿Qué es CNI?

CNI es una biblioteca que proporciona API para simplificar la configuración de interfaces de red para contenedores. Está diseñado para usarse con tiempos de ejecución de contenedores, como Kubernetes, para proporcionar una experiencia de configuración de red coherente para los desarrolladores. CNI proporciona una solución de configuración de red portátil y extensible que se puede usar con cualquier tiempo de ejecución de contenedor.

## ¿Cómo funciona CNI?

CNI funciona creando un espacio de nombres de red para cada contenedor. Un espacio de nombres de red es un entorno virtual que contiene su propia configuración de red. Esto permite que cada contenedor tenga su propia dirección IP y configuración de red. Luego, CNI usa complementos para configurar las interfaces de red para cada contenedor.

Hay dos tipos de complementos CNI:

- Complementos de **red**: estos complementos configuran la interfaz de red para un contenedor.
- Complementos **IPAM**: estos complementos asignan direcciones IP para contenedores.

## ¿Cómo configurar la red para Kubernetes usando CNI?

Kubernetes usa CNI para configurar redes para contenedores. Para usar CNI con Kubernetes, debe instalar un complemento de CNI. Hay muchos complementos de CNI disponibles, como flannel, Weave Net y Calico.

En esta sección, le mostraremos cómo instalar y configurar el complemento Flannel CNI.

### Instalación del complemento CNI de franela

El complemento flannel CNI está disponible en el repositorio CNI GitHub. Para instalar el complemento, debe descargar el binario y colocarlo en `$PATH`.

```
$ wget https://github.com/containernetworking/cni/releases/download/v0.6.0/cni-amd64-v0.6.0.tgz
$ tar -xvzf cni-amd64-v0.6.0.tgz -C /usr/local/bin/
```

### Configuración del complemento CNI de franela

Una vez que se instala el complemento CNI de franela, debe configurarlo. El complemento Flannel CNI utiliza un archivo de configuración para configurar la red. El archivo de configuración está en formato JSON y contiene los siguientes campos:

- `name`: El nombre de la red.
- `tipo`: El tipo de la red. El complemento flannel CNI es compatible con el tipo `flannel`.
- `delegate`: El complemento CNI de delegado a usar. El complemento flannel CNI utiliza el delegado `puente` de forma predeterminada.
- `puente`: El nombre del puente a utilizar. El complemento flannel CNI crea un puente con el nombre `cni0` por defecto.
- `isGateway`: Especifica si el puente es la puerta de enlace para la red. El complemento CNI de franela establece esto en "verdadero" de forma predeterminada.
- `ipMasq`: Especifica si habilitar el enmascaramiento de IP. El complemento CNI de franela establece esto en "verdadero" de forma predeterminada.
- `mtu`: La MTU de la red. El complemento Flannel CNI establece esto en `1500` de forma predeterminada.
- `hairpinMode`: Especifica si habilitar el modo de horquilla. El complemento CNI de franela establece esto en "verdadero" de forma predeterminada.

Aquí hay un ejemplo de configuración del complemento CNI de franela:

```json
{
    "name": "my-network",
    "type": "flannel",
    "delegate": {
        "bridge": "cni0"
    },
    "isGateway": true,
    "ipMasq": true,
    "mtu": 1500,
    "hairpinMode": true
}
```

Guarde el archivo de configuración como `my-network.json` y colóquelo en el directorio `/etc/cni/net.d/`.

### Creando la red CNI de franela

Una vez que el complemento Flannel CNI está instalado y configurado, puede crear la red usando el comando `cni-add`. El comando `cni-add` toma la ruta al archivo de configuración como argumento.

```
$ sudo cni-add my-network.json
```

Esto creará una red con el nombre `my-network`. La red se configurará utilizando los ajustes del archivo `my-network.json`.

### Eliminación de la red CNI de franela

Para eliminar la red CNI de franela, puede usar el comando `cni-del`. El comando `cni-del` toma la ruta al archivo de configuración como argumento.

```
$ sudo cni-del my-network.json
```

Esto eliminará la red con el nombre `my-network`.

## Conclusión

En este artículo, le mostramos cómo configurar redes para clústeres de Kubernetes mediante CNI. Cubrimos los siguientes temas:

- ¿Qué es CNI?
- ¿Cómo funciona el CNI?
- ¿Cómo configurar la red para Kubernetes usando CNI?

Si tiene alguna pregunta sobre la configuración de redes para Kubernetes, deje un comentario a continuación.