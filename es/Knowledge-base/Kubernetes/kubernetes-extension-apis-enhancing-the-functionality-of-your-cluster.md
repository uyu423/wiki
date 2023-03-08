---
title: API de extensión de Kubernetes: mejora de la funcionalidad de su clúster
description: 
published: true
date: 2023-02-14T01:33:40.808Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:33:39.403Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Extension APIs: Enhancing the Functionality of Your Cluster***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-extension-apis-enhancing-the-functionality-of-your-cluster)
{.links-list}


# API de extensión de Kubernetes: mejora de la funcionalidad de su clúster

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores. Agrupa los contenedores que componen una aplicación en unidades lógicas para facilitar la gestión y el descubrimiento. Kubernetes está disponible en las principales nubes públicas y privadas, incluidos Amazon Web Services (AWS), Google Cloud Platform (GCP), Azure y más.

Las API de extensión de Kubernetes son un conjunto de API que permiten a los desarrolladores ampliar la funcionalidad de Kubernetes. Estas API se pueden usar para crear nuevos recursos, agregar nuevos controladores y modificar el comportamiento de los recursos existentes.

La API de extensión de Kubernetes se basa en la especificación OpenAPI. La especificación OpenAPI es una descripción de interfaz estándar e independiente del idioma para las API REST. La API de extensión de Kubernetes permite a los desarrolladores utilizar cualquier cliente compatible con OpenAPI para interactuar con Kubernetes.

La API de extensión de Kubernetes se divide en tres grupos:

* El grupo de API principal, que contiene las API necesarias para todos los componentes de Kubernetes.
* El grupo de API de aplicaciones, que contiene las API necesarias para las aplicaciones de Kubernetes.
* El grupo de API de extensiones, que contiene las API necesarias para las extensiones de Kubernetes.

El grupo de API principal contiene las API necesarias para todos los componentes de Kubernetes. El grupo principal de API se divide en dos subgrupos:

* El grupo de API de metadatos, que contiene las API necesarias para recuperar y manipular metadatos de recursos de Kubernetes.
* El grupo de API de tiempo de ejecución, que contiene las API necesarias para los componentes de tiempo de ejecución de Kubernetes.

El grupo de API de aplicaciones contiene las API necesarias para las aplicaciones de Kubernetes. El grupo de API de aplicaciones se divide en dos subgrupos:

* El grupo de API de aplicaciones, que contiene las API necesarias para los componentes de aplicaciones de Kubernetes.
* El grupo de API de extensión, que contiene las API necesarias para los componentes de extensión de Kubernetes.

El grupo de API de extensiones contiene las API necesarias para las extensiones de Kubernetes. El grupo API de extensiones se divide en dos subgrupos:

* El grupo de API de configuración, que contiene las API necesarias para la configuración de la extensión de Kubernetes.
* El grupo de API de estado, que contiene las API necesarias para el estado de la extensión de Kubernetes.

## Grupo de API principal

El grupo de API principal contiene las API necesarias para todos los componentes de Kubernetes. El grupo principal de API se divide en dos subgrupos:

* El grupo de API de metadatos, que contiene las API necesarias para recuperar y manipular metadatos de recursos de Kubernetes.
* El grupo de API de tiempo de ejecución, que contiene las API necesarias para los componentes de tiempo de ejecución de Kubernetes.

### Grupo de API de metadatos

El grupo de API de metadatos contiene las API necesarias para recuperar y manipular metadatos de recursos de Kubernetes. El grupo de API de metadatos se divide en cuatro subgrupos:

* El grupo de API de objetos, que contiene las API necesarias para manipular objetos de Kubernetes.
* El grupo de API de lista, que contiene las API necesarias para manipular las listas de Kubernetes.
* El grupo de API de espacios de nombres, que contiene las API necesarias para manipular los espacios de nombres de Kubernetes.
* El grupo de API secretas, que contiene las API necesarias para manipular los secretos de Kubernetes.

#### Grupo de API de objetos

El grupo de API de objetos contiene las API necesarias para manipular objetos de Kubernetes. El grupo de API de objetos se divide en cuatro subgrupos:

