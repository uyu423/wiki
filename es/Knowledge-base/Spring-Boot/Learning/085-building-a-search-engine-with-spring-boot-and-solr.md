---
title: 085: Construcción de un motor de búsqueda con Spring Boot y Solr
description: 
published: true
date: 2023-02-05T15:33:30.480Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:33:24.898Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [085: Building a Search Engine with Spring Boot and Solr***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}


# 085: Construyendo un Motor de Búsqueda con Spring Boot y Solr

En esta publicación, le mostraremos cómo crear un motor de búsqueda usando [Spring Boot](https://spring.io/projects/spring-boot) y [Apache Solr](https://lucene.apache.org /solr/).

## ¿Qué es un motor de búsqueda?

Un motor de búsqueda es una herramienta basada en la web que permite a los usuarios encontrar información en Internet. Los motores de búsqueda usan algoritmos para rastrear e indexar páginas web, y usan heurística para proporcionar resultados de búsqueda relevantes a los usuarios.

Hay muchos tipos diferentes de motores de búsqueda, pero los más populares son los motores de búsqueda de propósito general como Google, Yahoo y Bing. Estos motores de búsqueda permiten a los usuarios buscar cualquier cosa en Internet.

## ¿Qué es Apache Solr?

[Apache Solr](https://lucene.apache.org/solr/) es una popular plataforma de búsqueda empresarial de código abierto que se basa en [Apache Lucene](https://lucene.apache.org/). Solr es utilizado por muchas organizaciones grandes, incluidas Adobe, CNET y eBay.

Solr es un servidor de búsqueda independiente que proporciona una API similar a REST para administrar índices y realizar búsquedas. Solr es altamente escalable y se puede implementar de forma distribuida.

## ¿Por qué usar Solr?

Hay muchas razones para usar Solr, pero algunas de las más populares son:

- **Solr es rápido**: Solr está diseñado para ser rápido, con baja latencia y alto rendimiento.
- **Solr es escalable**: Solr es altamente escalable y se puede implementar de forma distribuida.
- **Solr tiene muchas funciones**: Solr proporciona muchas funciones listas para usar, incluidas la búsqueda de texto completo, la búsqueda por facetas y el resaltado de coincidencias.

## Requisitos previos

Antes de comenzar, hay algunas cosas que debe tener para poder seguir esta publicación:

- **Java 8** o superior: puede descargar Java desde el [sitio web de Oracle](https://www.oracle.com/java/technologies/javase-downloads.html).
- **Maven**: Puede instalar Maven desde el [sitio web de Apache Maven](https://maven.apache.org/install.html).
- **Git**: puede instalar Git desde el [sitio web de Git](https://git-scm.com/downloads).

## Empezando

En esta sección, veremos los pasos necesarios para poner en marcha nuestro motor de búsqueda.

### Paso 1: crear un proyecto Spring Boot

Lo primero que debemos hacer es crear un nuevo proyecto Spring Boot. Podemos hacer esto usando [Spring Initializr](https://start.spring.io/).

Tendremos que especificar la siguiente información:

- **Grupo**: Este es el ID de grupo para nuestro proyecto. Usaremos `com.example`.
- **Artefacto**: Este es el ID del artefacto para nuestro proyecto. Usaremos `motor de búsqueda`.
- **Nombre**: Este es el nombre de nuestro proyecto. Usaremos `Motor de búsqueda`.
- **Descripción**: Esta es la descripción de nuestro proyecto. Usaremos `Un motor de búsqueda creado con Spring Boot y Solr`.
- **Nombre del paquete**: Este es el nombre del paquete para nuestro proyecto. Usaremos `com.example.search`.
- **Empaque**: Este es el tipo de empaque para nuestro proyecto. Usaremos `jar`.
- **Versión de Java**: Esta es la versión de Java para nuestro proyecto. Usaremos `8`.
- **Dependencias**: Estas son las dependencias de nuestro proyecto. Tendremos que agregar las siguientes dependencias:
  - `Web`: Esta dependencia agrega soporte para desarrollo web.
  - `Solr`: Esta dependencia agrega soporte para Apache Solr.

Una vez que tengamos toda la información completada, podemos hacer clic en el botón `Generar proyecto` para descargar nuestro proyecto.

### Paso 2: Configurar Solr

A continuación, debemos configurar Solr. Podemos hacer esto creando un archivo llamado `solr.xml` en el directorio `src/main/resources` de nuestro proyecto.

El archivo `solr.xml` debería verse así:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<solr>
  <solrcloud>
    <solrcloud>
      <zkHost>localhost:9983</zkHost>
    </solrcloud>
  </solrcloud>
  <shards>
    <shard>
      <name>shard1</name>
      <replicas>
        <replica>
          <name>replica1</name>
          <nodeName>node1</nodeName>
          <dataDir>data/shard1/replica1</dataDir>
        </replica>
      </replicas>
    </shard>
  </shards>
</solr>
```

En el archivo `solr.xml`, configuramos Solr para usar [ZooKeeper](https://zookeeper.apache.org/) para la coordinación y definimos un solo fragmento con una sola réplica.

### Paso 3: Crear un núcleo Solr

A continuación, necesitamos crear un núcleo Solr. Un núcleo de Solr es una instancia en ejecución de Solr que contiene una colección de documentos.

Podemos crear un núcleo Solr ejecutando el siguiente comando:

```
solr create -c <corename>
```

Para nuestro ejemplo, usaremos el nombre `motor de búsqueda`.

### Paso 4: configurar Spring Boot

Ahora que tenemos nuestro núcleo Solr creado, necesitamos configurar Spring Boot para usarlo. Podemos hacer esto agregando la siguiente configuración al archivo `application.properties`:

```properties
spring.data.solr.host=http://localhost:8983/solr/search-engine
```

En la configuración, hemos especificado la URL de nuestro núcleo Solr.

### Paso 5: Crear un documento

Ahora que tenemos nuestro núcleo Solr configurado, podemos agregarle documentos. Un documento es una unidad de información que Solr puede indexar.

Crearemos un documento creando una nueva clase Java llamada `SearchDocument` en el paquete `com.example.search.document`. La clase `SearchDocument` debería verse así:

```java
package com.example.search.document;

import org.apache.solr.client.solrj.beans.Field;
import org.springframework.data.annotation.Id;
import org.springframework.data.solr.core.mapping.SolrDocument;

@SolrDocument(solrCoreName = "search-engine")
public class SearchDocument {

    @Id
    @Field
    private String id;

    @Field
    private String title;

    @Field
    private String content;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

En la clase `SearchDocument`, hemos anotado la clase con la anotación `@SolrDocument` para indicar que es un documento de Solr. También hemos anotado los campos `id`, `title` y `content` con la anotación `@Field` para indicar que deben ser indexados por Solr.

### Paso 6: Crear un servicio

Ahora que tenemos nuestro documento creado, necesitamos crear un servicio que pueda indexarlo. Crearemos una nueva interfaz Java llamada `SearchService` en el paquete `com.example.search.service`. La interfaz `SearchService` debería verse así:

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;

public interface SearchService {

    void indexDocument(SearchDocument document);

}
```

En la interfaz `SearchService`, hemos definido un único método llamado `indexDocument` que acepta un objeto `SearchDocument` y lo indexa.

A continuación, crearemos una implementación de la interfaz `SearchService` llamada `SearchServiceImpl`. La clase `SearchServiceImpl` debería verse así:

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;
import org.apache.solr.client.solrj.SolrClient;
import org.apache.solr.client.solrj.SolrServerException;
import org.apache.solr.common.SolrInputDocument;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;

@Service
public class SearchServiceImpl implements SearchService {

    @Autowired
    private SolrClient solrClient;

    @Override
    public void indexDocument(SearchDocument document) {
        SolrInputDocument solrInputDocument = new SolrInputDocument();
        solrInputDocument.addField("id", document.getId());
        solrInputDocument.addField("title", document.getTitle());
        solrInputDocument.addField("content", document.getContent());

        try {
            solrClient.add(solrInputDocument);
            solrClient.commit();
        } catch (SolrServerException | IOException e) {
            // log error
        }
    }
}
```

En la clase `SearchServiceImpl`, hemos inyectado un objeto `SolrClient`. El objeto `SolrClient` se utiliza para interactuar con un servidor Solr.

También hemos implementado el método `indexDocument`. En el método `indexDocument`, hemos creado un objeto `SolrInputDocument` y le hemos agregado los campos del objeto `SearchDocument`.

Finalmente, agregamos `SolrInputDocument` a `SolrClient` y confirmamos los cambios.

### Paso 7: Crear un controlador

Ahora que tenemos nuestro servicio creado, necesitamos crear un controlador que pueda indexar documentos. Crearemos una nueva clase Java llamada `SearchController` en el paquete `com.example.search.controller`. La clase `SearchController` debería verse así:

```java
package com.example.search.controller;

import com.example.search.document.SearchDocument;
import com.example.search.service.SearchService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/search")
public class SearchController {

    @Autowired
    private SearchService searchService;

    @PostMapping
    public void indexDocument(@RequestBody SearchDocument document) {
        searchService.indexDocument(document);
    }

}
```

En la clase `SearchController`, hemos inyectado un objeto `SearchService`. También hemos creado un método anotado `@PostMapping` llamado `indexDocument` que acepta un objeto `SearchDocument`.

En el método `indexDocument`, hemos llamado al método `indexDocument` en el objeto `SearchService` para indexar el documento.

### Paso 8: compilar y ejecutar la aplicación

Ahora que tenemos nuestra aplicación creada, podemos compilarla y ejecutarla. Esto lo podemos hacer ejecutando el siguiente comando:

```
mvn spring-boot:run
```

Una vez que la aplicación está en funcionamiento, podemos indexar un documento enviando una solicitud POST al extremo `/search` con un objeto `SearchDocument` en el cuerpo de la solicitud.

## Conclusión

En esta publicación, le mostramos cómo crear un motor de búsqueda con Spring Boot y Solr. También le mostramos cómo configurar Solr y cómo indexar documentos.