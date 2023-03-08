---
title: Desarrollo de software 075: Pruebas de carga
description: 
published: true
date: 2023-02-04T20:17:29.574Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:17:24.210Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Software Development 075: Load Testing***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-075-load-testing)
{.links-list}


## Introducción

La prueba de carga es el proceso de poner demanda en un sistema o aplicación y medir su respuesta. El objetivo es determinar cómo se comporta el sistema o la aplicación en diversas condiciones de carga.

Las pruebas de carga son importantes porque pueden ayudar a identificar posibles cuellos de botella en el rendimiento del sistema o la aplicación. También puede ayudar a determinar la cantidad máxima de usuarios que puede manejar el sistema o la aplicación.

Hay muchas herramientas diferentes que se pueden utilizar para las pruebas de carga. En esta publicación, nos centraremos en Apache JMeter, que es una popular herramienta de código abierto.

## Instalación de Apache JMeter

Apache JMeter se puede descargar desde el siguiente enlace:

http://jmeter.apache.org/

Una vez que haya descargado el archivo, descomprímalo y debería ver la siguiente estructura de directorios:

```
apache-jmeter-3.1
├── bin
├── docs
├── lib
└── printable_docs
```

## Creación de un plan de prueba

Un plan de prueba es un conjunto de instrucciones que JMeter utilizará para ejecutar una prueba. El plan de prueba debe incluir los siguientes elementos:

- Grupo de subprocesos: este es un grupo de subprocesos que JMeter utilizará para ejecutar la prueba.
- Sampler: Este es un elemento que utilizará JMeter para enviar solicitudes al sistema o aplicación.
- Listener: este es un elemento que JMeter utilizará para recopilar y mostrar los resultados de la prueba.

Para crear un plan de prueba, inicie JMeter y debería ver la siguiente pantalla:

![Pantalla de inicio de JMeter](https://i.imgur.com/VkzMv9w.png)

Para agregar un grupo de subprocesos, haga clic con el botón derecho en el plan de prueba y seleccione Agregar > Subprocesos (usuarios) > Grupo de subprocesos.

![Grupo de subprocesos JMeter](https://i.imgur.com/DYUi4T4.png)

Para agregar una muestra, haga clic con el botón derecho en el grupo de subprocesos y seleccione Agregar > Muestra > Solicitud HTTP.

![Muestra de JMeter](https://i.imgur.com/iLKVLCy.png)

Para agregar un Oyente, haga clic con el botón derecho en el Grupo de subprocesos y seleccione Agregar > Oyente > Ver árbol de resultados.

![Oyente de JMeter](https://i.imgur.com/qoWql3Y.png)

## Configuración del plan de prueba

Una vez que haya agregado Thread Group, Sampler y Listener al plan de prueba, debe configurarlos.

Para configurar el Grupo de subprocesos, selecciónelo y debería ver las siguientes opciones:

![Opciones de grupo de hilos JMeter](https://i.imgur.com/g4vO4jQ.png)

- Número de subprocesos (usuarios): este es el número de subprocesos que utilizará JMeter para ejecutar la prueba.
- Recuento de bucles: esta es la cantidad de veces que JMeter ejecutará la prueba.
- Período de aceleración (en segundos): esta es la cantidad de tiempo que JMeter tardará en aumentar la cantidad de subprocesos.

Para configurar el Sampler, selecciónelo y debería ver las siguientes opciones:

![Opciones de muestra de JMeter](https://i.imgur.com/A1mlvkx.png)

- Protocolo: Este es el protocolo que utilizará JMeter para enviar la solicitud.
- Nombre del servidor o IP: este es el nombre del servidor o la dirección IP a la que JMeter enviará la solicitud.
- Número de puerto: este es el número de puerto que utilizará JMeter para enviar la solicitud.
- Ruta: Esta es la ruta que utilizará JMeter para enviar la solicitud.

Para configurar el Listener, selecciónelo y debería ver las siguientes opciones:

![Opciones de escucha de JMeter](https://i.imgur.com/OcTGiuk.png)

- Archivo de salida: este es el archivo que JMeter utilizará para generar los resultados de la prueba.
- Formato: Este es el formato en el que se mostrarán los resultados.

## Ejecutando la prueba

Una vez que haya configurado el plan de prueba, estará listo para ejecutar la prueba. Para ejecutar la prueba, seleccione el Plan de prueba y haga clic en el botón Ejecutar.

![Prueba de ejecución de JMeter](https://i.imgur.com/L1G5fvk.png)

JMeter ahora ejecutará la prueba y debería ver los resultados en el Listener.

![Resultados de la prueba de JMeter](https://i.imgur.com/Y6UgR8W.png)

## Analizando los resultados

Los resultados de la prueba se pueden analizar para determinar el rendimiento del sistema o aplicación.

Las siguientes métricas se pueden utilizar para analizar los resultados:

- Rendimiento: Este es el número de solicitudes que el sistema o aplicación puede manejar por segundo.
- Tiempo medio de respuesta: es el tiempo medio que tarda el sistema o la aplicación en responder a una solicitud.
- Percentiles: Es el porcentaje de solicitudes que tardan un cierto tiempo en responder.

## Información adicional

- Es importante tener en cuenta que las pruebas de carga no deben usarse para encontrar errores en el sistema o la aplicación.
- Las pruebas de carga se pueden utilizar para simular diferentes tipos de comportamiento del usuario.
- JMeter se puede utilizar para probar tanto aplicaciones web como servicios web.

## Referencias

-Apache JMeter: https://jmeter.apache.org/
- Tutorial de JMeter: https://www.tutorialspoint.com/jmeter/jmeter_tutorial.pdf
- Manual de usuario de JMeter: https://jmeter.apache.org/usermanual/index.html