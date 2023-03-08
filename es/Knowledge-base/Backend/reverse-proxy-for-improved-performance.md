---
title: Proxy inverso para mejorar el rendimiento
description: 
published: true
date: 2023-02-14T23:17:17.195Z
tags: 
editor: markdown
dateCreated: 2023-02-14T23:17:14.909Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Reverse Proxy for Improved Performance***English** document is available*](/en/Knowledge-base/Backend/reverse-proxy-for-improved-performance)
{.links-list}


# Proxy inverso para mejorar el rendimiento

Los servidores proxy web actúan como intermediarios entre los clientes y otros servidores. Un cliente se conecta al servidor proxy y solicita algún servicio, como un archivo, conexión, página web u otro recurso, disponible en un servidor diferente. El servidor proxy evalúa la solicitud de acuerdo con sus reglas de filtrado. Por ejemplo, puede verificar si el sitio solicitado está bloqueado en el país del usuario. Si el servidor proxy aprueba la solicitud, se conecta al sitio solicitado, descarga la página y la almacena en su propio caché. Cuando el usuario vuelve a solicitar la misma página, el servidor proxy devuelve la página almacenada en caché, lo que reduce la carga del servidor y mejora el tiempo de respuesta.

Un proxy inverso es un tipo de servidor proxy que recupera recursos en nombre de un cliente de uno o más servidores. Un proxy inverso acepta solicitudes de uno o más clientes y las reenvía al servidor backend adecuado. Un proxy inverso puede distribuir la carga de un solo cliente a varios servidores, lo que mejora el rendimiento.

Hay varias razones para usar un proxy inverso:

* **Rendimiento**: Al almacenar en caché el contenido estático y manejar las solicitudes dinámicas por separado, un proxy inverso puede mejorar el rendimiento de un servidor web.

* **Seguridad**: un proxy inverso puede ofrecer una capa adicional de seguridad al filtrar las solicitudes y bloquear las maliciosas.

* **Compatibilidad**: un proxy inverso puede mediar entre diferentes servidores back-end que usan diferentes tecnologías, lo que hace que parezca que usan una única tecnología unificada.

## Configuración de un proxy inverso

Hay una serie de paquetes de software que se pueden utilizar para configurar un proxy inverso. En esta sección, utilizaremos el servidor web NGINX.

 NGINX es un servidor HTTP gratuito, de código abierto y de alto rendimiento y un proxy inverso, así como un servidor proxy IMAP/POP3. NGINX es conocido por su alto rendimiento, estabilidad, amplio conjunto de funciones, configuración simple y bajo consumo de recursos.

Primero, instale NGINX usando su administrador de paquetes. Por ejemplo, en distribuciones basadas en Debian:

```
$ sudo apt-get install nginx
```

A continuación, cree un archivo en el directorio de configuración de NGINX, `/etc/nginx/conf.d/`, con el siguiente contenido:

```
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://localhost:8080;
    }
}
```

Este archivo configura NGINX para escuchar en el puerto 80 las solicitudes a `example.com` y para reenviar esas solicitudes a `localhost:8080`.

Finalmente, inicie NGINX:

```
$ sudo systemctl start nginx
```

## Conclusión

Un proxy inverso puede mejorar el rendimiento de un servidor web almacenando en caché el contenido estático y gestionando las solicitudes dinámicas por separado. Un proxy inverso también puede ofrecer una capa adicional de seguridad al filtrar las solicitudes y bloquear las maliciosas.