* El grupo de API de parches, que contiene las API necesarias para parchear objetos de Kubernetes.
* El grupo de eliminación de API, que contiene las API necesarias para eliminar objetos de Kubernetes.
* El grupo get API, que contiene las API necesarias para recuperar objetos de Kubernetes.
* El grupo de creación de API, que contiene las API necesarias para crear objetos de Kubernetes.

##### Grupo de API de parches

El grupo de API de parches contiene las API necesarias para aplicar parches a los objetos de Kubernetes. El grupo de API de parches se divide en dos subgrupos:

* El grupo de API estratégicas, que contiene las API necesarias para parchear objetos de Kubernetes mediante el parche de combinación estratégica.
* El grupo de API json, que contiene las API necesarias para parchear objetos de Kubernetes mediante el parche JSON.

###### Grupo estratégico de API

El grupo de API estratégicas contiene las API que se requieren para aplicar parches a los objetos de Kubernetes mediante el parche de combinación estratégica. El grupo estratégico de API se divide en dos subgrupos:

* El grupo de API de aplicación, que contiene las API necesarias para aplicar el parche de combinación estratégica a los objetos de Kubernetes.
* El grupo de API de parches, que contiene las API necesarias para parchear objetos de Kubernetes mediante el parche de combinación estratégica.

###### # Aplicar grupo de API

El grupo de API de aplicación contiene las API necesarias para aplicar el parche de combinación estratégica a los objetos de Kubernetes. El grupo de API de aplicación se divide en dos subgrupos:

* La API de aplicación, que aplica el parche de combinación estratégica al objeto de Kubernetes especificado.
* La API de parches, que parchea el objeto de Kubernetes especificado mediante el parche de combinación estratégica.

###### Grupo de API JSON

El grupo de API de JSON contiene las API necesarias para parchear objetos de Kubernetes mediante el parche de JSON. El grupo de API JSON se divide en dos subgrupos:

* El grupo de API de aplicación, que contiene las API necesarias para aplicar el parche JSON a los objetos de Kubernetes.
* El grupo de API de parches, que contiene las API necesarias para parchear objetos de Kubernetes mediante el parche JSON.

###### # Aplicar grupo de API

El grupo de API de aplicación contiene las API necesarias para aplicar el parche JSON a los objetos de Kubernetes. El grupo de API de aplicación se divide en dos subgrupos:

* La API de aplicación, que aplica el parche JSON al objeto de Kubernetes especificado.
* La API de parches, que parchea el objeto de Kubernetes especificado mediante el parche JSON.

#### Eliminar grupo de API

El grupo de eliminación de API contiene las API necesarias para eliminar objetos de Kubernetes. El grupo de eliminación de API se divide en dos subgrupos:

* La API de eliminación, que elimina el objeto de Kubernetes especificado.
* La API gracePeriod, que establece el período de gracia para eliminar el objeto de Kubernetes especificado.

#### Obtener grupo de API

El grupo obtener API contiene las API necesarias para recuperar objetos de Kubernetes. El grupo get API se divide en dos subgrupos:

* La API de lista, que enumera los objetos de Kubernetes en el espacio de nombres especificado.
* La API de vigilancia, que vigila los objetos de Kubernetes en el espacio de nombres especificado.

#### Crear grupo de API

El grupo de creación de API contiene las API necesarias para crear objetos de Kubernetes. El grupo de creación de API se divide en dos subgrupos:

* La API de creación, que crea el objeto de Kubernetes especificado.
* La API de creación de instancias, que crea una instancia del objeto de Kubernetes especificado.

### Grupo de API de tiempo de ejecución

El grupo de API de tiempo de ejecución contiene las API necesarias para los componentes de tiempo de ejecución de Kubernetes. El grupo de API de tiempo de ejecución se divide en cuatro subgrupos:

* El grupo de API de contenedor, que contiene las API necesarias para manipular contenedores de Kubernetes.
* El grupo de API de pod, que contiene las API necesarias para manipular los pods de Kubernetes.
* El grupo de API de servicio, que contiene las API necesarias para manipular los servicios de Kubernetes.
* El grupo de API de volumen, que contiene las API necesarias para manipular volúmenes de Kubernetes.

#### Grupo de API de contenedores

El grupo de API de contenedor contiene las API necesarias para manipular contenedores de Kubernetes. El grupo de API de contenedores se divide en dos subgrupos:

