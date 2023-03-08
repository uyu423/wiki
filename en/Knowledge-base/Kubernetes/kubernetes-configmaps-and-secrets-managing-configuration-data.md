---
title: Kubernetes ConfigMaps and Secrets: Managing Configuration Data
description: 
published: true
date: 2023-02-01T17:43:47.829Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:43:43.775Z
---

- [Kubernetes ConfigMaps and Secrets: administración de datos de configuración***Spanish** version of this document is available*](/es/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}
- [Kubernetes ConfigMap 및 Secrets: 구성 데이터 관리***Korean** version of this document is available*](/ko/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}
- [Kubernetes ConfigMaps 和秘密：管理配置数据***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}



# Kubernetes ConfigMaps and Secrets: Managing Configuration Data

Kubernetes provides two mechanisms for storing and managing configuration data and secrets: ConfigMaps and Secrets. In this article, we'll take a look at what each of these are, how they work, and how to use them effectively in your Kubernetes applications.

## What is a ConfigMap?

A ConfigMap is a Kubernetes resource that stores configuration data in key-value pairs. This data can be used by applications to read and use as needed. For example, you might store database connection strings, API keys, or other secrets in a ConfigMap.

ConfigMaps are stored in etcd, the same place Kubernetes stores its cluster state. This means that they are highly available and can be used by any node in the cluster.

## What is a Secret?

A Secret is a Kubernetes resource that stores sensitive information, such as passwords, API keys, or certificates. Secrets are encrypted and can only be decrypted by the nodes that need to use them. This means that Secrets are more secure than ConfigMaps, but they are also more difficult to manage.

 Secrets are also stored in etcd, but they are encrypted at rest.

## Creating a ConfigMap

Creating a ConfigMap is simple. We just need to create a YAML file with the configuration data. For example, let's create a ConfigMap for a database connection string:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  database-connection-string: "user:password@host:port/database"
```

We can then create the ConfigMap using the kubectl command-line tool:

```
$ kubectl create -f my-config.yaml
configmap/my-config created
```

## Creating a Secret

Creating a Secret is similar to creating a ConfigMap. We just need to create a YAML file with the configuration data. For example, let's create a Secret for an API key:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

The data in a Secret must be base64-encoded. We can then create the Secret using the kubectl command-line tool:

```
$ kubectl create -f my-secret.yaml
secret/my-secret created
```

## Using ConfigMaps and Secrets

Now that we've created our ConfigMap and Secret, let's see how we can use them in our applications.

There are two ways to use ConfigMaps and Secrets in Kubernetes: environment variables and volumes.

### Environment Variables

We can use environment variables to inject the data from our ConfigMap and Secret into our applications. To do this, we just need to add the following annotations to our ConfigMap and Secret:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/env": "MY_CONFIG"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/env": "MY_SECRET"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

The annotations will cause Kubernetes to inject the data from our ConfigMap and Secret into the environment of our application pods. The data will be available in the environment variables MY_CONFIG and MY_SECRET.

### Volumes

We can also use volumes to mount the data from our ConfigMap and Secret into our applications. To do this, we just need to add the following annotations to our ConfigMap and Secret:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/volume": "my-config-volume"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/volume": "my-secret-volume"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

The annotations will cause Kubernetes to create volumes for our ConfigMap and Secret. These volumes will be available in our application pods at the paths /etc/config/my-config-volume and /etc/config/my-secret-volume.

## Conclusion

ConfigMaps and Secrets are two important tools for managing configuration data and secrets in Kubernetes. They are both stored in etcd and can be used by any node in the cluster.

ConfigMaps are less secure than Secrets but are easier to manage. Secrets are more secure but are more difficult to manage.

We can use environment variables or volumes to inject the data from our ConfigMap and Secret into our applications.