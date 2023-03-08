---
title: Ajuste de escala automático de Kubernetes: adaptación a las cargas cambiantes
description: 
published: true
date: 2023-02-08T18:32:37.150Z
tags: 
editor: markdown
dateCreated: 2023-02-08T18:32:30.795Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Autoscaling: Adapting to Changing Loads***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-autoscaling-adapting-to-changing-loads)
{.links-list}


# Ajuste de escala automático de Kubernetes: adaptación a las cargas cambiantes

A medida que las organizaciones avanzan hacia una arquitectura de microservicios, las implementaciones en contenedores se han vuelto cada vez más populares. Kubernetes es una de las plataformas de orquestación de contenedores más populares y la utilizan organizaciones de todos los tamaños.

Una de las características clave de Kubernetes es su capacidad para escalar implementaciones hacia arriba o hacia abajo en respuesta a cargas cambiantes. Esto se conoce como ajuste de escala automático y puede ser útil en varias situaciones, como cuando se lanzan nuevas funciones o durante un pico en el tráfico.

En este artículo, veremos cómo funciona el ajuste de escala automático en Kubernetes y cómo puede usarlo para adaptarse a las cargas cambiantes.

## ¿Qué es el escalado automático?

El escalado automático es el proceso de escalar dinámicamente un sistema hacia arriba o hacia abajo en respuesta a condiciones cambiantes. En el contexto de Kubernetes, esto generalmente significa aumentar o reducir la cantidad de réplicas en una implementación.

El escalado automático se puede usar para escalar implementaciones en respuesta a cambios en la utilización de la CPU, el uso de la memoria u otras métricas personalizadas. Kubernetes también se puede configurar para escalar según la cantidad de pods pendientes o la cantidad de espacio disponible en el disco.

## ¿Cómo funciona el escalado automático en Kubernetes?

El escalado automático en Kubernetes se logra mediante el uso de controladores de replicación o implementaciones. Un controlador de replicación es responsable de mantener una cantidad deseada de réplicas para una implementación determinada.

Cuando el ajuste de escala automático está habilitado, el controlador de replicación escalará la implementación hacia arriba o hacia abajo según sea necesario para mantener la cantidad deseada de réplicas. El número de réplicas puede especificarse manualmente o ajustarse automáticamente en función de condiciones como el uso de la CPU o el uso de la memoria.

## ¿Cuándo debería usar el ajuste de escala automático?

El ajuste de escala automático se puede utilizar en una serie de situaciones en las que es necesario ajustar dinámicamente el número de réplicas.

Algunos casos de uso comunes para el ajuste de escala automático incluyen:

- Escalar las implementaciones hacia arriba o hacia abajo en respuesta a los cambios en el tráfico
- Escalar las implementaciones hacia arriba o hacia abajo en respuesta a los cambios en la utilización de la CPU
- Escalar las implementaciones hacia arriba o hacia abajo en respuesta a los cambios en el uso de la memoria

## Cómo habilitar el escalado automático en Kubernetes

El ajuste de escala automático se puede habilitar para una implementación determinada especificando la cantidad deseada de réplicas. Esto se puede hacer usando la herramienta de línea de comandos `kubectl` o editando el archivo YAML de la implementación.

Para habilitar el escalado automático usando `kubectl`, puede usar el comando `kubectl scale`. Por ejemplo, el siguiente comando establecerá la cantidad deseada de réplicas para una implementación en 3:

```
kubectl scale --replicas=3 deployment/my-deployment
```

Para habilitar el ajuste de escala automático mediante la edición del archivo YAML de la implementación, deberá agregar una clave `réplicas` a la sección `spec`. Por ejemplo:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: my-image
        ports:
        - containerPort: 8080
```

## Conclusión

En este artículo, analizamos cómo funciona el ajuste de escala automático en Kubernetes y cómo puede usarlo para adaptarse a las cargas cambiantes. El ajuste de escala automático se puede usar para escalar implementaciones hacia arriba o hacia abajo en respuesta a cambios en el tráfico, la utilización de la CPU o el uso de la memoria.

Si está interesado en obtener más información sobre Kubernetes, consulte los siguientes recursos:

- La documentación oficial de Kubernetes: https://kubernetes.io/docs/
- El canal de Slack de la comunidad de Kubernetes: https://kubernetes.slack.com/
- Resultados de la encuesta de la comunidad de usuarios finales de CNCF: https://www.cncf.io/blog/2019/03/12/cncf-end-user-community-survey-results/