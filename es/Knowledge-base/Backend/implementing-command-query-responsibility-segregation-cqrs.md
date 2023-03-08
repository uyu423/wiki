---
title: Implementación de la segregación de responsabilidad de consultas de comandos (CQRS)
description: 
published: true
date: 2023-02-10T03:55:28.003Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:55:26.375Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing Command Query Responsibility Segregation (CQRS)***English** document is available*](/en/Knowledge-base/Backend/implementing-command-query-responsibility-segregation-cqrs)
{.links-list}


# Implementación de la segregación de responsabilidad de consultas de comandos (CQRS)

En los últimos años, la popularidad de los microservicios ha llevado a un resurgimiento del interés en el patrón Command Query Responsibility Segregation (CQRS). CQRS es un patrón que se puede usar para diseñar aplicaciones como un conjunto de servicios independientes, cada uno responsable de una sola tarea.

El beneficio clave de usar CQRS es que puede hacer que las aplicaciones sean más escalables y fáciles de mantener. Cuando se implementa correctamente, CQRS también puede hacer que las aplicaciones sean más predecibles y fáciles de entender.

En este artículo, veremos más de cerca el patrón CQRS y cómo se puede usar para crear aplicaciones escalables y mantenibles. También veremos algunos de los desafíos que deben tenerse en cuenta al implementar CQRS.

## ¿Qué es CQRS?

Command Query Responsibility Segregation (CQRS) es un patrón que se puede utilizar para diseñar aplicaciones como un conjunto de servicios independientes, cada uno responsable de una sola tarea.

El término "Segregación de responsabilidad de consulta de comando" fue acuñado por primera vez por Greg Young en una publicación de blog en 2010. En esta publicación, Greg describió CQRS como "una técnica que escuché describir por primera vez a Eric Evans en su libro Diseño basado en dominios".

El patrón CQRS tiene sus raíces en la comunidad de diseño controlado por dominio (DDD) y, a menudo, se usa junto con otros patrones DDD, como el abastecimiento de eventos.

En esencia, el patrón CQRS es simple: implica dividir una aplicación en dos partes separadas, una responsable de manejar los comandos (también conocidas como escrituras) y la otra responsable de manejar las consultas (también conocidas como lecturas).

### Comandos

Los comandos son solicitudes para cambiar el estado del sistema. Por lo general, se desencadenan por las interacciones del usuario, como hacer clic en un botón o enviar un formulario.

Los comandos suelen ser procesados por un controlador de comandos, que es un fragmento de código responsable de validar el comando y aplicar los cambios al sistema.

### Consultas

Las consultas son solicitudes de información del sistema. Por lo general, se desencadenan por las interacciones del usuario, como cargar una página o realizar una búsqueda.

Las consultas generalmente son procesadas por un controlador de consultas, que es un fragmento de código responsable de obtener los datos del sistema y devolverlos al usuario.

El patrón CQRS a menudo se describe como una separación de preocupaciones, ya que separa la responsabilidad de manejar los comandos de la responsabilidad de manejar las consultas.

## Los beneficios de CQRS

El patrón CQRS puede ofrecer una serie de beneficios, tanto en términos de rendimiento técnico como de productividad del desarrollador.

### desempeño mejorado

Uno de los principales beneficios de CQRS es el rendimiento mejorado. Al dividir la aplicación en dos partes separadas, puede ser más fácil escalar la aplicación horizontalmente.

Por ejemplo, si la aplicación recibe mucho tráfico, la parte de consulta de la aplicación se puede escalar agregando más servidores de consulta. La parte de comando de la aplicación se puede escalar agregando más servidores de comando.

### previsibilidad mejorada

Otro beneficio de CQRS es la previsibilidad mejorada. Cuando una aplicación se divide en dos partes separadas, puede ser más fácil entender cómo funciona la aplicación. Esto se debe a que las responsabilidades de cada parte están claramente definidas.

### productividad mejorada

CQRS también puede mejorar la productividad de los desarrolladores. Al dividir la aplicación en dos partes, puede ser más fácil realizar cambios en la aplicación sin afectar la otra parte.

Por ejemplo, si se realiza un cambio en la forma en que se procesan los comandos, no afectará la forma en que se procesan las consultas. Esto puede facilitar y acelerar la implementación de cambios en la aplicación.

## Los desafíos de CQRS

Si bien el patrón CQRS puede ofrecer una serie de beneficios, también hay una serie de desafíos que deben tenerse en cuenta al implementar CQRS.

### mayor complejidad

Uno de los principales desafíos de CQRS es la mayor complejidad. Cuando una aplicación se divide en dos partes, puede ser más difícil entender cómo funciona la aplicación. Esto se debe a que las responsabilidades de cada parte no siempre están claras.

### mayor tiempo de desarrollo

Otro desafío de CQRS es el aumento del tiempo de desarrollo. Cuando una aplicación se divide en dos partes, puede llevar más tiempo desarrollarla. Esto se debe a que el equipo de desarrollo necesita desarrollar tanto la parte de comando como la parte de consulta de la aplicación.

### aumento de los gastos generales operativos

Otro desafío de CQRS es el aumento de los gastos generales operativos. Cuando una aplicación se divide en dos partes, puede ser más difícil operar la aplicación. Esto se debe a que el equipo operativo necesita administrar tanto la parte de comando como la parte de consulta de la aplicación.

## Conclusión

En este artículo, analizamos el patrón CQRS y cómo se puede utilizar para crear aplicaciones escalables y mantenibles. También analizamos algunos de los desafíos que deben tenerse en cuenta al implementar CQRS.

Si bien el patrón CQRS puede ofrecer varios beneficios, no es adecuado para todas las aplicaciones. La decisión de usar o no CQRS debe tomarse caso por caso.

## Referencias

- [CQRS](https://martinfowler.com/bliki/CQRS.html)
- [Segregación de responsabilidad de consulta de comando] (https://en.wikipedia.org/wiki/Command_query_responsibility_segregation)
- [gregoryyoung/m-r](https://github.com/gregoryyoung/m-r)
- [Weblog de Amit Sheth](https://amitsheth.wordpress.com/2014/02/18/what-is-cqrs/)