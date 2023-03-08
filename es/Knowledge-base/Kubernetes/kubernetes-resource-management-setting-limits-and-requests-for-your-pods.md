---
title: Gestión de recursos de Kubernetes: configuración de límites y solicitudes para sus pods
description: 
published: true
date: 2023-02-05T20:17:22.218Z
tags: 
editor: markdown
dateCreated: 2023-02-05T20:17:20.631Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Resource Management: Setting Limits and Requests for Your Pods***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-resource-management-setting-limits-and-requests-for-your-pods)
{.links-list}


# Gestión de recursos de Kubernetes: configuración de límites y solicitudes para sus pods

En un entorno de producción, debe poder controlar los recursos que utilizan sus aplicaciones. Esto es especialmente importante en un entorno en contenedores como Kubernetes, donde muchas aplicaciones pueden ejecutarse en el mismo clúster.

Hay dos formas principales de hacer esto en Kubernetes: establecer límites y solicitudes. Los límites definen la cantidad máxima de recursos que puede usar un pod, mientras que las solicitudes definen la cantidad mínima de recursos que necesita un pod.

En este artículo, veremos cómo establecer límites y solicitudes para sus pods. También veremos algunas mejores prácticas para usar esta configuración.

## Cómo establecer límites y solicitudes

Los límites y las solicitudes se establecen como anotaciones en un pod. Puede configurarlos cuando crea un pod, o puede configurarlos más tarde con el comando de anotación de kubectl.

Este es un ejemplo de cómo establecer límites y solicitudes al crear un pod:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
  annotations:
    "limits.cpu": "1",
    "requests.cpu": "0.5"
spec:
  containers:
  - name: mycontainer
    image: myimage
```

En este ejemplo, estamos configurando un límite de 1 CPU y una solicitud de 0,5 CPU.

También puede configurar estas anotaciones con el comando de anotación de kubectl:

```
kubectl annotate pod mypod "limits.cpu=1" "requests.cpu=0.5"
```

## Mejores prácticas

Hay algunas prácticas recomendadas que se deben tener en cuenta al establecer límites y solicitudes:

* Establecer límites y solicitudes para cada recurso. Si solo establece un límite, Kubernetes no lo aplicará.
* Asegúrese de que sus solicitudes sean inferiores a sus límites. Si no lo son, su pod no se programará.
* Trate de establecer sus solicitudes y límites lo más cerca posible entre sí. Esto ayudará a garantizar que su pod obtenga los recursos que necesita.
* Tenga en cuenta los límites predeterminados que establece su clúster. Si no establece límites y solicitudes, su pod utilizará estos valores predeterminados.

## Conclusión

En este artículo, analizamos cómo establecer límites y solicitudes para sus pods. También hemos analizado algunas prácticas recomendadas para usar esta configuración. Al seguir estas mejores prácticas, puede asegurarse de que sus pods obtengan los recursos que necesitan sin usar más recursos de los necesarios.