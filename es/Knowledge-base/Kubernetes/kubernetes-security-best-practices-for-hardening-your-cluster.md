---
title: Seguridad de Kubernetes: mejores prácticas para fortalecer su clúster
description: 
published: true
date: 2023-02-09T01:32:55.691Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:32:53.973Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Security: Best Practices for Hardening Your Cluster***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-security-best-practices-for-hardening-your-cluster)
{.links-list}


# Seguridad de Kubernetes: mejores prácticas para fortalecer su clúster

A medida que adopta Kubernetes, obtiene la flexibilidad para implementar, escalar y administrar aplicaciones en contenedores de una manera altamente disponible. Pero este nuevo nivel de control y responsabilidad también conlleva nuevos desafíos de seguridad.

Kubernetes es un sistema complejo con muchos componentes y partes móviles, lo que dificulta su seguridad de forma predeterminada. Sin embargo, siguiendo algunas prácticas recomendadas simples, puede fortalecer su clúster de Kubernetes y proteger sus aplicaciones de amenazas comunes.

En este artículo, cubriremos algunas de las mejores prácticas de seguridad de Kubernetes más importantes, que incluyen:

* Configuración de RBAC para controlar el acceso a los recursos de Kubernetes
* Cifrado del tráfico de red con TLS
* Implementación de políticas de red para restringir la comunicación entre pods
* Ejecución de contenedores en un contexto de seguridad con privilegios mínimos
* Protección del servidor API de Kubernetes
* Uso de un escáner de imágenes para hacer cumplir las políticas de seguridad

## Configuración de RBAC para controlar el acceso a los recursos de Kubernetes

El control de acceso basado en roles (RBAC) es una característica de Kubernetes que le permite controlar de forma granular qué usuarios y cuentas de servicio tienen acceso a qué recursos de Kubernetes.

RBAC está deshabilitado de forma predeterminada en Kubernetes, por lo que el primer paso para asegurar su clúster es habilitarlo. Puede hacerlo pasando el indicador `--authorization-mode=RBAC` al binario `kube-apiserver` al iniciar su clúster de Kubernetes.

Una vez que RBAC está habilitado, puede crear objetos `Role` y `ClusterRole` para definir los permisos que se deben otorgar a un usuario o cuenta de servicio determinados. Por ejemplo, podría crear un "Rol" que permita a un usuario ver y enumerar todos los recursos en un espacio de nombres, pero no crear ni eliminar ningún recurso.

A continuación, puede crear un `RoleBinding` o `ClusterRoleBinding` para vincular un `Role` o `ClusterRole` a una cuenta de usuario o de servicio. Esto otorgará los permisos especificados al usuario o cuenta de servicio.

Es importante tener en cuenta que, de forma predeterminada, cualquier usuario autenticado tendrá acceso completo a la API de Kubernetes. Esto significa que, a menos que restrinja explícitamente el acceso con RBAC, cualquier usuario que pueda autenticarse en su clúster de Kubernetes podrá realizar cualquier acción, incluida la eliminación de todos los recursos del clúster.

## Cifrado del tráfico de red con TLS

Transport Layer Security (TLS) es un protocolo que le permite cifrar el tráfico de red para evitar escuchas ilegales y manipulaciones.

Kubernetes usa TLS para cifrar toda la comunicación entre los componentes, así como la comunicación entre el servidor de la API de Kubernetes y los clientes. De forma predeterminada, Kubernetes generará certificados autofirmados para todos los componentes. Si bien esto es suficiente para la mayoría de los entornos de desarrollo y prueba, debe usar certificados firmados en producción para asegurarse de que el tráfico no pueda ser interceptado o alterado.

Puede generar certificados firmados utilizando una autoridad de certificación (CA) de su elección, o puede usar una herramienta como `kube-ssl` para generar e implementar automáticamente certificados firmados para su clúster de Kubernetes.

## Implementación de una política de red para restringir la comunicación entre pods

La política de red es una característica de Kubernetes que le permite controlar qué pods pueden comunicarse entre sí. De manera predeterminada, todos los pods en un clúster de Kubernetes pueden comunicarse entre sí, pero esto expone sus aplicaciones a riesgos innecesarios.

Por ejemplo, si tiene un pod que contiene datos confidenciales, es posible que desee restringir las comunicaciones para permitir solo la comunicación desde pods de confianza. O bien, si tiene una aplicación que consta de varios microservicios, es posible que desee restringir las comunicaciones para permitir solo la comunicación entre los servicios que necesitan comunicarse entre sí.

