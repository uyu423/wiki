---
title: RBAC de Kubernetes: protección del acceso a los recursos del clúster
description: 
published: true
date: 2023-02-09T00:32:28.962Z
tags: 
editor: markdown
dateCreated: 2023-02-09T00:32:27.330Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes RBAC: Securing Access to Cluster Resources***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}


# Kubernetes RBAC: Acceso seguro a los recursos del clúster

El control de acceso basado en roles (RBAC) es un método para regular el acceso a sistemas informáticos, aplicaciones y datos. Es un componente fundamental de la seguridad en cualquier entorno empresarial.

En Kubernetes, RBAC se usa para controlar el acceso a la API de Kubernetes. Cualquier usuario, grupo o cuenta de servicio que necesite acceder a la API de Kubernetes debe recibir una función que defina el nivel de acceso que tiene.

Hay tres tipos de roles en Kubernetes:

- **ClusterRole**: un ClusterRole define un conjunto de permisos que se pueden aplicar a todos los espacios de nombres en un clúster.
- **Función**: una función solo se puede aplicar a un único espacio de nombres.
- **ServiceAccount**: una ServiceAccount define un conjunto de permisos que se pueden aplicar a una cuenta de servicio.

Los roles se pueden crear utilizando la herramienta de línea de comandos `kubectl`. Por ejemplo, para crear un ClusterRole llamado `my-cluster-role`, usaría el siguiente comando:

```
kubectl create clusterrole my-cluster-role --verb=get,list,watch
```

Esto le daría a `my-cluster-role` los permisos para `obtener`, `listar` y `observar` recursos en el clúster.

Los roles también se pueden crear usando archivos YAML. El siguiente es un archivo YAML de ejemplo para un ClusterRole:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: my-cluster-role
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

Los roles se pueden vincular a usuarios, grupos o cuentas de servicio mediante `RoleBinding` o `ClusterRoleBinding`. Por ejemplo, el siguiente comando le daría a `my-user` el `my-cluster-role`:

```
kubectl create clusterrolebinding my-cluster-role-binding --clusterrole=my-cluster-role --user=my-user
```

Esto le daría a `my-user` los permisos definidos en `my-cluster-role`.

 Los enlaces también se pueden crear utilizando archivos YAML. El siguiente es un archivo YAML de ejemplo para un ClusterRoleBinding:

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: my-cluster-role-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: my-cluster-role
subjects:
- kind: User
  name: my-user
  apiGroup: rbac.authorization.k8s.io
```

Esto le daría a `my-user` el `my-cluster-role`.

RBAC se puede usar para controlar el acceso a la API de Kubernetes para cualquier usuario, grupo o cuenta de servicio. Es un componente fundamental de la seguridad en cualquier clúster de Kubernetes.