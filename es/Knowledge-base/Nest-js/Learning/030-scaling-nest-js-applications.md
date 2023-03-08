---
title: 030: Escalado de aplicaciones Nest.js
description: 
published: true
date: 2023-02-15T09:32:29.455Z
tags: 
editor: markdown
dateCreated: 2023-02-15T09:32:21.972Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [030: Scaling Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/030-scaling-nest-js-applications)
{.links-list}


# Escalado de aplicaciones Nest.js

A medida que crezca su aplicación, eventualmente deberá comenzar a pensar en cómo escalarla. En este artículo, veremos algunas de las opciones disponibles para usted al escalar una aplicación Nest.js.

## Escalado horizontal

Una forma de escalar una aplicación es agregar más servidores o nodos a la aplicación. Esto se conoce como escalado horizontal.

Agregar más nodos a una aplicación tiene algunos beneficios. Primero, permite que la aplicación maneje más tráfico. En segundo lugar, puede mejorar el rendimiento, ya que cada nodo puede gestionar las solicitudes de forma independiente.

Hay algunas cosas a tener en cuenta al escalar horizontalmente. Primero, deberá asegurarse de que cada nodo tenga una identificación única. Esto es para que el balanceador de carga pueda enviar tráfico al nodo correcto.

En segundo lugar, deberá asegurarse de que los nodos no tengan estado. Esto significa que cada nodo puede manejar cualquier solicitud, independientemente del estado de los otros nodos.

En tercer lugar, deberá utilizar un equilibrador de carga. Un equilibrador de carga es una pieza de software que se encuentra frente a la aplicación y enruta el tráfico a los diferentes nodos.

Hay algunas opciones diferentes disponibles para los balanceadores de carga, pero usaremos nginx en este ejemplo.

En cuarto lugar, deberá asegurarse de que los nodos puedan comunicarse entre sí. Esto es para que puedan compartir información, como datos de sesión.

Finalmente, deberá asegurarse de que los nodos se puedan agregar y eliminar dinámicamente. Esto es para que la aplicación se pueda ampliar o reducir según sea necesario.

## Escalando verticalmente

Otra forma de escalar una aplicación es agregar más recursos a un solo nodo. Esto se conoce como escalado vertical.

Agregar más recursos a un nodo tiene algunos beneficios. Primero, permite que el nodo maneje más tráfico. En segundo lugar, puede mejorar el rendimiento, ya que el nodo tiene más recursos para trabajar.

Hay algunas cosas a tener en cuenta al escalar verticalmente. Primero, deberá asegurarse de que el nodo se pueda agregar y eliminar dinámicamente. Esto es para que la aplicación se pueda ampliar o reducir según sea necesario.

En segundo lugar, deberá asegurarse de que el nodo se pueda actualizar sin afectar a los otros nodos. Esto es para que pueda agregar más recursos al nodo sin afectar el rendimiento de los otros nodos.

En tercer lugar, deberá asegurarse de que el nodo se pueda degradar sin afectar a los otros nodos. Esto es para que pueda eliminar recursos del nodo sin afectar el rendimiento de los otros nodos.

En cuarto lugar, deberá asegurarse de que el nodo se pueda migrar sin afectar a los demás nodos. Esto es para que pueda mover el nodo a un servidor diferente sin afectar el rendimiento de los otros nodos.

Finalmente, deberá asegurarse de que el nodo se pueda replicar sin afectar a los otros nodos. Esto es para que pueda crear una copia del nodo en otro servidor sin afectar el rendimiento de los otros nodos.

## Conclusión

Escalar una aplicación es una parte importante del crecimiento de un negocio. Hay algunas opciones diferentes disponibles para usted al escalar una aplicación Nest.js. Puede escalar horizontalmente agregando más nodos a la aplicación, o puede escalar verticalmente agregando más recursos a un solo nodo.