* El grupo de API exec, que contiene las API necesarias para ejecutar comandos en contenedores de Kubernetes.
* El grupo de API portForward, que contiene las API necesarias para reenviar puertos a contenedores de Kubernetes.

##### Grupo de API ejecutivo

El grupo de API exec contiene las API necesarias para ejecutar comandos en contenedores de Kubernetes. El grupo API exec se divide en dos subgrupos:

* La API exec, que ejecuta el comando especificado en el contenedor de Kubernetes especificado.
* La API de conexión, que se adjunta al contenedor de Kubernetes especificado.

###### API ejecutiva

La API exec ejecuta el comando especificado en el contenedor de Kubernetes especificado. La API exec se divide en dos subgrupos:

* La API exec, que ejecuta el comando especificado en el contenedor de Kubernetes especificado.
* La API de conexión, que se adjunta al contenedor de Kubernetes especificado.

###### Adjuntar API

La API de conexión se conecta al contenedor de Kubernetes especificado. La API de conexión se divide en dos subgrupos:

* La API exec, que ejecuta el comando especificado en el contenedor de Kubernetes especificado.
* La API de conexión, que se adjunta al contenedor de Kubernetes especificado.

##### Grupo de API PortForward

El grupo de API portForward contiene las API necesarias para reenviar puertos a contenedores de Kubernetes. El grupo de la API portForward se divide en dos subgrupos:

* La API portForward, que reenvía el puerto especificado al contenedor de Kubernetes especificado.
* La API streamPortForward, que transmite el puerto especificado al contenedor de Kubernetes especificado.

###### API de reenvío de puertos

La API portForward reenvía el puerto especificado al contenedor de Kubernetes especificado. La API portForward se divide en dos subgrupos:

* La API portForward, que reenvía el puerto especificado al contenedor de Kubernetes especificado.
* La API streamPortForward, que transmite el puerto especificado al contenedor de Kubernetes especificado.

###### API de StreamPortForward

La API streamPortForward transmite el puerto especificado al contenedor de Kubernetes especificado. La API streamPortForward se divide en dos subgrupos:

* La API portForward, que reenvía el puerto especificado al contenedor de Kubernetes especificado.
* La API streamPortForward, que transmite el puerto especificado al contenedor de Kubernetes especificado.

#### Grupo de API de pod

El grupo de API de pod contiene las API necesarias para manipular los pods de Kubernetes. El grupo de API de pod se divide en dos subgrupos:

* El grupo de API de vinculación, que contiene las API necesarias para manipular las vinculaciones de pods de Kubernetes.
* El grupo de API de registro, que contiene las API necesarias para recuperar los registros del pod de Kubernetes.

##### Grupo de API de vinculación

El grupo de API de vinculación contiene las API necesarias para manipular las vinculaciones de pods de Kubernetes. El grupo de API de enlace se divide en dos subgrupos:

* La API de vinculación, que vincula el pod especificado al nodo especificado.
* La API de desvinculación, que desvincula el pod especificado del nodo especificado.

###### API de vinculación

La API de vinculación vincula el pod especificado al nodo especificado. La API de vinculación se divide en dos subgrupos:

* La API de vinculación, que vincula el pod especificado al nodo especificado.
* La API de desvinculación, que desvincula el pod especificado del nodo especificado.

###### Desvincular API

La API de desvinculación desvincula el pod especificado del nodo especificado. La API de desvinculación se divide en dos subgrupos:

* La API de vinculación, que vincula el pod especificado al nodo especificado.
* La API de desvinculación, que desvincula el pod especificado del nodo especificado.

##### Grupo de API de registro

El grupo de API de registro contiene las API necesarias para recuperar los registros del pod de Kubernetes. El grupo de API de registro se divide en dos subgrupos:

* La API get, que obtiene los registros del pod especificado.
* La API de seguimiento, que sigue los registros del pod especificado.

###### Obtener API

La API get obtiene los registros del pod especificado. La API get se divide en dos subgrupos:

* La API get, que obtiene los registros del pod especificado.
* La API de seguimiento, que sigue los registros del pod especificado.

###### Seguir API

La API de seguimiento sigue los registros del pod especificado. La siguiente API se divide en dos subgrupos:

* La API get, que obtiene los registros del pod especificado.
* La API de seguimiento, que sigue los registros del pod especificado.

#### Grupo de API de servicio

