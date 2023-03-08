---
title: Kubernetes con Envoy: administración del tráfico para sus servicios
description: 
published: true
date: 2023-02-12T23:17:35.874Z
tags: 
editor: markdown
dateCreated: 2023-02-12T23:17:34.227Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes with Envoy: Managing Traffic for Your Services***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-envoy-managing-traffic-for-your-services)
{.links-list}


# Kubernetes con Envoy: gestión del tráfico de sus servicios

En una arquitectura de microservicios, es común que cada servicio tenga su propia URL única. Esto puede crear problemas al intentar enrutar el tráfico entre servicios, especialmente cuando se trata de balanceo de carga.

Una solución a este problema es utilizar un proxy inverso. Un proxy inverso es un servidor que se encuentra entre el cliente y el servidor web. Intercepta todas las solicitudes del cliente y las reenvía al servidor apropiado.

Envoy es un popular proxy inverso de código abierto que se puede usar junto con Kubernetes. Kubernetes es una plataforma de orquestación de contenedores que le permite implementar y administrar aplicaciones en contenedores a escala.

Envoy se puede usar para enrutar el tráfico entre servicios en un clúster de Kubernetes. También se puede utilizar para equilibrar la carga del tráfico entre servicios.

En este artículo, veremos cómo usar Envoy con Kubernetes para administrar el tráfico de sus servicios.

## Configuración de Enviado

Envoy se puede implementar como un contenedor sidecar junto con su contenedor de aplicaciones. Este es el modelo de implementación recomendado para Envoy.

Un contenedor sidecar es un contenedor que se implementa junto con su contenedor de aplicaciones. Proporciona un enlace de red dedicado entre el contenedor de la aplicación y el mundo exterior.

Para implementar Envoy como contenedor sidecar, debe crear un pod de Kubernetes que contenga tanto el contenedor Envoy como el contenedor de su aplicación.

Aquí hay una definición de pod de ejemplo que implementa Envoy como un contenedor sidecar junto con un contenedor Nginx:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.7.9
    ports:
    - containerPort: 80
  - name: envoy
    image: envoyproxy/envoy:v1.5.0
    ports:
    - containerPort: 8001
    - containerPort: 8002
```

En la definición de Pod anterior, hemos definido dos contenedores. El primer contenedor es nuestro contenedor Nginx. El segundo contenedor es el contenedor Envoy.

También hemos definido dos puertos para el contenedor Envoy. El puerto 8001 es el puerto en el que Envoy escuchará el tráfico HTTP. El puerto 8002 es el puerto en el que Envoy escuchará el tráfico TCP.

## Configuración de Enviado

Envoy se configura mediante un archivo de configuración JSON. El archivo de configuración define los puertos de escucha, los upstreams y las rutas.

Los puertos de escucha son los puertos en los que Envoy escuchará el tráfico entrante.

Los upstreams son los servicios upstream a los que Envoy enviará el tráfico por proxy.

Las rutas son las rutas que utilizará Envoy para mapear el tráfico hacia los flujos ascendentes.

Aquí hay un ejemplo de archivo de configuración de Envoy:

```json
{
  "admin": {
    "access_log_path": "/tmp/admin_access.log",
    "address": {
      "socket_address": {
        "address": "127.0.0.1",
        "port_value": 8001
      }
    }
  },
  "static_resources": {
    "listeners": [
      {
        "name": "listener_0",
        "address": {
          "socket_address": {
            "address": "127.0.0.1",
            "port_value": 80
          }
        },
        "filter_chains": [
          {
            "filters": [
              {
                "name": "envoy.http_connection_manager",
                "config": {
                  "stat_prefix": "ingress_http",
                  "route_config": {
                    "virtual_hosts": [
                      {
                        "name": "service",
                        "domains": [
                          "*"
                        ],
                        "routes": [
                          {
                            "match": {
                              "prefix": "/"
                            },
                            "route": {
                              "cluster": "service"
                            }
                          }
                        ]
                      }
                    ]
                  },
                  "http_filters": [
                    {
                      "name": "envoy.router"
                    }
                  ]
                }
              }
            ]
          }
        ]
      }
    ],
    "clusters": [
      {
        "name": "service",
        "connect_timeout": "0.25s",
        "type": "strict_dns",
        "lb_policy": "round_robin",
        "hosts": [
          {
            "socket_address": {
              "address": "127.0.0.1",
              "port_value": 8002
            }
          }
        ]
      }
    ]
  }
}
```

En el archivo de configuración anterior, hemos definido un oyente en el puerto 80 y un clúster para nuestro servicio ascendente. También hemos definido una ruta que asigna el tráfico desde la ruta "/" a nuestro servicio ascendente.

## Implementación de Envoy

Envoy se puede implementar mediante Kubernetes DaemonSet. Un DaemonSet garantiza que todos los nodos del clúster de Kubernetes tengan una copia del contenedor Envoy en ejecución.

Aquí hay un ejemplo de definición de DaemonSet:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: envoy
  labels:
    app: envoy
spec:
  selector:
    matchLabels:
      app: envoy
  template:
    metadata:
      labels:
        app: envoy
    spec:
      containers:
      - name: envoy
        image: envoyproxy/envoy:v1.5.0
        ports:
        - containerPort: 8001
        - containerPort: 8002
        env:
        - name: ENVOY_CONFIG
          value: /etc/envoy/envoy.json
        volumeMounts:
        - name: envoy-config
          mountPath: /etc/envoy
      volumes:
      - name: envoy-config
        configMap:
          name: envoy-config
```

En la definición anterior de DaemonSet, hemos definido un contenedor para Envoy y un volumen para el archivo de configuración de Envoy. También hemos definido una variable de entorno que apunta al archivo de configuración de Envoy.

## Conclusión

En este artículo, analizamos cómo usar Envoy con Kubernetes para administrar el tráfico de sus servicios. También hemos analizado cómo configurar e implementar Envoy.