---
title: 078: Integración de Spring Boot con Apache Cassandra para la gestión de datos distribuidos
description: 
published: true
date: 2023-02-05T09:32:41.473Z
tags: 
editor: markdown
dateCreated: 2023-02-05T09:32:39.733Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [078: Integrating Spring Boot with Apache Cassandra for Distributed Data Management***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/078-integrating-spring-boot-with-apache-cassandra-for-distributed-data-management)
{.links-list}


# 078: Integrando Spring Boot con Apache Cassandra para la Gestión de Datos Distribuidos

## Introducción

En esta publicación, veremos cómo integrar [Spring Boot](https://spring.io/projects/spring-boot) con [Apache Cassandra](http://cassandra.apache.org/) para distribución gestión de datos.

Cassandra es una base de datos NoSQL altamente escalable que es adecuada para el almacenamiento y la gestión de datos a gran escala. Spring Boot es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

## Resumen de Casandra

Cassandra es una base de datos NoSQL diseñada para alta disponibilidad y escalabilidad. Es una opción popular para el almacenamiento y la gestión de datos a gran escala.

Cassandra es una base de datos [sin maestro] (https://en.wikipedia.org/wiki/Masterless_architecture), lo que significa que no hay un único punto de falla. Los datos se replican en varios nodos del clúster de Cassandra, y cada nodo puede actuar como un [nodo inicial](http://docs.datastax.com/en/cassandra/3.x/cassandra/initialize/initializeSingleDS.html) para otros nodos.

Cassandra también es [escalable linealmente] (https://en.wikipedia.org/wiki/Linear_scalability), lo que significa que puede manejar una carga creciente al agregar más nodos al clúster.

## Modelo de datos de Cassandra

Cassandra usa un modelo de datos [orientado a columnas](https://en.wikipedia.org/wiki/Column-oriented_DBMS). Los datos se organizan en [familias de columnas](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlAboutDataModels.html), que son similares a las tablas de una base de datos relacional.

Cada familia de columnas tiene una [clave principal](http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlPrimaryKeyConcept.html), que se usa para identificar de manera única una fila de datos. Una clave principal se compone de una o más [columnas] (http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlColumns.html).

Cassandra también admite [índices secundarios] (http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlIndexesConcept.html), que se pueden usar para consultar datos en una familia de columnas por una columna que no es parte de la clave principal.

## Lenguaje de consulta de Cassandra

Cassandra usa un [lenguaje de consulta similar a SQL] (http://docs.datastax.com/en/cassandra/3.x/cassandra/dml/dmlSelect.html) llamado CQL (Cassandra Query Language) que se usa para consultar y actualizar datos en una base de datos Cassandra.

CQL es similar a SQL, pero no es una base de datos SQL totalmente compatible. Hay algunas [diferencias](http://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlCommandsTOC.html) entre CQL y SQL que debe tener en cuenta al trabajar con Cassandra.

## Resumen de arranque de primavera

[Spring Boot](https://spring.io/projects/spring-boot) es un marco Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

Spring Boot se basa en [Spring framework](https://spring.io/projects/spring-framework), que es un popular marco de aplicación de Java. Spring Boot facilita la creación de aplicaciones basadas en Spring proporcionando una [configuración predeterminada](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-external-config.html ) y [dependencias iniciales](https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-maven-guides.html# getting-started-with-maven-dependency-management ) que se puede utilizar para crear una variedad de aplicaciones.

## Spring Boot y Cassandra

Spring Boot facilita la [integración](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html# boot-features-nosql-cassandra) con Cassandra . Spring Boot proporciona una [configuración automática de Cassandra] (https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-nosql.html#boot-features-nosql-cassandra) que se puede utilizar para configurar y conectarse a una base de datos de Cassandra.

Spring Boot también proporciona un objeto [CassandraTemplate](https://docs.spring.io/spring-data/cassandra/docs/current/api/org/springframework/data/cassandra/core/CassandraTemplate.html) que se puede usar para consultar y actualizar datos en una base de datos Cassandra.

## Empezando

En esta sección, veremos cómo comenzar con Spring Boot y Cassandra. Comenzaremos creando un nuevo proyecto Spring Boot usando [Spring Initializr](https://start.spring.io/).

Tendremos que agregar las siguientes dependencias a nuestro proyecto:

- Web - Se usa para agregar un servidor web a nuestra aplicación
- Cassandra: se utiliza para conectarse a una base de datos de Cassandra

También necesitaremos agregar las siguientes dependencias de Maven a nuestro proyecto:

- [Controlador de Cassandra](https://mvnrepository.com/artifact/org.apache.cassandra/cassandra-driver-core) - Se usa para conectarse a una base de datos de Cassandra
- [Unidad de Cassandra] (https://mvnrepository.com/artifact/org.cassandraunit/cassandra-unit) - Se usa para probar unitariamente nuestro código de Cassandra

## Configuración de Cassandra

En esta sección, veremos cómo configurar Cassandra para nuestra aplicación Spring Boot.

Comenzaremos agregando un archivo [Configuración de Cassandra](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-configuration) a nuestro proyecto. Este archivo se usará para configurar nuestra conexión Cassandra.

Tendremos que establecer las siguientes propiedades en nuestro archivo de configuración:

- `cassandra.contact-points` - Los puntos de contacto de Cassandra que nuestra aplicación usará para conectarse al clúster de Cassandra
- `cassandra.port` - El puerto en el que se ejecuta nuestro clúster de Cassandra
- `cassandra.keyspace-name` - El nombre del espacio de claves que usará nuestra aplicación
- `cassandra.username` - El nombre de usuario que usará nuestra aplicación para conectarse a Cassandra
- `cassandra.password` - La contraseña que usará nuestra aplicación para conectarse a Cassandra

## Creando una Entidad Cassandra

En esta sección, veremos cómo crear una clase de [entidad Cassandra](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# cassandra-mapping-entity) .

Las entidades de Cassandra son similares a las [entidades JPA] (https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# orm-support.jpa.entity). Se utilizan para asignar una tabla Cassandra a una clase Java.

Tendremos que anotar nuestra clase de entidad Cassandra con la anotación `@Table`. Esta anotación se usa para especificar el nombre de la tabla Cassandra a la que se asignará nuestra entidad.

También necesitaremos anotar nuestra clase de entidad con la anotación `@PrimaryKeyClass`. Esta anotación se usa para especificar la clase de clave principal para nuestra entidad.

Nuestra clase de clave principal deberá anotar la anotación `@PrimaryKeyColumn` para cada columna de clave principal. Esta anotación se usa para especificar el nombre de la columna y el orden en que se usará en la clave principal.

## Crear un repositorio de Cassandra

En esta sección, veremos cómo crear un [repositorio de Cassandra](https://docs.spring.io/spring-data/cassandra/docs/current/reference/html/# repositories.query-methods.details ) interfaz.

Los repositorios de Cassandra son similares a los [repositorios JPA] (https://docs.spring.io/spring-data/jpa/docs/current/reference/html/# repositories). Se utilizan para acceder a datos en una base de datos de Cassandra.

Tendremos que anotar nuestra interfaz de repositorio de Cassandra con la anotación `@Repository`. Esta anotación se usa para marcar nuestra interfaz como un repositorio de Spring Data.

También necesitaremos anotar nuestra interfaz de repositorio con la anotación `@CassandraRepository`. Esta anotación se usa para marcar nuestra interfaz como un repositorio de Cassandra.

Podemos usar la anotación `@Query` en nuestros métodos de repositorio para especificar una consulta CQL. También podemos usar la anotación `@Param` para vincular los parámetros del método a los parámetros de consulta CQL.

## Prueba unitaria del código de Cassandra

En esta sección, veremos cómo probar unitariamente nuestro código Cassandra.

Comenzaremos anotando nuestra clase de prueba con la anotación `@RunWith(CassandraUnitRunner.class)`. Esta anotación se usa para ejecutar nuestras pruebas unitarias con el corredor Cassandra Unit.

También necesitaremos anotar nuestra clase de prueba con la anotación `@CassandraDataSet`. Esta anotación se usa para cargar un conjunto de datos de Cassandra en nuestro entorno de prueba.

Podemos usar la anotación `@EmbeddedCassandra` para iniciar un servidor Cassandra integrado para nuestras pruebas unitarias. También podemos usar la anotación `@SharedEmbeddedCassandra` para iniciar un servidor Cassandra integrado compartido para nuestras pruebas unitarias.

## Conclusión

En esta publicación, analizamos cómo integrar Spring Boot con Cassandra para la administración de datos distribuidos. Comenzamos observando el modelo de datos y el lenguaje de consulta de Cassandra. Luego, analizamos cómo comenzar con Spring Boot y Cassandra.

Luego, analizamos cómo configurar Cassandra para nuestra aplicación Spring Boot. También hemos visto cómo crear una clase de entidad de Cassandra y una interfaz de repositorio de Cassandra.

Finalmente, hemos visto cómo probar unitariamente nuestro código Cassandra.