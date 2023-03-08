---
title: Kubernetes en nubes privadas: implementación de clústeres en su propia infraestructura
description: 
published: true
date: 2023-02-14T07:32:42.071Z
tags: 
editor: markdown
dateCreated: 2023-02-14T07:32:40.468Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes on Private Clouds: Deploying Clusters on Your Own Infrastructure***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-private-clouds-deploying-clusters-on-your-own-infrastructure)
{.links-list}


# Kubernetes en nubes privadas: implementación de clústeres en su propia infraestructura

Kubernetes es una herramienta de orquestación de contenedores de código abierto que ha ganado popularidad en los últimos años por su capacidad para automatizar la implementación, el escalado y la administración de aplicaciones en contenedores.

Si bien Kubernetes se puede implementar en nubes públicas como Amazon Web Services (AWS), Google Cloud Platform (GCP) y Microsoft Azure, muchas organizaciones prefieren ejecutar Kubernetes en su propia infraestructura privada por razones de seguridad, costo o soberanía de datos.

Este artículo proporcionará una descripción general de la herramienta de orquestación de contenedores de Kubernetes y le mostrará cómo implementar un clúster de Kubernetes en su propia infraestructura, ya sea en las instalaciones o en una nube privada.

## ¿Qué es Kubernetes?

Kubernetes es una plataforma portátil, extensible y de código abierto para administrar cargas de trabajo y servicios en contenedores, que facilita tanto la configuración declarativa como la automatización. Tiene un gran ecosistema de rápido crecimiento. Los servicios, el soporte y las herramientas de Kubernetes están ampliamente disponibles.

Kubernetes fue diseñado originalmente por Google y ahora es mantenido por Cloud Native Computing Foundation.

## Características de Kubernetes

Algunas de las características clave de Kubernetes incluyen:

- Implementación y escalado automatizados de aplicaciones en contenedores
- Equilibrio de carga y descubrimiento de servicios
- Orquestación de almacenamiento
- Autosanación
- Gestión de secretos y configuraciones.

## Beneficios de Kubernetes

El uso de Kubernetes ofrece muchos beneficios, entre ellos:

-Mayor eficiencia: al automatizar la implementación, el escalado y la administración de aplicaciones en contenedores, Kubernetes puede ayudarlo a aumentar la eficiencia de sus equipos de desarrollo y operaciones.
-Tiempo de actividad mejorado: las capacidades de recuperación automática de Kubernetes pueden ayudarlo a mejorar el tiempo de actividad de sus aplicaciones al reiniciar automáticamente los contenedores bloqueados y replicar los contenedores fallidos.
-Mayor agilidad: la automatización y la configuración declarativa de Kubernetes pueden ayudarlo a aumentar la agilidad de su proceso de desarrollo al permitirle implementar y actualizar aplicaciones rápidamente.
-Costos operativos reducidos: al automatizar la gestión de aplicaciones en contenedores, Kubernetes puede ayudarlo a reducir los costos operativos de su infraestructura.

## Arquitectura de Kubernetes

Kubernetes es un sistema complejo con una variedad de componentes. La siguiente es una descripción general de alto nivel de la arquitectura de Kubernetes:

- El Master Node es el corazón del clúster de Kubernetes. Es responsable de administrar el clúster y mantener un registro del estado del clúster. El Master Node está compuesto por los siguientes componentes:
  - El servidor API es el punto central de comunicación para el clúster de Kubernetes. Es responsable de exponer la API de Kubernetes y procesar las solicitudes de la API.
  - El Programador es responsable de programar los pods para que se ejecuten en los nodos del clúster.
  - El Controller Manager es responsable de administrar el estado del clúster.
- Los Worker Nodes son los nodos del clúster de Kubernetes donde se implementan realmente los pods. Cada pod en el clúster se implementa en un nodo de trabajo.

## Componentes de Kubernetes

Kubernetes se compone de una serie de componentes, cada uno de los cuales desempeña un papel específico en el funcionamiento del clúster de Kubernetes. La siguiente es una breve descripción general de los componentes de Kubernetes:

- El servidor API es el punto central de comunicación para el clúster de Kubernetes. Es responsable de exponer la API de Kubernetes y procesar las solicitudes de la API.
- El Programador es responsable de programar los pods para que se ejecuten en los nodos del clúster.
- El Controller Manager es responsable de administrar el estado del clúster.
- El componente Etcd se encarga de almacenar los datos de configuración del clúster de Kubernetes.
- Kubelet es responsable de ejecutar pods en los nodos del clúster de Kubernetes.
- Kube-Proxy es responsable de enrutar el tráfico al pod correcto en el clúster de Kubernetes.

## Implementación de Kubernetes en su propia infraestructura

Hay varias formas de implementar Kubernetes en su propia infraestructura. Los siguientes son algunos de los métodos más populares:

- Utilice una solución específica de Kubernetes, como MicroK8s de Canonical, Red Hat OpenShift o VMware Tanzu Kubernetes Grid Integrated Edition (TKGI).
- Use una solución independiente de la nube, como Hashicorp Terraform, Puppet o Ansible.
- Use una solución específica de la nube, como Amazon Web Services (AWS) CloudFormation, Google Cloud Platform (GCP) Deployment Manager o Azure Resource Manager (ARM) Templates.

## Conclusión

Kubernetes es una poderosa herramienta de orquestación de contenedores que puede ayudarlo a aumentar la eficiencia y la agilidad de sus equipos de operaciones y desarrollo. Kubernetes se puede implementar en nubes públicas como AWS, GCP y Azure, o en su propia infraestructura privada.

Este artículo ha proporcionado una descripción general de la herramienta de orquestación de contenedores de Kubernetes y le ha mostrado cómo implementar un clúster de Kubernetes en su propia infraestructura.