---
title: 073: Integración de Spring Boot con Elasticsearch para búsqueda y análisis
description: 
published: true
date: 2023-02-02T04:43:40.724Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:43:39.048Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [073: Integrating Spring Boot with Elasticsearch for Search and Analytics***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}


# Introducción

Elasticsearch es un potente motor de análisis y búsqueda de código abierto que facilita la exploración de los datos. Spring Boot es un marco de aplicación de Java popular que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

En esta publicación, mostraremos cómo integrar Spring Boot con Elasticsearch para búsqueda y análisis. Primero crearemos una aplicación Spring Boot y agregaremos las dependencias requeridas. Luego, crearemos un índice de Elasticsearch y le agregaremos algunos datos. Finalmente, escribiremos una aplicación Spring Boot que use las API de Elasticsearch para buscar y agregar datos del índice.

# requisitos previos

Para seguir con esta publicación, necesitará lo siguiente:

-JDK 8 o posterior
-Gradle 4.0 o posterior

# Creación de una aplicación Spring Boot

Comenzaremos creando una aplicación Spring Boot. Usaremos Spring Initializr para generar una estructura de proyecto básica. Navegue a http://start.spring.io/ y seleccione las siguientes opciones:

- Proyecto: Proyecto Gradle
- Idioma: Java
- Versión de arranque de primavera: 2.0.3
- Metadatos del proyecto:
  - Grupo: com.ejemplo
  - Artefacto: spring-boot-elasticsearch
  - Nombre: Spring Boot Elasticsearch
  - Descripción: una aplicación Spring Boot que se integra con Elasticsearch
  - Nombre del paquete: com.example.springbootelasticsearch
  - Envase: Tarro
  - Versión Java: 8
  - Dependencias: Web, Lombok

Haga clic en "Generar proyecto" para descargar el archivo del proyecto. Extraiga el archivo e importe el proyecto a su IDE favorito.

# Agregar dependencias

A continuación, debemos agregar las dependencias requeridas a nuestro proyecto. Necesitaremos las siguientes dependencias:

- Spring Data Elasticsearch: Brinda soporte para Elasticsearch en aplicaciones Spring
- Elasticsearch: El propio motor de Elasticsearch
- Lombok: una biblioteca que puede generar código repetitivo para nosotros

Agregue las siguientes dependencias a la sección `dependencias` de su archivo `build.gradle`:

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-data-elasticsearch')
    compile('org.elasticsearch:elasticsearch:6.3.2')
    compileOnly('org.projectlombok:lombok')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

# Configurando Elasticsearch

A continuación, debemos configurar Elasticsearch. De forma predeterminada, Spring Boot buscará una instancia de Elasticsearch en `http://localhost:9200`. Si tiene Elasticsearch ejecutándose en un host o puerto diferente, puede configurarlo configurando las propiedades `spring.data.elasticsearch.cluster-nodes` y `spring.data.elasticsearch.cluster-name` en su `application.properties` expediente. Por ejemplo:

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=my-cluster
```

# Creación de un índice de Elasticsearch

Un índice de Elasticsearch es una colección de documentos que tienen características similares. Podemos pensar en un índice como una tabla en una base de datos relacional. Así como necesitamos crear una tabla antes de poder insertar datos en ella, necesitamos crear un índice antes de poder agregarle documentos.

Podemos usar las API de Elasticsearch para crear un índice. El siguiente ejemplo crea un índice llamado `clientes` con los campos `nombre` y `dirección`:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testCreateIndex() {
    operations.createIndex(Customer.class);
}
```

# Agregar datos al índice

Una vez que hemos creado un índice, podemos agregarle documentos. Un documento es un objeto JSON que contiene los datos que queremos indexar. En nuestro ejemplo, indexaremos registros de clientes. Cada registro de cliente tendrá un `nombre` y una `dirección`.

Podemos usar las API de Elasticsearch para indexar documentos. El siguiente ejemplo indexa un registro de cliente:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testIndex() {
    Customer customer = new Customer();
    customer.setName("John Smith");
    customer.setAddress("123 Main Street");

    operations.index(customer);
}
```

# Buscando en el índice

Ahora que hemos agregado algunos datos a nuestro índice, podemos buscarlos. Podemos usar las API de Elasticsearch para buscar documentos. El siguiente ejemplo busca registros de clientes que tengan el nombre "John Smith":

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testSearch() {
    QueryBuilder query = QueryBuilders.queryStringQuery("name:John Smith");
    SearchHits<Customer> customers = operations.search(query, Customer.class);

    assertEquals(1, customers.getTotalHits());
    assertEquals("John Smith", customers.getSearchHit(0).getContent().getName());
}
```

# Agregando datos

Además de buscar documentos, también podemos agregar datos del índice. Podemos usar las API de Elasticsearch para ejecutar agregaciones. El siguiente ejemplo agrega registros de clientes por estado:

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testAggregation() {
    QueryBuilder query = QueryBuilders.matchAllQuery();
    AggregationBuilder aggregation = AggregationBuilders.terms("by_state").field("address.state");
    SearchQuery searchQuery = new NativeSearchQueryBuilder()
            .withQuery(query)
            .withSearchType(SearchType.QUERY_THEN_FETCH)
            .withIndices("customers")
            .withTypes("customer")
            .addAggregation(aggregation)
            .build();

    Aggregations aggregations = operations.query(searchQuery, SearchResponse::getAggregations);
    StringTerms byStateAggregation = aggregations.get("by_state");
    assertEquals(2, byStateAggregation.getBuckets().size());
    assertEquals("CA", byStateAggregation.getBucketByKey("CA").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("CA").getDocCount());
    assertEquals("TX", byStateAggregation.getBucketByKey("TX").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("TX").getDocCount());
}
```

# Conclusión

En esta publicación, mostramos cómo integrar Spring Boot con Elasticsearch para búsqueda y análisis. Primero creamos una aplicación Spring Boot y agregamos las dependencias requeridas. Luego creamos un índice de Elasticsearch y le agregamos algunos datos. Finalmente, hemos escrito una aplicación Spring Boot que usa las API de Elasticsearch para buscar y agregar datos del índice.