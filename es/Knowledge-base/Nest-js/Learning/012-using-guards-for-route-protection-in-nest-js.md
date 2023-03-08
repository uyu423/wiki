---
title: 012: uso de guardias para la protección de rutas en Nest.js
description: 
published: true
date: 2023-02-14T22:32:14.192Z
tags: 
editor: markdown
dateCreated: 2023-02-14T22:32:12.576Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [012: Using guards for route protection in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/012-using-guards-for-route-protection-in-nest-js)
{.links-list}


# Uso de guardias para la protección de rutas en Nest.js

En esta publicación, veremos cómo usar guardias en Nest.js para proteger las rutas. Comenzaremos con una comprensión básica de qué son los protectores y cómo funcionan, y luego veremos cómo usarlos para proteger nuestras rutas.

## ¿Qué son los guardias?

Los guardias son funciones que se pueden utilizar para proteger las rutas. Se pueden usar para verificar si un usuario ha iniciado sesión, si tiene los permisos necesarios o si cumple con otros criterios. Si no se cumplen los criterios, el vigilante impedirá al usuario acceder a la ruta.

## ¿Cómo funcionan los guardias?

Los guardias están registrados con Nest.js como middleware. Esto significa que se ejecutarán antes que el controlador de ruta. Si el guardia devuelve `verdadero`, la ruta será accesible. Si el guardia devuelve `falso`, la ruta será inaccesible.

## ¿Cómo se pueden usar guardias para proteger las rutas?

Los protectores se pueden usar para proteger las rutas de varias maneras. Por ejemplo, se puede usar un guardia para verificar si un usuario ha iniciado sesión antes de permitirle acceder a una ruta. Si el usuario no está logueado, el vigilante le impedirá acceder a la ruta.

Otra forma de usar guardias es verificar si un usuario tiene los permisos necesarios antes de permitirle acceder a una ruta. Por ejemplo, si una ruta requiere que un usuario sea administrador, se puede usar un guardia para verificar si el usuario tiene el permiso `admin`. Si no tienen el permiso, el vigilante les impedirá acceder a la ruta.

## Conclusión

En esta publicación, analizamos cómo usar guardias en Nest.js para proteger las rutas. Los guardias son funciones que se pueden usar para verificar si un usuario cumple con los criterios necesarios antes de permitirle acceder a una ruta. Se pueden usar para verificar si un usuario ha iniciado sesión, si tiene los permisos necesarios o si cumple con otros criterios.