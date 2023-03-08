---
title: Implementación de proxies inversos para un mejor rendimiento
description: 
published: true
date: 2023-02-02T01:36:50.272Z
tags: 
editor: markdown
dateCreated: 2023-02-02T01:36:46.138Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing Reverse Proxies for Better Performance***English** document is available*](/en/Knowledge-base/Backend/implementing-reverse-proxies-for-better-performance)
{.links-list}


# Implementación de proxies inversos para un mejor rendimiento

Un proxy inverso es un tipo de servidor proxy que recupera recursos en nombre de un cliente de uno o más servidores. Los proxies inversos se utilizan para mejorar el rendimiento, equilibrar la carga y proporcionar seguridad. En este artículo, discutiremos los beneficios de usar proxies inversos y cómo implementarlos para un mejor rendimiento.

## ¿Por qué usar proxies inversos?

Hay varias razones para usar proxies inversos. Los proxies inversos pueden mejorar el rendimiento almacenando en caché los recursos y distribuyendo la carga entre varios servidores. También pueden brindar seguridad filtrando solicitudes y ocultando la identidad de los servidores.

## Almacenamiento en caché

Uno de los principales beneficios de usar un proxy inverso es el almacenamiento en caché. El almacenamiento en caché es una técnica para almacenar datos a los que se accede con frecuencia en una ubicación de acceso más rápido que la fuente de datos original. Al almacenar en caché los recursos, un proxy inverso puede reducir la carga en el servidor de origen y mejorar el rendimiento.

Para implementar el almacenamiento en caché, un proxy inverso debe tener una fuente de datos almacenable en caché. El tipo más común de datos almacenables en caché es el contenido estático, como archivos HTML, imágenes y hojas de estilo CSS. Un proxy inverso también puede almacenar en caché contenido dinámico, como las respuestas de una aplicación PHP. Sin embargo, el contenido dinámico es más difícil de almacenar en caché porque a menudo incluye datos personalizados o datos que cambian con frecuencia.

## Balanceo de carga

Otro beneficio de usar un proxy inverso es el equilibrio de carga. El equilibrio de carga es una técnica para distribuir la carga entre varios servidores. Al equilibrar las solicitudes de carga, un proxy inverso puede mejorar el rendimiento al distribuir la carga entre varios servidores.

El equilibrio de carga generalmente se implementa mediante un algoritmo de turno rotativo, que distribuye las solicitudes de manera uniforme entre un grupo de servidores. Sin embargo, se pueden usar otros algoritmos para distribuir la carga según la carga del servidor u otros factores.

## Seguridad

Los proxies inversos también pueden brindar seguridad al filtrar solicitudes y ocultar la identidad de los servidores. Al filtrar solicitudes, un proxy inverso puede bloquear solicitudes maliciosas antes de que lleguen al servidor de origen. Al ocultar la identidad de los servidores, un proxy inverso puede evitar que los atacantes se dirijan a servidores específicos.

## Implementación de un proxy inverso

Hay muchos paquetes de software que se pueden usar para implementar un proxy inverso. En esta sección, analizaremos cómo implementar un proxy inverso mediante el servidor web Nginx.

### Instalación de Nginx

Nginx es un servidor web gratuito y de código abierto. Se puede utilizar como proxy inverso, equilibrador de carga y caché HTTP. Nginx está disponible para muchos sistemas operativos, incluidos Linux, FreeBSD y Windows.

Para instalar Nginx en Ubuntu, use el siguiente comando:

```
sudo apt-get install nginx
```

Para instalar Nginx en CentOS, use el siguiente comando:

```
sudo yum install nginx
```

### Configuración de Nginx

El archivo de configuración predeterminado de Nginx se encuentra en /etc/nginx/nginx.conf. El archivo de configuración está dividido en secciones, con cada sección encerrada entre llaves.

La primera sección es la sección ```eventos```. La sección ```events``` define los módulos de procesamiento controlados por eventos. La sección ```eventos``` es obligatoria, pero puede estar vacía.

La segunda sección es la sección ```http```. La sección ```http``` define la configuración global para el servidor HTTP. La sección ```http``` es obligatoria.

La tercera sección es la sección ```servidor```. La sección ```servidor``` define un servidor virtual. La sección ```servidor``` es obligatoria.

La cuarta sección es la sección ```ubicación```. La sección ```ubicación``` define la configuración para una ubicación específica. La sección ```ubicación``` es opcional.

Un archivo de configuración típico de Nginx podría verse así:

```
events {
}

http {
    server {
        location / {
        }
    }
}
```

En el ejemplo anterior, la sección ```eventos``` está vacía. La sección ```http``` contiene una sección ```servidor```, que contiene una sección ```ubicación```. La sección ```ubicación``` está vacía.

### Configuración de un proxy inverso

Para configurar Nginx como proxy inverso, debemos agregar una directiva ```proxy_pass``` a la sección ```ubicación```. La directiva ```proxy_pass``` se utiliza para reenviar solicitudes a un servidor proxy. La directiva ```proxy_pass``` se puede utilizar con un servidor HTTP o FastCGI.

En el siguiente ejemplo, configuramos Nginx para que actúe como un proxy inverso para el servidor Apache HTTP. La directiva ```proxy_pass``` reenvía las solicitudes al servidor Apache.

```
events {
}

http {
    server {
        location / {
            proxy_pass http://localhost:8080;
        }
    }
}
```

En el ejemplo anterior, configuramos Nginx para que actúe como un proxy inverso para el servidor PHP-FPM. La directiva ```proxy_pass``` reenvía las solicitudes al servidor PHP-FPM.

```
events {
}

http {
    server {
        location / {
            proxy_pass http://localhost:9000;
        }
    }
}
```

## Conclusión

En este artículo, hemos discutido los beneficios de usar proxies inversos y cómo implementarlos para un mejor rendimiento. Los proxies inversos pueden mejorar el rendimiento almacenando en caché los recursos y distribuyendo la carga entre varios servidores. También pueden brindar seguridad filtrando solicitudes y ocultando la identidad de los servidores.