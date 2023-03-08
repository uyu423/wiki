---
title: SQL Injection
description: 
published: true
date: 2023-02-07T07:17:44.024Z
tags: 
editor: markdown
dateCreated: 2023-02-07T07:17:42.079Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [SQL Injection***English** document is available*](/en/Knowledge-base/Dictionary/sql-injection)
{.links-list}


# Descripción general
SQL Injection es un tipo de ataque cibernético que implica la inserción de código malicioso en una consulta de base de datos. Se utiliza para acceder o modificar datos confidenciales almacenados en una base de datos.

# Descripción
SQL Injection es una forma de ataque que explota las vulnerabilidades en las consultas de la base de datos. Es un tipo de ataque de inyección en el que se inserta código SQL malicioso en una consulta para obtener acceso o modificar datos confidenciales. El atacante puede usar este acceso para robar datos, modificar datos o incluso eliminar datos de la base de datos.

Los ataques de inyección SQL se pueden usar para eludir los mecanismos de autenticación, ejecutar código arbitrario e incluso obtener acceso al sistema operativo subyacente. El atacante también puede usar SQL Injection para modificar registros de la base de datos, como cambiar la contraseña de un usuario o eliminar registros.

Los ataques de inyección SQL generalmente se realizan mediante el envío de información maliciosa a una aplicación web. Esta entrada luego es procesada por la aplicación y pasada a la base de datos. Si la aplicación no valida correctamente la entrada, la base de datos puede ejecutar el código malicioso.

# Historia
Los ataques de inyección SQL han existido desde los primeros días de Internet. En 1998, el primer ataque de inyección SQL informado públicamente ocurrió en una aplicación web desarrollada por una empresa llamada Security Dynamics. Desde entonces, los ataques de inyección SQL se han vuelto cada vez más comunes y sofisticados.

# Características
Los ataques de inyección SQL generalmente se realizan mediante el envío de información maliciosa a una aplicación web. Luego, la aplicación procesa la entrada maliciosa y la pasa a la base de datos. Si la aplicación no valida correctamente la entrada, la base de datos puede ejecutar el código malicioso.

Los ataques de inyección SQL se pueden usar para eludir los mecanismos de autenticación, ejecutar código arbitrario e incluso obtener acceso al sistema operativo subyacente. El atacante también puede usar SQL Injection para modificar registros de la base de datos, como cambiar la contraseña de un usuario o eliminar registros.

# Ejemplo
Un ejemplo de un ataque de inyección SQL es un atacante que envía información maliciosa a una aplicación web. Luego, la aplicación procesa la entrada maliciosa y la pasa a la base de datos. Si la aplicación no valida correctamente la entrada, la base de datos puede ejecutar el código malicioso.

Por ejemplo, un atacante podría enviar la siguiente entrada a una aplicación web:

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

Esta entrada haría que la aplicación ejecutara la siguiente consulta:

```
SELECT * FROM users WHERE username='admin' OR '1'='1'
```

Esta consulta devolvería todos los usuarios de la base de datos, independientemente de su nombre de usuario.

# Pros y contras
Los ataques de inyección SQL tienen ventajas y desventajas. Por un lado, se pueden utilizar para acceder a datos sensibles o modificar registros en la base de datos. Por otro lado, también pueden usarse para causar un daño significativo a un sistema, como eliminar datos o ejecutar código arbitrario.

# Controversia
Los ataques de inyección SQL son un tema controvertido en la comunidad de seguridad. Algunos argumentan que son un mal necesario, ya que pueden usarse para obtener acceso a datos confidenciales y modificar registros en la base de datos. Otros argumentan que deben evitarse a toda costa, ya que pueden usarse para causar un daño significativo a un sistema.

# Tecnología relacionada
Los ataques de inyección SQL están relacionados con otros tipos de ciberataques, como Cross-Site Scripting (XSS) y Cross-Site Request Forgery (CSRF). Estos ataques también se pueden utilizar para obtener acceso a datos confidenciales o modificar registros en la base de datos.

# Digresión
Los ataques de inyección SQL son un tipo de ataque que se puede utilizar para obtener acceso o modificar datos confidenciales almacenados en una base de datos. Han existido desde los primeros días de Internet y se han vuelto cada vez más comunes y sofisticados. Si bien se pueden usar para obtener acceso a datos confidenciales o modificar registros en la base de datos, también se pueden usar para causar daños significativos a un sistema.

# Otros
Los ataques de inyección SQL se pueden prevenir validando correctamente la entrada del usuario. Esto se puede hacer mediante declaraciones preparadas y consultas parametrizadas, que garantizan que la entrada proporcionada por el usuario se trate como datos y no como código ejecutable. Además, las aplicaciones web deben probarse en busca de vulnerabilidades y parchearse regularmente para evitar ataques de inyección SQL.