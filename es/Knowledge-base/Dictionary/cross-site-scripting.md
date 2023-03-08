---
title: Cross-Site Scripting
description: 
published: true
date: 2023-02-16T20:55:37.408Z
tags: 
editor: markdown
dateCreated: 2023-02-16T20:55:34.826Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Cross-Site Scripting***English** document is available*](/en/Knowledge-base/Dictionary/cross-site-scripting)
{.links-list}


# Descripción general
Cross-site scripting (XSS) es un tipo de vulnerabilidad de seguridad informática que permite a los atacantes inyectar código malicioso en páginas web vistas por otros usuarios. Los ataques XSS generalmente se usan para robar datos, secuestrar sesiones de usuarios o redirigir a los usuarios a sitios web maliciosos.

# Descripción
Cross-site scripting (XSS) es un tipo de vulnerabilidad de seguridad informática que se produce cuando un atacante puede inyectar código malicioso en una página web visitada por otros usuarios. Los ataques XSS generalmente se usan para robar datos, secuestrar sesiones de usuarios o redirigir a los usuarios a sitios web maliciosos.

Los ataques XSS explotan la confianza que los navegadores web tienen en los sitios web que visitan. El código malicioso suele estar incrustado en un enlace o una etiqueta de imagen, y cuando el usuario hace clic en el enlace o la imagen, se ejecuta el código malicioso.

Los ataques XSS se pueden dividir en dos grandes categorías: XSS almacenado y XSS reflejado. En un ataque XSS almacenado, el código malicioso se almacena en el servidor y se ejecuta cuando un usuario visita la página. En un ataque XSS reflejado, el código malicioso no se almacena en el servidor, sino que se refleja al usuario en la respuesta.

Los ataques XSS se pueden prevenir mediante la validación de entrada, la codificación de salida y otras medidas de seguridad. Además, los desarrolladores web deben ser conscientes de los riesgos potenciales que plantean los ataques XSS y tomar medidas para proteger sus sitios web.

# Historia
Las secuencias de comandos entre sitios se descubrieron por primera vez a fines de la década de 1990, cuando un investigador de seguridad descubrió que se podía inyectar código malicioso en las páginas web mediante el uso de campos de formulario HTML. Desde entonces, los ataques XSS se han vuelto cada vez más sofisticados y generalizados.

En 2004, se lanzó el primer gran ataque XSS contra el popular sitio web de redes sociales MySpace. El ataque se utilizó para propagar código malicioso entre millones de usuarios, lo que resultó en el robo de datos de usuarios y el secuestro de cuentas de usuarios.

# Características
Los ataques XSS explotan la confianza que los navegadores web tienen en los sitios web que visitan. El código malicioso suele estar incrustado en un enlace o una etiqueta de imagen, y cuando el usuario hace clic en el enlace o la imagen, se ejecuta el código malicioso.

Los ataques XSS se pueden dividir en dos grandes categorías: XSS almacenado y XSS reflejado. En un ataque XSS almacenado, el código malicioso se almacena en el servidor y se ejecuta cuando un usuario visita la página. En un ataque XSS reflejado, el código malicioso no se almacena en el servidor, sino que se refleja al usuario en la respuesta.

Los ataques XSS se pueden usar para robar datos, secuestrar sesiones de usuario o redirigir a los usuarios a sitios web maliciosos.

# Ejemplo
Un ejemplo de un ataque XSS almacenado sería un atacante que incrusta un código malicioso en un comentario en una publicación de blog. Cuando un usuario visita la publicación del blog, se ejecuta el código malicioso y el atacante puede robar datos o secuestrar la sesión del usuario.

# Pros y contras
La principal ventaja de los ataques XSS es que permiten a los atacantes inyectar código malicioso en las páginas web vistas por otros usuarios. Esto se puede usar para robar datos, secuestrar sesiones de usuarios o redirigir a los usuarios a sitios web maliciosos.

La principal desventaja de los ataques XSS es que pueden ser difíciles de detectar y prevenir. Los ataques XSS explotan la confianza que los navegadores web tienen en los sitios web que visitan y, como tal, pueden ser difíciles de detectar y prevenir.

# Controversia
Los ataques XSS han sido una fuente de controversia en la comunidad de seguridad. Algunos argumentan que los ataques XSS son un mal necesario, ya que permiten a los investigadores descubrir posibles vulnerabilidades de seguridad en las aplicaciones web. Otros argumentan que los ataques XSS son demasiado peligrosos para ser utilizados como herramienta de prueba de seguridad.

# Tecnología relacionada
Los ataques XSS están relacionados con otros tipos de vulnerabilidades de seguridad de aplicaciones web, como la inyección SQL y la falsificación de solicitudes entre sitios (CSRF).

# Digresión
Los ataques XSS también se pueden usar para propagar código malicioso, como malware, a través de la web.

# Otros
Los ataques XSS se pueden prevenir mediante la validación de entrada, la codificación de salida y otras medidas de seguridad. Además, los desarrolladores web deben ser conscientes de los riesgos potenciales que plantean los ataques XSS y tomar medidas para proteger sus sitios web.