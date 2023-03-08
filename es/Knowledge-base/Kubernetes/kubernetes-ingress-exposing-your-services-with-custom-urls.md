---
title: Ingress de Kubernetes: exposición de sus servicios con URL personalizadas
description: 
published: true
date: 2023-02-08T21:32:18.348Z
tags: 
editor: markdown
dateCreated: 2023-02-08T21:32:16.710Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Ingress: Exposing Your Services with Custom URLs***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-ingress-exposing-your-services-with-custom-urls)
{.links-list}


# Ingress de Kubernetes: exposición de sus servicios con URL personalizadas

Kubernetes Ingress es una forma poderosa de exponer sus servicios al mundo. Con Ingress, puede crear direcciones URL personalizadas para sus servicios, lo que puede ser útil por varios motivos.

Por ejemplo, puede que desee crear una URL para su servicio que sea fácil de recordar, o puede que desee crear una URL que sea específica para un determinado servicio.

En este artículo, veremos cómo crear recursos de Kubernetes Ingress y también veremos algunos de los beneficios de usar Ingress.

## Crear un recurso de ingreso

Crear un recurso de Ingress es simple. Simplemente cree un archivo llamado ingress.yaml con los siguientes contenidos:

```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: my-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
      - path: /my-service
        backend:
          serviceName: my-service
          servicePort: 80
```

En el ejemplo anterior, creamos un recurso Ingress que expone el servicio my-service en la URL /my-service.

## Beneficios del ingreso

Hay una serie de beneficios al usar Ingress.

Primero, Ingress le permite crear URL personalizadas para sus servicios. Esto puede ser útil por varias razones. Por ejemplo, puede que desee crear una URL para su servicio que sea fácil de recordar, o puede que desee crear una URL que sea específica para un determinado servicio.

En segundo lugar, Ingress le permite equilibrar la carga del tráfico entre varios servicios. Esto puede ser útil si tiene varios servicios que sirven para el mismo propósito.

En tercer lugar, Ingress le permite enrutar el tráfico en función del nombre de host. Esto puede ser útil si desea enrutar el tráfico a diferentes servicios en función del nombre de host.

En cuarto lugar, Ingress le permite enrutar el tráfico en función de la ruta. Esto puede ser útil si desea enrutar el tráfico a diferentes servicios en función de la ruta.

Finalmente, Ingress le permite proteger sus servicios con SSL/TLS. Esto puede ser útil si desea asegurarse de que el tráfico a sus servicios esté encriptado.

## Conclusión

En este artículo, analizamos cómo crear recursos de Kubernetes Ingress y también analizamos algunos de los beneficios de usar Ingress.