---
title: Operadores de Kubernetes: automatización de la gestión de aplicaciones con controladores personalizados
description: 
published: true
date: 2023-02-09T03:23:44.331Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:23:42.732Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kubernetes Operators: Automating Application Management with Custom Controllers***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-operators-automating-application-management-with-custom-controllers)
{.links-list}


# Operadores de Kubernetes: automatización de la gestión de aplicaciones con controladores personalizados

En este artículo, hablaremos sobre los operadores de Kubernetes. Kubernetes es un sistema de código abierto para automatizar aplicaciones en contenedores. Los operadores son un método para empaquetar, implementar y administrar una aplicación de Kubernetes. En este artículo, nos centraremos en qué es un Operador y cómo puede ayudarlo a automatizar la administración de sus aplicaciones.

## ¿Qué es un Operador?

Un operador es un método para empaquetar, implementar y administrar una aplicación de Kubernetes. Los operadores de Kubernetes son extensiones de software de Kubernetes que se utilizan para administrar tipos específicos de aplicaciones. Los operadores usan recursos personalizados para representar el estado de la aplicación y definir los comportamientos deseados. Los controladores personalizados observan los cambios en estos recursos personalizados y realizan los cambios necesarios para que la aplicación siga funcionando como se desea.

Los operadores se crean utilizando las API y las mejores prácticas de Kubernetes. Esto los hace portátiles entre las implementaciones de Kubernetes y permite que se extiendan fácilmente.

## ¿Por qué usar un Operador?

Los operadores ofrecen un enfoque declarativo para la gestión de aplicaciones. Esto significa que puede describir el estado deseado de una aplicación y el Operador se asegurará de que la aplicación alcance y permanezca en ese estado.

Los operadores también ofrecen una forma de automatizar la gestión de sus aplicaciones. Las aplicaciones pueden ser complejas y requieren muchos componentes diferentes para implementarse y configurarse correctamente. Este puede ser un proceso lento y propenso a errores. Los operadores pueden automatizar este proceso, haciendo que sea más fácil y rápido implementar y administrar sus aplicaciones.

Los operadores también pueden ayudarlo a administrar el ciclo de vida de sus aplicaciones. Esto incluye tareas como actualizar y degradar aplicaciones, así como ampliar o reducir las aplicaciones.

## ¿Cómo usar un Operador?

Los operadores se implementan como definiciones de recursos personalizadas (CRD). Los CRD son anotaciones que se agregan a los recursos de Kubernetes existentes. Esto permite que el Operador esté atento a los cambios en el recurso y tome las medidas necesarias.

Los operadores también se implementan como controladores personalizados. Los controladores personalizados son controladores de Kubernetes que vigilan los cambios en los recursos personalizados. Cuando se detecta un cambio, el controlador tomará las acciones necesarias para garantizar que el recurso alcance el estado deseado.

## Escribir un operador

Los operadores están escritos en Go. El SDK de operadores es un conjunto de herramientas que facilita la escritura, la creación y la implementación de operadores de Kubernetes. El SDK proporciona una CLI, andamios y herramientas de prueba.

Los operadores se crean utilizando las API y las mejores prácticas de Kubernetes. Esto los hace portátiles entre las implementaciones de Kubernetes y permite que se extiendan fácilmente.

La CLI del SDK del operador se puede utilizar para generar el andamiaje para un operador. Esto incluye la definición de recurso personalizado (CRD) y el controlador personalizado.

Una vez generado el andamiaje se puede implementar el Operador. El operador deberá estar atento a los cambios en el recurso personalizado y tomar las medidas necesarias.

Los operadores se pueden implementar en Kubernetes mediante kubectl o la CLI del SDK del operador.

## Conclusión

En este artículo, hemos discutido los operadores de Kubernetes. Hemos cubierto qué es un operador y cómo puede ayudarlo a automatizar la administración de sus aplicaciones. También hemos visto cómo escribir e implementar un Operador.