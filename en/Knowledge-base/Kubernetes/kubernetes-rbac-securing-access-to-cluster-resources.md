---
title: Kubernetes RBAC: Securing Access to Cluster Resources
description: 
published: true
date: 2023-02-09T00:32:33.335Z
tags: 
editor: markdown
dateCreated: 2023-02-09T00:32:27.333Z
---

- [RBAC de Kubernetes: protección del acceso a los recursos del clúster***Spanish** document is available*](/es/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}
- [Kubernetes RBAC：保护对集群资源的访问***Chinese Simplified** document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}
- [Kubernetes RBAC: 클러스터 리소스에 대한 액세스 보안***Korean** document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}


# Kubernetes RBAC: Securing Access to Cluster Resources

Role-based access control (RBAC) is a method of regulating access to computer systems, applications, and data. It is a fundamental component of security in any enterprise environment.

In Kubernetes, RBAC is used to control access to the Kubernetes API. Any user, group, or service account that needs to access the Kubernetes API must be given a role that defines the level of access they have.

There are three types of roles in Kubernetes:

- **ClusterRole**: A ClusterRole defines a set of permissions that can be applied to all namespaces in a cluster.
- **Role**: A Role can only be applied to a single namespace.
- **ServiceAccount**: A ServiceAccount defines a set of permissions that can be applied to a service account.

Roles can be created using the `kubectl` command line tool. For example, to create a ClusterRole named `my-cluster-role`, you would use the following command:

```
kubectl create clusterrole my-cluster-role --verb=get,list,watch
```

This would give the `my-cluster-role` the permissions to `get`, `list`, and `watch` resources in the cluster.

Roles can also be created using YAML files. The following is an example YAML file for a ClusterRole:

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

Roles can be binded to users, groups, or service accounts using `RoleBinding` or `ClusterRoleBinding`. For example, the following command would give the `my-user` the `my-cluster-role`:

```
kubectl create clusterrolebinding my-cluster-role-binding --clusterrole=my-cluster-role --user=my-user
```

This would give the `my-user` the permissions defined in the `my-cluster-role`.

 Bindings can also be created using YAML files. The following is an example YAML file for a ClusterRoleBinding:

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

This would give the `my-user` the `my-cluster-role`.

RBAC can be used to control access to the Kubernetes API for any user, group, or service account. It is a fundamental component of security in any Kubernetes cluster.