---
title: GraphQL
description: 
published: true
date: 2023-02-11T18:17:45.384Z
tags: 
editor: markdown
dateCreated: 2023-02-11T18:17:43.544Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [GraphQL***English** document is available*](/en/Knowledge-base/Dictionary/graphql)
{.links-list}


# Descripción general
GraphQL es un lenguaje de consulta para API y un tiempo de ejecución para cumplir con esas consultas con datos existentes. Proporciona un enfoque eficiente, potente y flexible para desarrollar API web.

# Descripción
GraphQL es un lenguaje de consulta creado por Facebook en 2012 que ofrece una alternativa a REST y arquitecturas de servicios web ad-hoc. Permite a los clientes definir la estructura de los datos que necesitan, y el servidor devuelve exactamente la misma estructura de los datos. Esto elimina la necesidad de obtener varias API y reduce la obtención excesiva de datos, lo que da como resultado aplicaciones más rápidas y eficientes.

GraphQL está organizado en un sistema de tipos, que define las relaciones entre diferentes tipos de datos, y un lenguaje de consulta que permite a los clientes solicitar campos de datos específicos. El lenguaje de consulta GraphQL se utiliza para definir los datos que deben devolverse desde un servidor. Se envía una consulta de GraphQL a un punto final y el servidor responde con los datos en el formato solicitado.

GraphQL se usa a menudo en aplicaciones web y móviles, así como en arquitecturas de microservicios. También se utiliza en aplicaciones basadas en datos, como los sistemas de gestión de contenido, para definir la estructura de los datos que deben devolverse.

# Historia
GraphQL fue creado por Facebook en 2012 como una alternativa a la arquitectura REST tradicional. Inicialmente, se usó internamente en Facebook para potenciar sus aplicaciones móviles, pero luego se lanzó como código abierto en 2015. Desde entonces, GraphQL se ha vuelto cada vez más popular y ahora lo usa una amplia variedad de empresas y organizaciones.

# Características
GraphQL tiene varias características que lo convierten en una alternativa atractiva a las arquitecturas REST tradicionales. Éstas incluyen:

- Autodocumentación: GraphQL se autodocumenta, lo que significa que la estructura de los datos se define en la consulta, por lo que el servidor sabe qué datos devolver.
- Flexible: GraphQL es flexible y permite que los clientes soliciten exactamente los datos que necesitan, eliminando la necesidad de obtener varias API.
- Eficiente: las consultas de GraphQL son eficientes, ya que solo devuelven los datos que se solicitan, lo que reduce la obtención excesiva de datos.
- Sistema de tipos: GraphQL tiene un sistema de tipos que define las relaciones entre diferentes tipos de datos.

# Ejemplo
Aquí hay un ejemplo de una consulta GraphQL:

```
query {
  user(id: "123") {
    name
    age
    email
  }
}
```

Esta consulta solicita el nombre, la edad y el correo electrónico del usuario con el ID "123". El servidor luego responderá con los datos solicitados en la misma estructura que la consulta:

```
{
  "user": {
    "name": "John Doe",
    "age": 30,
    "email": "john@example.com"
  }
}
```

# Pros y contras
GraphQL tiene varias ventajas sobre las arquitecturas REST tradicionales, incluidas la flexibilidad, la eficiencia y las consultas autodocumentadas. Sin embargo, también tiene algunos inconvenientes, como la falta de estandarización y la necesidad de herramientas adicionales para implementar.

# Controversia
GraphQL ha sido objeto de cierta controversia, ya que algunos desarrolladores argumentan que es demasiado complejo y requiere herramientas adicionales para implementarlo.

# Tecnología relacionada
GraphQL se usa a menudo junto con otras tecnologías, como Apollo, una plataforma para crear aplicaciones basadas en datos.

# Digresión
GraphQL es una tecnología cada vez más popular y su uso está creciendo rápidamente.

# Otros
GraphQL es una tecnología de código abierto y su código fuente está disponible en GitHub.