La política de red se implementa como un recurso de Kubernetes y puede usarla para especificar qué pods pueden comunicarse entre sí. Por ejemplo, la siguiente política de red permitirá la comunicación entre los pods en los espacios de nombres "frontend" y "backend", pero no permitirá la comunicación entre los pods en el espacio de nombres "frontend" y los pods en el espacio de nombres "base de datos":

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: frontend-backend
  namespace: frontend
spec:
  podSelector:
    matchLabels:
      app: frontend
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: backend
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: backend
```

La política de red es un tema complejo y hay muchas formas diferentes de configurarla. Recomendamos leer la documentación de Kubernetes sobre política de red para obtener más información.

## Ejecución de contenedores en un contexto de seguridad con privilegios mínimos

Un contexto de seguridad es un conjunto de opciones relacionadas con la seguridad que se pueden aplicar a un pod o contenedor. Estas opciones se pueden usar para controlar cosas como qué usuarios y grupos pueden acceder al pod o contenedor, así como qué capacidades están permitidas.

De forma predeterminada, los contenedores en Kubernetes se ejecutan como usuario "raíz", lo que otorga a los contenedores acceso total al sistema host. Este es un riesgo de seguridad importante, ya que un contenedor malicioso podría acceder a datos confidenciales del sistema host o incluso apoderarse de todo el sistema host.

Para mitigar este riesgo, siempre debe ejecutar contenedores en un contexto de seguridad con privilegios mínimos. Esto significa especificar un usuario no root para que se ejecute el contenedor, así como especificar qué capacidades puede usar el contenedor.

Por ejemplo, la siguiente definición de `Pod` ejecutará el contenedor `nginx` como el usuario `nginx` y no permitirá que el contenedor use ninguna capacidad:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  securityContext:
    runAsUser: 1000
    fsGroup: 1000
  containers:
  - name: nginx
    image: nginx
    securityContext:
      capabilities: {}
```

La ejecución de contenedores como usuario no root es una buena práctica de seguridad en general, y es especialmente importante en Kubernetes, donde los contenedores pueden acceder potencialmente a datos confidenciales del sistema host.

## Protección del servidor API de Kubernetes

El servidor de API de Kubernetes es el punto central de comunicación para todos los componentes de Kubernetes y es responsable de procesar todas las solicitudes de API. Esto hace que el servidor API sea un componente crítico del sistema Kubernetes y es importante protegerlo para evitar el acceso no autorizado.

Una forma de proteger el servidor API es usar certificados TLS para cifrar todo el tráfico hacia y desde el servidor API. Como mencionamos anteriormente, Kubernetes generará certificados autofirmados para todos los componentes de manera predeterminada, pero debe usar certificados firmados en producción para asegurarse de que el tráfico no pueda ser interceptado o alterado.

Otra forma de asegurar el servidor API es usar un complemento de autenticación. Kubernetes incluye varios complementos de autenticación integrados, incluidos `HTTPBasicAuth`, `Token`, `X509` y `Webhook`. También puede usar complementos de autenticación de terceros, como `OIDC` o `LDAP`.

## Uso de un escáner de imágenes para hacer cumplir las políticas de seguridad

Los escáneres de imágenes son herramientas que lo ayudan a aplicar políticas de seguridad para imágenes de contenedores. Por ejemplo, puede usar un escáner de imágenes para verificar vulnerabilidades conocidas en sus imágenes o para aplicar políticas que requieran que las imágenes estén firmadas por una autoridad de confianza.

Kubernetes incluye un escáner de imágenes incorporado llamado `Clair`, que se puede usar para escanear imágenes en busca de vulnerabilidades conocidas. Clair es un proyecto de código abierto y puede encontrar más información al respecto en el sitio web del proyecto.

Además de Clair, hay otros escáneres de imágenes disponibles, tanto de código abierto como comerciales. Recomendamos investigar un poco para encontrar un escáner de imágenes que satisfaga sus necesidades específicas.

## Conclusión

En este artículo, cubrimos algunas de las mejores prácticas de seguridad de Kubernetes más importantes. Al seguir estas mejores prácticas, puede fortalecer su clúster de Kubernetes y proteger sus aplicaciones de amenazas comunes.