El grupo de API de servicio contiene las API necesarias para manipular los servicios de Kubernetes. El grupo de API de servicio se divide en tres subgrupos:

* El grupo de API de proxy, que contiene las API necesarias para manipular los proxies de servicio de Kubernetes.
* El grupo de API de puntos finales, que contiene las API necesarias para manipular los puntos finales del servicio de Kubernetes.
* El grupo de API de nodos, que contiene las API necesarias para manipular los nodos de servicio de Kubernetes.

##### Grupo de API de proxy

El grupo de API de proxy contiene las API necesarias para manipular los proxies de servicio de Kubernetes. El grupo de API de proxy se divide en dos subgrupos:

* La API get, que obtiene el proxy para el servicio especificado.
* La API de actualización, que actualiza el proxy para el servicio especificado.

###### Obtener API

La API get obtiene el proxy para el servicio especificado. La API get se divide en dos subgrupos:

* La API get, que obtiene el proxy para el servicio especificado.
* La API de actualización, que actualiza el proxy para el servicio especificado.

###### API de actualización

La API de actualización actualiza el proxy para el servicio especificado. La API de actualización se divide en dos subgrupos:

* La API get, que obtiene el proxy para el servicio especificado.
* La API de actualización, que actualiza el proxy para el servicio especificado.

##### Grupo de API de punto final

El grupo de API de puntos finales contiene las API necesarias para manipular los puntos finales del servicio de Kubernetes. El grupo de API de punto final se divide en dos subgrupos:

* La API get, que obtiene los puntos finales para el servicio especificado.
* La API de actualización, que actualiza los puntos finales para el servicio especificado.

###### Obtener API

La API de obtención obtiene los puntos finales para el servicio especificado. La API get se divide en dos subgrupos:

* La API get, que obtiene los puntos finales para el servicio especificado.
* La API de actualización, que actualiza los puntos finales para el servicio especificado.

###### API de actualización

La API de actualización actualiza los puntos finales para el servicio especificado. La API de actualización se divide en dos subgrupos:

* La API get, que obtiene los puntos finales para el servicio especificado.
* La API de actualización, que actualiza los puntos finales para el servicio especificado.

##### Grupo de API de nodo

El grupo de API de nodos contiene las API necesarias para manipular los nodos de servicio de Kubernetes. El grupo de API de nodos se divide en dos subgrupos:

* La API get, que obtiene los nodos para el servicio especificado.
* La API de actualización, que actualiza los nodos para el servicio especificado.

###### Obtener API

La API get obtiene los nodos para el servicio especificado. La API get se divide en dos subgrupos:

* La API get, que obtiene los nodos para el servicio especificado.
* La API de actualización, que actualiza los nodos para el servicio especificado.

###### API de actualización

La API de actualización actualiza los nodos para el servicio especificado. La API de actualización se divide en dos subgrupos:

* La API get, que obtiene los nodos para el servicio especificado.
* La API de actualización, que actualiza los nodos para el servicio especificado.

#### Grupo de API de volumen

El grupo de API de volumen contiene las API necesarias para manipular volúmenes de Kubernetes. El grupo API de volumen se divide en dos subgrupos:

* El grupo de API adjuntas, que contiene las API necesarias para adjuntar volúmenes de Kubernetes.
* El grupo de API de separación, que contiene las API necesarias para separar volúmenes de Kubernetes.

##### Adjuntar grupo de API

El grupo de API adjuntas contiene las API necesarias para adjuntar volúmenes de Kubernetes. El grupo de API de conexión se divide en dos subgrupos:

* La API de conexión, que adjunta el volumen especificado al nodo especificado.
* La API de lista, que enumera los volúmenes que se adjuntan al nodo especificado.

###### Adjuntar API

La API de conexión adjunta el volumen especificado al nodo especificado. La API de conexión se divide en dos subgrupos:

* La API de conexión, que adjunta el volumen especificado al nodo especificado.
* La API de lista, que enumera los volúmenes que se adjuntan al nodo especificado.

###### API de lista

La API de lista enumera los volúmenes que están adjuntos al nodo especificado. La lista API se divide en dos subgrupos:

* La API de conexión, que adjunta el volumen especificado al nodo especificado.
* La API de lista, que enumera los volúmenes que se adjuntan al nodo especificado.

##### Desvincular grupo de API
