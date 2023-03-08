---
title: Kubernetes ConfigMaps and Secrets: administración de datos de configuración
description: 
published: true
date: 2023-02-01T17:43:47.829Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:43:43.781Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Kubernetes ConfigMaps and Secrets: Managing Configuration Data***Spanish** version of this document is available*](/es/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}



# Kubernetes ConfigMaps and Secrets: administración de datos de configuración

Kubernetes proporciona dos mecanismos para almacenar y administrar datos y secretos de configuración: ConfigMaps y Secrets. En este artículo, veremos qué es cada uno de estos, cómo funcionan y cómo usarlos de manera efectiva en sus aplicaciones de Kubernetes.

## ¿Qué es un mapa de configuración?

Un ConfigMap es un recurso de Kubernetes que almacena datos de configuración en pares clave-valor. Las aplicaciones pueden usar estos datos para leerlos y usarlos según sea necesario. Por ejemplo, puede almacenar cadenas de conexión de base de datos, claves de API u otros secretos en un ConfigMap.

Los ConfigMaps se almacenan en etcd, el mismo lugar donde Kubernetes almacena su estado de clúster. Esto significa que tienen una alta disponibilidad y pueden ser utilizados por cualquier nodo del clúster.

## ¿Qué es un secreto?

Un secreto es un recurso de Kubernetes que almacena información confidencial, como contraseñas, claves de API o certificados. Los secretos están encriptados y solo pueden ser desencriptados por los nodos que necesitan usarlos. Esto significa que los secretos son más seguros que ConfigMaps, pero también son más difíciles de administrar.

 Los secretos también se almacenan en etcd, pero se cifran en reposo.

## Creación de un mapa de configuración

Crear un ConfigMap es simple. Solo necesitamos crear un archivo YAML con los datos de configuración. Por ejemplo, creemos un ConfigMap para una cadena de conexión de base de datos:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  database-connection-string: "user:password@host:port/database"
```

Luego podemos crear el ConfigMap usando la herramienta de línea de comandos kubectl:

```
$ kubectl create -f my-config.yaml
configmap/my-config created
```

## Creando un secreto

Crear un secreto es similar a crear un ConfigMap. Solo necesitamos crear un archivo YAML con los datos de configuración. Por ejemplo, creemos un secreto para una clave de API:

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

Los datos en un secreto deben estar codificados en base64. Luego podemos crear el Secreto usando la herramienta de línea de comandos kubectl:

```
$ kubectl create -f my-secret.yaml
secret/my-secret created
```

## Uso de ConfigMaps y secretos

Ahora que hemos creado nuestro ConfigMap y Secret, veamos cómo podemos usarlos en nuestras aplicaciones.

Hay dos formas de usar ConfigMaps y Secrets en Kubernetes: variables de entorno y volúmenes.

### Variables de entorno

Podemos usar variables de entorno para inyectar los datos de nuestro ConfigMap y Secret en nuestras aplicaciones. Para hacer esto, solo necesitamos agregar las siguientes anotaciones a nuestro ConfigMap y Secret:

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

Las anotaciones harán que Kubernetes inyecte los datos de nuestro ConfigMap y Secret en el entorno de nuestros módulos de aplicaciones. Los datos estarán disponibles en las variables de entorno MY_CONFIG y MY_SECRET.

### Volúmenes

También podemos usar volúmenes para montar los datos de nuestro ConfigMap y Secret en nuestras aplicaciones. Para hacer esto, solo necesitamos agregar las siguientes anotaciones a nuestro ConfigMap y Secret:

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

Las anotaciones harán que Kubernetes cree volúmenes para nuestro ConfigMap y Secret. Estos volúmenes estarán disponibles en nuestros módulos de aplicaciones en las rutas /etc/config/my-config-volume y /etc/config/my-secret-volume.

## Conclusión

ConfigMaps y Secrets son dos herramientas importantes para administrar datos de configuración y secretos en Kubernetes. Ambos se almacenan en etcd y pueden ser utilizados por cualquier nodo del clúster.

Los ConfigMaps son menos seguros que los Secretos, pero son más fáciles de administrar. Los secretos son más seguros pero más difíciles de gestionar.

Podemos usar variables de entorno o volúmenes para inyectar los datos de nuestro ConfigMap y Secret en nuestras aplicaciones.