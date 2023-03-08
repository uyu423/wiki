---
title: Kubernetes con Istio: implementación de Service Mesh para sus aplicaciones
description: 
published: true
date: 2023-02-02T05:44:02.961Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:43:58.529Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with Istio: Implementing Service Mesh for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-istio-implementing-service-mesh-for-your-applications)
{.links-list}


# Kubernetes con Istio: Implementando Service Mesh para sus aplicaciones

Kubernetes es un sistema de código abierto para automatizar la gestión de aplicaciones en contenedores. Istio es una plataforma abierta para conectar, administrar y asegurar microservicios.

Service Mesh es una capa de infraestructura configurable para aplicaciones de microservicios que hace que la comunicación entre servicios sea confiable, rápida y segura. Una malla de servicio generalmente consta de un plano de datos y un plano de control. El plano de datos está compuesto por un conjunto de proxies inteligentes que median la comunicación entre microservicios. El plano de control administra y configura los proxies.

Istio es una red de servicios para Kubernetes. Se compone de un plano de datos y un plano de control. El plano de datos está compuesto por un conjunto de proxies inteligentes que median la comunicación entre microservicios. El plano de control administra y configura los proxies.

Kubernetes con Istio se puede utilizar para implementar una red de servicios para sus aplicaciones. En este artículo, le mostraremos cómo instalar y configurar Istio en un clúster de Kubernetes y cómo implementar una aplicación de microservicios de muestra.

## Instalación de Istio en Kubernetes

Istio se puede instalar en un clúster de Kubernetes mediante el administrador de paquetes de Helm. Helm es una herramienta para gestionar aplicaciones de Kubernetes.

Para instalar Istio, primero debe instalar Helm y agregar el repositorio de Istio Helm.

### Instalación de Helm

Descargue el binario de Helm del [sitio web de Helm] (https://helm.sh/docs/using_helm/# installing-helm).

Extraiga el binario helm y agréguelo a su RUTA.

```
tar xzf helm-v2.16.5-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/
```

Inicialice Helm e instale Tiller, el componente del lado del servidor de Helm.

```
helm init
```

### Adición del repositorio Istio Helm

Agregue el repositorio Istio Helm.

```
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.5.2/charts/
```

Actualice el repositorio de Helm.

```
helm repo update
```

## Implementación de una aplicación de microservicios de muestra

Implementaremos una aplicación de microservicios de muestra que consta de cuatro servicios:

- Un servicio frontend escrito en Node.js
- Un servicio backend escrito en Golang
- Un servicio de base de datos.
- Un servicio de balanceador de carga

Los servicios de frontend y backend se implementarán en módulos separados. El servicio de base de datos se implementará en un pod separado. El servicio del equilibrador de carga se implementará en un pod separado.

El servicio frontend hará solicitudes al servicio backend. El servicio de backend realizará solicitudes al servicio de base de datos. El servicio de equilibrador de carga enrutará el tráfico a los servicios de frontend y backend.

Implementaremos la aplicación utilizando el gráfico de Istio Helm.

### Instalación del gráfico de timón de Istio

Instale el gráfico Istio Helm con el siguiente comando:

```
helm install --name istio-system -f /path/to/custom-values.yaml istio.io/istio
```

El gráfico Istio Helm está instalado en el espacio de nombres `istio-system`.

### Implementación del servicio de interfaz

Cree un pod para el servicio frontend.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
  labels:
    app: frontend
spec:
  containers:
  - name: frontend
    image: node:12-alpine
    ports:
    - containerPort: 3000
```

Implemente la cápsula.

```
kubectl apply -f /path/to/frontend-pod.yaml
```

### Implementación del servicio backend

Cree un pod para el servicio de backend.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend
  labels:
    app: backend
spec:
  containers:
  - name: backend
    image: golang:1.14-alpine
    ports:
    - containerPort: 3000
```

Implemente la cápsula.

```
kubectl apply -f /path/to/backend-pod.yaml
```

### Implementación del servicio de base de datos

Cree un pod para el servicio de base de datos.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: database
  labels:
    app: database
spec:
  containers:
  - name: database
    image: mysql:5.7
    ports:
    - containerPort: 3306
```

Implemente la cápsula.

```
kubectl apply -f /path/to/database-pod.yaml
```

### Implementación del servicio del equilibrador de carga

Cree un pod para el servicio de equilibrador de carga.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: load-balancer
  labels:
    app: load-balancer
spec:
  containers:
  - name: load-balancer
    image: nginx:1.17.9-alpine
    ports:
    - containerPort: 80
```

Implemente la cápsula.

```
kubectl apply -f /path/to/load-balancer-pod.yaml
```

### Prueba de la aplicación

Para probar la aplicación, enviaremos una solicitud al servicio de equilibrador de carga. El servicio del equilibrador de carga enrutará la solicitud al servicio de interfaz. El servicio frontend hará una solicitud al servicio backend. El servicio de backend hará una solicitud al servicio de la base de datos.

Primero, necesitamos obtener la dirección IP del servicio del balanceador de carga.

```
kubectl get svc
```

La salida debería verse así:

```
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
frontend        ClusterIP      10.108.1.194     <none>        3000/TCP         1m
backend         ClusterIP      10.96.247.199    <none>        3000/TCP         1m
database        ClusterIP      10.111.142.247   <none>        3306/TCP         1m
load-balancer   LoadBalancer   10.102.129.251   <pending>     80:32000/TCP     1m
```

El servicio del equilibrador de carga tiene un "ClusterIP" de "10.102.129.251" y un "PUERTO" de "80:32000".

Ahora podemos enviar una solicitud al servicio de equilibrador de carga.

```
curl -v http://10.102.129.251:80
```

La salida debería verse así:

```
*   Trying 10.102.129.251:80...
* TCP_NODELAY set
* Connected to 10.102.129.251 (10.102.129.251) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.102.129.251:80
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200 OK
< Content-Type: text/html
< Content-Length: 28
<
<html>
<body>
Hello, World!
</body>
</html>
* Connection #0 to host 10.102.129.251 left intact
```

La solicitud se enrutó al servicio frontend y se devolvió la respuesta.

## Conclusión

En este artículo, le mostramos cómo instalar y configurar Istio en un clúster de Kubernetes y cómo implementar una aplicación de microservicios de muestra. Istio se puede utilizar para implementar una red de servicios para sus aplicaciones.